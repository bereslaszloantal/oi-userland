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
# Copyright 2015 Alexander Pyhalov
#

BUILD_STYLE=configure
BUILD_BITS=64
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=         xvidcore
COMPONENT_VERSION=      1.3.7
COMPONENT_REVISION=     1
COMPONENT_FMRI=         library/video/xvid
COMPONENT_CLASSIFICATION=System/Multimedia Libraries
COMPONENT_SUMMARY=      ISO MPEG-4 compliant video codec
COMPONENT_SRC=          $(COMPONENT_NAME)
COMPONENT_ARCHIVE=      $(COMPONENT_SRC)-$(COMPONENT_VERSION).tar.gz
COMPONENT_ARCHIVE_HASH= \
	sha256:abbdcbd39555691dd1c9b4d08f0a031376a3b211652c0d8b3b8aa9be1303ce2d
COMPONENT_ARCHIVE_URL=  \
	https://downloads.xvid.com/downloads/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL=  https://www.xvid.com/
COMPONENT_LICENSE=      GPLv2.0
COMPONENT_LICENSE_FILE= LICENSE

include $(WS_MAKE_RULES)/encumbered.mk
TEST_TARGET=$(NO_TESTS)
include $(WS_MAKE_RULES)/common.mk

PATH = $(PATH.gnu)

COMPONENT_PREP_ACTION += ( cd $(COMPONENT_SRC)/build/generic && $(CONFIG_SHELL) bootstrap.sh)

# Missing files in build dir for configure without this.
COMPONENT_PRE_CONFIGURE_ACTION = ($(CLONEY) $(SOURCE_DIR) $(@D))

CONFIGURE_OPTIONS+= --enable-assembly
CONFIGURE_OPTIONS+= --target=amd64-pc-solaris2.11

CONFIGURE_SCRIPT = $(@D)/build/generic/configure

$(BUILD_DIR)/%/.configured:     $(SOURCE_DIR)/.prep
	($(RM) -rf $(@D) ; $(MKDIR) $(@D))
	$(COMPONENT_PRE_CONFIGURE_ACTION)
	(cd $(@D)/build/generic ; $(ENV) $(CONFIGURE_ENV) $(CONFIG_SHELL) \
	        $(CONFIGURE_SCRIPT) $(CONFIGURE_OPTIONS))
	$(COMPONENT_POST_CONFIGURE_ACTION)
	$(TOUCH) $@

COMPONENT_BUILD_ARGS += -C $(@D)/build/generic
COMPONENT_INSTALL_ARGS += -C $(@D)/build/generic

# Auto-generated dependencies
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
