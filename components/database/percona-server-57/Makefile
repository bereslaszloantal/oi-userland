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
# Copyright 2011-2013, EveryCity Ltd. All rights reserved.
# Copyright 2019, Michal Nowak
# 

BUILD_BITS=			32_and_64
BUILD_STYLE=		cmake
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		percona-server
COMPONENT_VERSION =	5.7.39-42
IPS_COMPONENT_VERSION =	5.7.39.42
COMPONENT_SRC=		$(COMPONENT_NAME)-$(HUMAN_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_PROJECT_URL=	https://www.percona.com/
COMPONENT_ARCHIVE_HASH=	sha256:bda853fb951eef8be1c2f24391798cf1f3377c776a376f4c55b192e42ae8d1b2
COMPONENT_ARCHIVE_URL=	https://www.percona.com/downloads/Percona-Server-5.7/Percona-Server-$(COMPONENT_VERSION)/source/tarball/$(COMPONENT_ARCHIVE)

# We need specific boost version
COMPONENT_ARCHIVE_1= boost_1_59_0.tar.gz
COMPONENT_ARCHIVE_HASH_1=	sha256:47f11c8844e579d02691a607fbd32540104a9ac7a2534a8ddaef50daf502baac
COMPONENT_ARCHIVE_URL_1=	https://downloads.sourceforge.net/project/boost/boost/1.59.0/$(COMPONENT_ARCHIVE_1)

include $(WS_MAKE_RULES)/common.mk

COMPONENT_POST_UNPACK_ACTION = ( $(MKDIR) $(BUILD_DIR)/boost && /usr/gnu/bin/tar -C $(BUILD_DIR)/boost -xzf $(USERLAND_ARCHIVES)$(COMPONENT_ARCHIVE_1))

CMAKE_PREFIX=/usr/percona-server/5.7
CONFDIR=/etc/percona-server/5.7
DATA_PREFIX=/var/percona-server/5.7

CMAKE_PLUGINDIR.32 =	lib/plugin
CMAKE_PLUGINDIR.64 =	lib/$(MACH64)/plugin

# Make sure GCC 6 is accepted
CMAKE_OPTIONS+= -DFORCE_UNSUPPORTED_COMPILER=ON
CMAKE_OPTIONS+= -DCMAKE_BUILD_TYPE=RELEASE
CMAKE_OPTIONS+=	-DWITH_SSL=system
CMAKE_OPTIONS+= -DINSTALL_LAYOUT=SVR4
CMAKE_OPTIONS+= -DINSTALL_BINDIR=$(CMAKE_BINDIR.$(BITS))
CMAKE_OPTIONS+= -DINSTALL_INCLUDEDIR=include
CMAKE_OPTIONS+= -DINSTALL_INFODIR=bin
CMAKE_OPTIONS+= -DINSTALL_LIBDIR=$(CMAKE_LIBDIR.$(BITS))
CMAKE_OPTIONS+= -DINSTALL_PLUGINDIR=$(CMAKE_PLUGINDIR.$(BITS))
CMAKE_OPTIONS+= -DINSTALL_MANDIR=man
CMAKE_OPTIONS+= -DINSTALL_SHAREDIR=share
CMAKE_OPTIONS+= -DINSTALL_MYSQLSHAREDIR=share
CMAKE_OPTIONS+= -DINSTALL_SBINDIR=$(CMAKE_BINDIR.$(BITS))
CMAKE_OPTIONS+= -DINSTALL_SCRIPTDIR=$(CMAKE_BINDIR.$(BITS))
CMAKE_OPTIONS+= -DMYSQL_DATADIR=$(DATA_PREFIX)/data
CMAKE_OPTIONS+= -DSYSCONFDIR=$(CONFDIR)
CMAKE_OPTIONS+= -DENABLE_DTRACE=on
CMAKE_OPTIONS+= -DINSTALL_SUPPORTFILESDIR=share/mysql
CMAKE_OPTIONS+= -DWITH_BOOST=$(BUILD_DIR)/boost
CMAKE_OPTIONS+= -DINSTALL_SECURE_FILE_PRIVDIR=""

# gcc invocation in some link.txt file is missing -m$(BITS) parameter
# and it makes 64-bit build to fail, this is a quick hack to make it build
# for now, cmake build system needs a proper fix
COMPONENT_POST_CMAKE_ACTION.32=
COMPONENT_POST_CMAKE_ACTION.64= find $(@D) -type f -name link.txt \
    -exec perl -pi -e 's/gcc\ \ -fPIC/\/gcc\ -m64\ -fPIC/' {} \;
COMPONENT_POST_CMAKE_ACTION=$(COMPONENT_POST_CMAKE_ACTION.$(BITS))

# Auto-generated dependencies
REQUIRED_PACKAGES += $(GCC_RUNTIME_PKG)
REQUIRED_PACKAGES += $(GXX_RUNTIME_PKG)
#REQUIRED_PACKAGES += database/percona-server-57/client
REQUIRED_PACKAGES += library/readline
REQUIRED_PACKAGES += library/security/openssl
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += runtime/perl
REQUIRED_PACKAGES += shell/bash
REQUIRED_PACKAGES += shell/ksh93
REQUIRED_PACKAGES += SUNWcs
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
REQUIRED_PACKAGES += system/library/security/libsasl
REQUIRED_PACKAGES += web/curl
