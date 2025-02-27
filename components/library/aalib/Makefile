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

#
# Copyright (c) 2011, 2013, Oracle and/or its affiliates. All rights reserved.
#

BUILD_BITS= 32_and_64
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=         aalib
COMPONENT_VERSION=      1.4.0
HUMAN_VERSION=		1.4rc5
IPS_COMPONENT_VERSION =	1.4.5
COMPONENT_REVISION=     4
COMPONENT_SRC=          $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_PROJECT_URL=  https://aa-project.sourceforge.net/aalib/
COMPONENT_ARCHIVE=      $(COMPONENT_NAME)-$(HUMAN_VERSION).tar.gz
COMPONENT_ARCHIVE_HASH= sha256:fbddda9230cf6ee2a4f5706b4b11e2190ae45f5eda1f0409dc4f99b35e0a70ee
COMPONENT_ARCHIVE_URL=  https://downloads.sourceforge.net/aa-project/$(COMPONENT_ARCHIVE)

CONFIGURE_FIX_LIBTOOL_RPATH = no

TEST_TARGET= $(NO_TESTS)
include $(WS_MAKE_RULES)/common.mk

PKG_PROTO_DIRS += $(COMPONENT_SRC)

COMPONENT_PREP_ACTION= (cd $(@D) && autoreconf -fi)

# We need to reset configure options here because aalib is confused with
# CC and CFLAGS definitions as configure parameters.
CONFIGURE_OPTIONS += --prefix=/usr
CONFIGURE_OPTIONS += --infodir=$(CONFIGURE_INFODIR)
CONFIGURE_OPTIONS += --mandir=$(CONFIGURE_MANDIR)
CONFIGURE_OPTIONS += --bindir=$(CONFIGURE_BINDIR.$(BITS))
CONFIGURE_OPTIONS += --libdir=$(CONFIGURE_LIBDIR.$(BITS))
CONFIGURE_OPTIONS += --enable-shared
CONFIGURE_OPTIONS += --disable-static
CONFIGURE_OPTIONS += --x-includes=/usr/include
CONFIGURE_OPTIONS += --x-libraries=$(CONFIGURE_LIBDIR.$(BITS))
CONFIGURE_OPTIONS += $(CONFIGURE_OPTIONS.$(BITS))

ASLR_MODE= $(ASLR_ENABLE)

# actually there is a test we put in the demos,
# but it's 32-bit only and not a target

# Auto-generated dependencies
REQUIRED_PACKAGES += library/slang
REQUIRED_PACKAGES += shell/ksh93
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
REQUIRED_PACKAGES += x11/library/libx11
