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
# Copyright (c) 2008, 2018, Oracle and/or its affiliates. All rights reserved.
# COpyright 2018, Aurelien Larcher
#

BUILD_STYLE=configure
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		font-isas-misc
COMPONENT_VERSION= 	1.0.4
COMPONENT_SUMMARY=      Institute of Software, Academia Sinica GB2312-80 bitmap fonts
COMPONENT_ARCHIVE_EXTENSION= .tar.xz
COMPONENT_ARCHIVE_HASH=	sha256:47e595bbe6da444b9f6fcaa26539abc7ba1989e23afa6cdc49e22e484cc438fc
COMPONENT_LICENSE=      MIT
COMPONENT_LICENSE_FILE= COPYING

FONT_TYPE = X11MISC

include $(WS_MAKE_RULES)/font.mk

COMPONENT_FONT_NAME = isas
COMPONENT_FONT_PKG  = isas-misc

# Install to separate directory for easier packaging
CONFIGURE_OPTIONS += --with-fontdir=$(COMPONENT_FONT_DEST_DIR)

# Auto-generated dependencies
