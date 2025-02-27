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
# Copyright (c) 2016 Predrag Zečević
# Copyright (c) 2020 Michal Nowak
#

BUILD_BITS=		64
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=           aria2
COMPONENT_VERSION=        1.36.0
COMPONENT_REVISION=       1
COMPONENT_FMRI=           web/aria2
COMPONENT_PROJECT_URL=    https://aria2.github.io/
COMPONENT_CLASSIFICATION= Applications/Internet
COMPONENT_SUMMARY=	aria2 - lightweight multi-protocol and multi-source download utility
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_HASH=	sha256:58d1e7608c12404f0229a3d9a4953d0d00c18040504498b483305bcb3de907a5
COMPONENT_ARCHIVE_URL=	https://github.com/aria2/aria2/releases/download/release-$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)
COMPONENT_LICENSE=	GPLv3

include $(WS_MAKE_RULES)/common.mk

PATH=$(PATH.gnu)

LDFLAGS += -lsocket -lnsl

CONFIGURE_OPTIONS += --disable-static
CONFIGURE_OPTIONS += --with-ca-bundle=/etc/certs/ca-certificates.crt
CONFIGURE_OPTIONS += --with-bashcompletiondir=/usr/share/bash-completion/completions/

CONFIGURE_ENV += LD_OPTIONS="$(LD_OPTIONS)"

COMPONENT_TEST_ENV += LD_OPTIONS="$(LD_OPTIONS)"

# Tests may output some compilation lines, so just pull out the relevant test
# output lines for the test results comparison.
COMPONENT_TEST_TRANSFORMS += \
	'-n ' \
	'-e "/TOTAL:/p" ' \
	'-e "/PASS:/p" ' \
	'-e "/SKIP:/p" ' \
	'-e "/XFAIL:/p" ' \
	'-e "/FAIL:/p" ' \
	'-e "/XPASS:/p" ' \
	'-e "/ERROR:/p" '

# We have one failing test (from test-suite.log):
# 09/26 19:19:47 [INFO] Processing metaurl group metaurl=README.torrent
# 09/26 19:19:47 [ERROR] Unrecognized URI or unsupported protocol: README.torrent

# cppunit is for tests
REQUIRED_PACKAGES += developer/cppunit

# Auto-generated dependencies
REQUIRED_PACKAGES += $(GCC_RUNTIME_PKG)
REQUIRED_PACKAGES += $(GXX_RUNTIME_PKG)
REQUIRED_PACKAGES += database/sqlite-3
REQUIRED_PACKAGES += library/gmp
REQUIRED_PACKAGES += library/libcares
REQUIRED_PACKAGES += library/gnutls-3
REQUIRED_PACKAGES += library/libssh2
REQUIRED_PACKAGES += library/libxml2
REQUIRED_PACKAGES += library/nettle
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
