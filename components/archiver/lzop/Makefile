#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"). You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2013 Adam Stevko. All rights reserved.
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		lzop
COMPONENT_VERSION=	1.0.4
HUMAN_VERSION=		1.04
COMPONENT_REVISION=	2
COMPONENT_SUMMARY=	Dictionary-based LZ-type compressor favoring speed
COMPONENT_SRC=		$(COMPONENT_NAME)-$(HUMAN_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	sha256:7e72b62a8a60aff5200a047eea0773a8fb205caf7acbe1774d95147f305a2f41
COMPONENT_PROJECT_URL=	https://www.lzop.org
COMPONENT_ARCHIVE_URL=	https://www.lzop.org/download/$(COMPONENT_ARCHIVE)
COMPONENT_FMRI=	compress/$(COMPONENT_NAME)
COMPONENT_CLASSIFICATION=	Applications/System Utilities
COMPONENT_LICENSE=	GPLv2

include $(WS_MAKE_RULES)/common.mk

# Auto-generated dependencies
REQUIRED_PACKAGES += library/lzo
REQUIRED_PACKAGES += system/library
