#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2013 Alexander Pyhalov.  All rights reserved.
# Copyright 2017 Aurelien Larcher.  All rights reserved.
#

BUILD_BITS= 32_and_64
USE_DEFAULT_TEST_TRANSFORMS= yes
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME= libsigc++
COMPONEN_MAJOR_VERSION=	2.10
COMPONENT_VERSION= $(COMPONEN_MAJOR_VERSION).0
COMPONENT_REVISION= 1
COMPONENT_SUMMARY= Libsigc++ - a library that implements a typesafe callback system for standard C++ (g++ - compiled)
COMPONENT_PROJECT_URL = http://libsigc.sourceforge.net
COMPONENT_SRC= $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE= $(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_HASH= sha256:f843d6346260bfcb4426259e314512b99e296e8ca241d771d21ac64f28298d81
COMPONENT_ARCHIVE_URL= https://download.gnome.org/sources/libsigc++/$(COMPONEN_MAJOR_VERSION)/$(COMPONENT_ARCHIVE)
COMPONENT_FMRI= library/c++/sigcpp
COMPONENT_CLASSIFICATION=	Development/C++ 
COMPONENT_LICENSE= LGPLv2.1 

include $(WS_MAKE_RULES)/common.mk

# Missing files in build dir for configure without this.
COMPONENT_PRE_CONFIGURE_ACTION = ($(CLONEY) $(SOURCE_DIR) $(@D))  

CONFIGURE_OPTIONS += --sysconfdir=$(ETCDIR)
CONFIGURE_OPTIONS += MAKE=$(GMAKE)

# Test failure
unexport SHELLOPTS

# Auto-generated dependencies
REQUIRED_PACKAGES += $(GCC_RUNTIME_PKG)
REQUIRED_PACKAGES += $(GXX_RUNTIME_PKG)
REQUIRED_PACKAGES += system/library
