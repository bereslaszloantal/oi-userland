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
# Copyright 2011 EveryCity Ltd. All rights reserved.
# Copyright 2021 Andreas Wacknitz. All rights reserved.
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		developer-gnu
COMPONENT_VERSION=	1.0
COMPONENT_SUMMARY=	GNU Tools Development cluster
COMPONENT_CLASSIFICATION=	Meta Packages/Group Packages
COMPONENT_FMRI=		developer/gnu

include ../../../make-rules/ips.mk

#PKGLINT=/bin/true

download:

prep:

build:

install:
	[ -d $(PROTO_DIR) ] || mkdir -p $(PROTO_DIR)

clean:
	$(RM) -r $(BUILD_DIR) $(PROTO_DIR)
