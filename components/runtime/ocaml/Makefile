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
# Copyright (c) 2013, 2016, Oracle and/or its affiliates. All rights reserved.
# Copyright 2017 Andreas Grueninger, Grueninger GmbH, (grueni). All rights reserved.
# Copyright 2023 Friedrich Kink. All rights reserved.
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=			ocaml
COMPONENT_FMRI=			runtime/ocaml
COMPONENT_VERSION_MAJOR=	5.0
COMPONENT_VERSION=		$(COMPONENT_VERSION_MAJOR).0
IPS_COMPONENT_VERSION=		$(COMPONENT_VERSION)
COMPONENT_PROJECT_URL=		https://ocaml.org
COMPONENT_SRC=			$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=		$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_SRC=		$(COMPONENT_VERSION).tar.gz
COMPONENT_ARCHIVE_HASH=		sha256:72fa3d0ba19b82fcb9e6c62e0090b9d22e5905c4be0f94faf56904a9377a9e5b
COMPONENT_ARCHIVE_URL=		https://github.com/$(COMPONENT_NAME)/$(COMPONENT_NAME)/archive/$(COMPONENT_ARCHIVE_SRC)
COMPONENT_SUMMARY=		Objective Caml compiler and programming environment
COMPONENT_LICENSE=		QPLv1, GPLv2
COMPONENT_LICENSE_FILE=		$(COMPONENT_NAME).license
COMPONENT_CLASSIFICATION=	Development/System
COMPONENT_DESCRIPTION= Objective Caml is a high-level, strongly-typed, functional and \
object-oriented programming language from the ML family of languages. This package comprises \
two batch compilers (a fast bytecode compiler and an optimizing native-code compiler), \
an interactive toplevel system, parsing tools (Lex,Yacc,Camlp4), a replay debugger, \
a documentation generator, and a comprehensive library.

# Documentation sources
#
COMPONENT_ARCHIVE_1=		ocaml-$(COMPONENT_VERSION_MAJOR)-refman-html.tar.gz
COMPONENT_ARCHIVE_HASH_1=	sha256:ea5cedafd31ee7ce06c6a19c5edc6ff0ab36bec0d60bd374be201e8ae94434a1
COMPONENT_ARCHIVE_URL_1=	https://caml.inria.fr/distrib/ocaml-$(COMPONENT_VERSION_MAJOR)/$(COMPONENT_ARCHIVE_1)

COMPONENT_ARCHIVE_2=		ocaml-$(COMPONENT_VERSION_MAJOR)-refman.pdf
COMPONENT_ARCHIVE_HASH_2=	sha256:5bdda0163736cabc4b2a0bbc046c1e031e5f5a2a1b3290d9427e966ad85b1d34
COMPONENT_ARCHIVE_URL_2=	https://caml.inria.fr/distrib/ocaml-$(COMPONENT_VERSION_MAJOR)/$(COMPONENT_ARCHIVE_2)

COMPONENT_ARCHIVE_3=		ocaml-$(COMPONENT_VERSION_MAJOR)-refman.info.tar.gz
COMPONENT_ARCHIVE_HASH_3=	sha256:07270a92d5db9418e1e9bdb81d6b435d5011f4b337972556d6dca43a6305c81d
COMPONENT_ARCHIVE_URL_3=	https://caml.inria.fr/distrib/ocaml-$(COMPONENT_VERSION_MAJOR)/$(COMPONENT_ARCHIVE_3)


include $(WS_MAKE_RULES)/common.mk

COMPONENT_BUILD_ARGS += -j1

# Set up some environment variables to make things look nicer.
# We make an 64 build and use /usr/bin/ for the commands
UL_OCAML_PDFDOC     = $(USERLAND_ARCHIVES)$(COMPONENT_ARCHIVE_2)

CONFIGURE_OPTIONS  = --bindir=$(CONFIGURE_BINDIR.$(BITS))
CONFIGURE_OPTIONS += --libdir=$(CONFIGURE_LIBDIR.$(BITS))/$(COMPONENT_NAME)
CONFIGURE_OPTIONS += --mandir=$(CONFIGURE_MANDIR)
CONFIGURE_OPTIONS += --datarootdir=$(CONFIGURE_PREFIX)/share/$(COMPONENT_NAME)
CONFIGURE_OPTIONS += --disable-debug-runtime
CONFIGURE_OPTIONS += --without-gnu-ld
CONFIGURE_OPTIONS += --enable-installing-bytecode-programs
CONFIGURE_OPTIONS += --enable-flambda
# otherwise no tests possible
CONFIGURE_OPTIONS += --enable-ocamltest

COMPONENT_PRE_CONFIGURE_ACTION = \
  ($(CLONEY) $(SOURCE_DIR) $(@D))

COMPONENT_BUILD_TARGETS = world opt opt.opt

COMPONENT_POST_BUILD_ACTION = (cd $(@D); \
   $(GTAR) xf $(USERLAND_ARCHIVES)$(COMPONENT_ARCHIVE_1); \
   $(GTAR) xf $(USERLAND_ARCHIVES)$(COMPONENT_ARCHIVE_3); )

# This action moves additional files we want to install into the proto area.
# I prefer using "cp -R" for copying the documentation tarball and example
# contents since it will make it easier to see new files need to be packaged
# when Ocaml is updated.
#
COMPONENT_POST_INSTALL_ACTION = ( \
                cd $(@D) &&\
                $(MKDIR) $(PROTOUSRSHAREDIR)/info &&\
		$(MKDIR) $(PROTOUSRSHAREDOCDIR)/$(COMPONENT_NAME) &&\
                $(CP) $(@D)/infoman/ocaml*.gz $(PROTOUSRSHAREDIR)/info &&\
                $(CP) $(UL_OCAML_PDFDOC) $(PROTOUSRSHAREDOCDIR)/$(COMPONENT_NAME)/refman.pdf &&\
                $(CP) -R $(@D)/htmlman $(PROTOUSRSHAREDOCDIR)/$(COMPONENT_NAME)) 

# target all uses the new ocamltests, legacy uses the Makefile based tests.
# All tests succeed but the parsing of the ocamltest results is wrong and 
# leads to erroneously failing tests.
# Only native tests are concerned.
COMPONENT_TEST_TARGETS = all
#COMPONENT_TEST_TARGETS = legacy
COMPONENT_TEST_ARGS += SHELL=$(SHELL) 
COMPONENT_TEST_DIR =  $(@D)/testsuite
COMPONENT_TEST_TRANSFORMER = $(NAWK)
COMPONENT_TEST_TRANSFORMS  = "'/tests passed|tests skipped|tests failed|unexpected errors|tests considered/'"

# ASLR should be enabled when 64-bit support is enabled
ASLR_MODE = $(ASLR_ENABLE)

# Auto-generated dependencies
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
