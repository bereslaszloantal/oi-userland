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
# Copyright 2017 Alexander Pyhalov
# Copyright 2019 Michal Nowak
#

BUILD_STYLE=justmake
BUILD_BITS=64
USE_OPENSSL11=          yes
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=         mongodb
COMPONENT_MAJOR_VERSION=3.4
COMPONENT_MINOR_VERSION=19
COMPONENT_VERSION=      $(COMPONENT_MAJOR_VERSION).$(COMPONENT_MINOR_VERSION)
COMPONENT_REVISION=     2
COMPONENT_SUMMARY=      MongoDB distributed document-oriented database
COMPONENT_PROJECT_URL=  https://www.mongodb.com/
COMPONENT_FMRI=         database/mongodb-34
COMPONENT_CLASSIFICATION=System/Databases
COMPONENT_SRC=          $(COMPONENT_NAME)-src-r$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=      $(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_URL=  https://fastdl.mongodb.org/src/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH= sha256:a05938cc118fb796ae37bb22503979a1ca3a0a5016040f3daf388ca21e9bfcba
COMPONENT_LICENSE=      GNU-AGPL-3.0
COMPONENT_LICENSE_FILE= GNU-AGPL-3.0.txt

include $(WS_MAKE_RULES)/common.mk

BUILD_TOOLS=	$(BUILD_DIR)/tools/.built
INSTALL_TOOLS=	$(BUILD_DIR)/tools/.installed

MONGO_PREFIX=	usr/mongodb/$(COMPONENT_MAJOR_VERSION)

GMAKE=/usr/bin/scons

COMPONENT_BUILD_ARGS += TARGET_ARCH=x86_64
COMPONENT_BUILD_ARGS += CXXFLAGS="$(CXXFLAGS)"
COMPONENT_BUILD_ARGS += CC="$(CC)"
COMPONENT_BUILD_ARGS += CXX="$(CXX)"
COMPONENT_BUILD_ARGS += CFLAGS="$(CFLAGS)"
COMPONENT_BUILD_ARGS += LIBPATH=/usr/lib/$(MACH64)
COMPONENT_BUILD_ARGS += LINKFLAGS="$(LDFLAGS)"

COMPONENT_BUILD_ARGS += --prefix=$(PROTO_DIR)/$(MONGO_PREFIX)
COMPONENT_BUILD_ARGS += --use-system-zlib
COMPONENT_BUILD_ARGS += --ssl
COMPONENT_BUILD_ARGS += --release
COMPONENT_BUILD_ARGS += --disable-ggdb
# Fixes gcc 7 build
COMPONENT_BUILD_ARGS += --disable-warnings-as-errors

COMPONENT_BUILD_TARGETS=	all

COMPONENT_INSTALL_ARGS = $(COMPONENT_BUILD_ARGS)

GOROOT=$(shell go env | grep GOROOT | awk -F= '{ print $$2 }' | tr -d '"')

$(BUILD_TOOLS):	$(BUILD_64)
	$(MKDIR) $(@D)/bin
	$(CP) -a $(SOURCE_DIR)/src/mongo/gotools/* $(@D) 
	cd $(@D)/src/github.com/mongodb/mongo-tools && GOROOT=$(GOROOT) GO111MODULE=auto /usr/bin/bash build.sh ssl
	$(TOUCH) $(@)

$(INSTALL_TOOLS): $(BUILD_TOOLS) $(INSTALL_64)
	$(CP) $(BUILD_DIR)/tools/src/github.com/mongodb/mongo-tools/bin/* $(PROTO_DIR)/$(MONGO_PREFIX)/bin
	$(TOUCH) $(@)

TEST_SUITES += core
TEST_SUITES += dbtest
TEST_SUITES += dur_jscore_passthrough
TEST_SUITES += jstestfuzz
TEST_SUITES += jstestfuzz_replication
TEST_SUITES += jstestfuzz_sharded
TEST_SUITES += replica_sets_jscore_passthrough
TEST_SUITES += unittests

# A bit of magic to replace spaces with commas
comma:= ,
empty:=
space:= $(empty) $(empty)

COMPONENT_TEST_CMD = $(PYTHON) buildscripts/resmoke.py \
			--continueOnFailure \
			--dbpathPrefix=/tmp/db \
			--suites=$(subst $(space),$(comma),$(TEST_SUITES))

COMPONENT_TEST_TARGETS =

COMPONENT_TEST_TRANSFORMS +=    '-e "s/\[resmoke\][ -+0-9T:\.\-]*//"' \
                                '-e "s/\s\s*[0-9][0-9]*\.[0-9][0-9]* seconds/ SEC seconds/"' \
                                '-n ' \
                                '-e "/Summary of all suites/,\\$$p"'

# Not strictly necessary
$(TEST_64):     $(INSTALL_64) $(INSTALL_TOOLS)

build:		$(BUILD_64) $(BUILD_TOOLS)

install:	$(INSTALL_64) $(INSTALL_TOOLS)


# Test requirements
REQUIRED_PACKAGES += library/python/pymongo-27
REQUIRED_PACKAGES += library/python/pyyaml

# Build dependencies
REQUIRED_PACKAGES += developer/build/scons
REQUIRED_PACKAGES += developer/golang

# Auto-generated dependencies via `gmake GMAKE=gmake REQUIRED_PACKAGES`
REQUIRED_PACKAGES += SUNWcs
REQUIRED_PACKAGES += library/security/openssl
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += $(GCC_RUNTIME_PKG)
REQUIRED_PACKAGES += $(GXX_RUNTIME_PKG)
REQUIRED_PACKAGES += system/library/boost
REQUIRED_PACKAGES += system/library/libpcap
REQUIRED_PACKAGES += system/library/math
