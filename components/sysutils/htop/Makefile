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
# Copyright 2018, Aurelien Larcher
# Copyright 2020, Michal Nowak
# Copyright 2020, 2021 Andreas Wacknitz
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		htop
COMPONENT_VERSION=	3.2.2
COMPONENT_SUMMARY=	htop - an interactive process viewer for Unix
COMPONENT_PROJECT_URL=	https://htop.dev/
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH= sha256:3829c742a835a0426db41bb039d1b976420c21ec65e93b35cd9bfd2d57f44ac8
COMPONENT_ARCHIVE_URL=	https://github.com/htop-dev/$(COMPONENT_NAME)/archive/$(COMPONENT_VERSION).tar.gz
COMPONENT_FMRI=		diagnostic/htop
COMPONENT_CLASSIFICATION=	Applications/System Utilities
COMPONENT_LICENSE=  GPLv2 

TEST_TARGET= $(NO_TESTS)
include $(WS_MAKE_RULES)/common.mk

PATH=$(GNUBIN64):$(PATH.gnu)

COMPONENT_PREP_ACTION= ( cd $(@D); $(RM) config.h; sh autogen.sh )

# Auto-generated dependencies
REQUIRED_PACKAGES += library/ncurses
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
