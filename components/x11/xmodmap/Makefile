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
# Copyright 2015 Aurelien Larcher
#

X11_CATEGORY=APP
include ../../../make-rules/shared-macros.mk
include $(WS_MAKE_RULES)/x11.mk

COMPONENT_NAME=     xmodmap
COMPONENT_VERSION=  1.0.11
COMPONENT_FMRI=     x11/xmodmap
COMPONENT_SUMMARY=  xmodmap - X11 keyboard/mouse mapping configuration utility
COMPONENT_ARCHIVE_EXTENSION= .tar.gz
COMPONENT_ARCHIVE_HASH= \
  sha256:c4fac9df448b98ac5a1620f364e74ed5f7084baae0d09123700f34d4b63cb5d8

include $(WS_MAKE_RULES)/common.mk

# Auto-generated dependencies
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += x11/library/libx11
