#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL)". You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2015 Alexander Pyhalov
#

BUILD_BITS= 32_and_64
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=         id3lib
COMPONENT_VERSION=      3.8.3
COMPONENT_REVISION=     2
COMPONENT_SUMMARY=      id3lib - a software library for manipulating ID3v1/v1.1 and ID3v2 tags
COMPONENT_PROJECT_URL=  https://id3lib.sourceforge.net/
COMPONENT_SRC=          $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=      $(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH= sha256:2749cc3c0cd7280b299518b1ddf5a5bcfe2d1100614519b68702230e26c7d079
COMPONENT_ARCHIVE_URL=  https://sourceforge.net/projects/id3lib/files/id3lib/$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)/download/
COMPONENT_FMRI=         library/id3lib
COMPONENT_CLASSIFICATION=System/Multimedia Libraries
COMPONENT_LICENSE=      LGPLv2
COMPONENT_LICENSE_FILE= COPYING

include $(WS_MAKE_RULES)/common.mk

COMPONENT_PREP_ACTION= ( cd $(@D)  && \
	libtoolize --copy --force && \
	aclocal -I m4 && \
	autoheader && \
	automake -c -f -a && \
	autoconf )

FP_ARCH.32 = default
FP_ARCH.64 = 64bit

CONFIGURE_OPTIONS += --sysconfdir=/etc
CONFIGURE_OPTIONS += --enable-shared
CONFIGURE_OPTIONS += --disable-static
CONFIGURE_OPTIONS += --enable-fpm=$(FP_ARCH.$(BITS))

# Auto-generated dependencies
REQUIRED_PACKAGES += $(GCC_RUNTIME_PKG)
REQUIRED_PACKAGES += $(GXX_RUNTIME_PKG)
REQUIRED_PACKAGES += system/library
