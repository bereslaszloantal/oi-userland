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
# Copyright (c) 2015-2017, Aurelien Larcher 
#
BUILD_BITS= 64_and_32
USE_COMMON_TEST_MASTER= no
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME =        lcms2
COMPONENT_MJR_VERSION=	2.15
COMPONENT_VERSION=      $(COMPONENT_MJR_VERSION)
COMPONENT_SUMMARY=      The Little Color Management System
COMPONENT_SRC=          $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_PROJECT_URL=  https://www.littlecms.com/
COMPONENT_ARCHIVE=      $(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	sha256:b20cbcbd0f503433be2a4e81462106fa61050a35074dc24a4e356792d971ab39
COMPONENT_ARCHIVE_URL=	https://sourceforge.net/projects/lcms/files/lcms/$(COMPONENT_MJR_VERSION)/$(COMPONENT_ARCHIVE)
COMPONENT_FMRI=         library/lcms2
COMPONENT_CLASSIFICATION=System/Libraries
COMPONENT_LICENSE=      MIT
COMPONENT_LICENSE_FILE= COPYING

include $(WS_MAKE_RULES)/common.mk

# build with the distribution preferred libjpeg implementation
CFLAGS   += $(JPEG_CPPFLAGS) $(JPEG_CFLAGS)
CXXFLAGS += $(JPEG_CPPFLAGS) $(JPEG_CXXFLAGS)
LDFLAGS  += $(JPEG_LDFLAGS)

# Seems that we have no other way to designate that we want large file support.
CFLAGS += $(CPP_LARGEFILES)

# Need to ensure lcms custom chunk memory allocator aligns properly for all
# of our platforms - see _cmsALIGNMEM macro in src/lcms2_internal.h and
# _MAX_ALIGNMENT definition in per-platform sections of <sys/isa_defs.h>
CPPFLAGS += -DCMS_PTR_ALIGNMENT=_MAX_ALIGNMENT

CONFIGURE_OPTIONS += --includedir=/usr/include/lcms2
CONFIGURE_OPTIONS += --enable-shared
CONFIGURE_OPTIONS += --disable-static
CONFIGURE_OPTIONS += --with-jpeg
CONFIGURE_OPTIONS += --with-tiff
CONFIGURE_OPTIONS += --with-zlib
CONFIGURE_OPTIONS += --with-pic

COMPONENT_PRE_TEST_ACTION = ( cd $(@D); $(MAKE) -C testbed clean )

COMPONENT_TEST_ARGS = -k -i
COMPONENT_TEST_TRANSFORMS += \
	'-e "s|^.*test bed.*$$|XXX_REMOVE_XXX|g" ' \
	'-e "s|^.*MPixel.*$$|XXX_REMOVE_XXX|g" ' \
	'-e "s|^.*Single block hit.*$$|XXX_REMOVE_XXX|g" ' \
	'-e "s|^.*$(CC).*$$|XXX_REMOVE_XXX|g" ' \
	'-e "s|^.*source=.*libtool=no.*$$|XXX_REMOVE_XXX|g" ' \
	'-e "s|^.*DEPDIR=.deps.*$$|XXX_REMOVE_XXX|g" ' \
	'-e "s|^make.*(ignored)*$$|XXX_REMOVE_XXX|g" ' \
	'-e "s|^make.*: Leaving directory.*$$|XXX_REMOVE_XXX|g" ' \
	'-e "s|^make.*: Entering directory.*$$|XXX_REMOVE_XXX|g" ' \
	'-e "/^XXX_REMOVE_XXX$$/d" '

# Auto-generated dependencies
REQUIRED_PACKAGES += $(JPEG_IMPLEM_PKG)
REQUIRED_PACKAGES += image/library/libtiff
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
