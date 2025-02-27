#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#
# Copyright (c) 2011, 2020, Oracle and/or its affiliates.
#

BUILD_BITS= 32_and_64
include ../../../../make-rules/shared-macros.mk

COMPONENT_VERSION_SHORT= 3.1
COMPONENT_NAME=	openssl-$(COMPONENT_VERSION_SHORT)

COMPONENT_VERSION=	3.1.1
COMPONENT_FMRI=		library/security/openssl-31
COMPONENT_CLASSIFICATION=System/Security
COMPONENT_SUMMARY=	OpenSSL - a Toolkit for Transport Layer (TLS v1+) protocols and general purpose cryptographic library
COMPONENT_PROJECT_URL=	https://www.openssl.org/
COMPONENT_SRC=		openssl-$(HUMAN_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	sha256:b3aa61334233b852b63ddb048df181177c2c659eb9d4376008118f9c08d07674
COMPONENT_ARCHIVE_URL=	$(COMPONENT_PROJECT_URL)source/$(COMPONENT_ARCHIVE)
COMPONENT_LICENSE=	OpenSSL, SSLeay

include $(WS_MAKE_RULES)/common.mk

PATH= $(GCC_ROOT)/bin:$(PATH.illumos)

# OpenSSL does not use autoconf but its own configure system.
CONFIGURE_SCRIPT = $(SOURCE_DIR)/Configure
CONFIG_SHELL=

# This is to force OpenSSL's Configure script to use gmake for 'make links'.
# Otherwise it fails with:
#     mksh: Fatal error in reader: Unmatched `(' on line
CONFIGURE_ENV += MAKE="$(GMAKE)"

CONFIGURE_OPTIONS = -DNO_WINDOWS_BRAINDEATH
CONFIGURE_OPTIONS += --openssldir=/etc/openssl/3.1
CONFIGURE_OPTIONS += --prefix=/usr/openssl/3.1
CONFIGURE_OPTIONS += --libdir=lib/$(ARCHLIBSUBDIR)
# comply with API 1.0 for now
CONFIGURE_OPTIONS += --api=1.1.1
CONFIGURE_OPTIONS += shared threads zlib

CONFIGURE_OPTIONS.64 += enable-ec_nistp_64_gcc_128

# We define our own compiler and linker option sets for Solaris. See Configure
# for more information.
CONFIGURE_OPTIONS32_i386 =	solaris-x86-gcc
CONFIGURE_OPTIONS32_sparc =	solaris-sparcv9-gcc
CONFIGURE_OPTIONS64_i386 =	solaris64-x86_64-gcc
CONFIGURE_OPTIONS64_sparc =	solaris64-sparcv9-gcc

# Options specific to regular build.
# They must not be specified as common, as they cannot be overridden.
$(BUILD_DIR)/$(MACH32)/.configured:	CONFIGURE_OPTIONS += \
	$(CONFIGURE_OPTIONS32_$(MACH))
$(BUILD_DIR)/$(MACH64)/.configured:	CONFIGURE_OPTIONS += \
	$(CONFIGURE_OPTIONS64_$(MACH))

# OpenSSL has its own configure system which must be run from the fully
# populated source code directory. However, the Userland configuration phase is
# run from the build directory. So, we must get the full source code into the
# build directory.
COMPONENT_PRE_CONFIGURE_ACTION = \
      $(CLONEY) $(SOURCE_DIR) $(BUILD_DIR)/$(MACH$(BITS)) && \
      echo $(PROTO_DIR); echo "RunPath"; echo $(BITS); echo $(WS_MAKE_RULES);

# Add -znodelete to compiler commands as that otherwise breaks some dynamic unloading stuff. See patchfile for details
COMPONENT_POST_CONFIGURE_ACTION = \
      $(GPATCH) -p1 --verbose $(@D)/Makefile patches-post-config/Makefile.patch

#
# The test 'test_ca' is removed because it depends on directories not present
# in the build directory.
#
COMPONENT_POST_CONFIGURE_ACTION = \
    ( echo "Patching Makefile..." && \
      $(GPATCH) -p0 $(@D)/Makefile patches-post-config/Makefile.patch && \
      echo "Removing test_ca test" && \
      $(RM) $(SOURCE_DIR)/test/recipes/*-test_ca.t $(@D)/test/recipes/*-test_ca.t; )

# We add /usr/perl5/bin to PATH so that OpenSSL install code can locate the
# system pod2man. If not set, OpenSSL make would use an internal implementation
# from the tarball which would corrupt some man pages.
#
# The MANSUFFIX needs to be complemented by patches/002-man_page_suffix.patch
COMPONENT_INSTALL_ARGS += PATH=$(PATH) MANSUFFIX=openssl

# Lint targets expect that PROTOUSRLIBDIR{,64} directories exist.
# Since everything is installed into distinct directory trees, these
# need to be created explicitly. These actions are probably temporary -
# once 1.1 will start deliver to the usual directories, these can be removed.
COMPONENT_PRE_INSTALL_ACTION += (\
	echo "Ensuring library directories exist in the proto area"; \
	test -d $(PROTOUSRLIBDIR) || $(MKDIR) $(PROTOUSRLIBDIR); \
	test -d $(PROTOUSRLIBDIR64) || $(MKDIR) $(PROTOUSRLIBDIR64);)

#
# There is also separate STC test suite 'openssl'
# for regression testing. These internal tests are unit tests only.
#
COMPONENT_TEST_TARGETS = test

COMPONENT_TEST_TRANSFORMS = \
        '-n ' \
        '-e "/PASS/p" ' \
        '-e "/skipped/p" ' \
        '-e "/ok/p" ' \
        '-e "/success/p" '

REQUIRED_PACKAGES += developer/build/makedepend

# Auto-generated dependencies
REQUIRED_PACKAGES += SUNWcs
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += runtime/perl
REQUIRED_PACKAGES += system/library
