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
# Copyright 2013-2016 Alexander Pyhalov
#
BUILD_BITS=	32_and_64
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		pygobject
COMPONENT_VERSION=	2.28.6
COMPONENT_REVISION=	7
COMPONENT_PROJECT_URL=	https://www.gnome.org
COMPONENT_SUMMARY=	Python bindings for GObject
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.bz2
COMPONENT_ARCHIVE_HASH= sha256:d464699db159f72e41a8d629ab44b7fef6cf8d746e51f576b6fbc4ce317239d3
COMPONENT_ARCHIVE_URL=	https://download.gnome.org/sources/$(COMPONENT_NAME)/2.28/$(COMPONENT_ARCHIVE)
COMPONENT_FMRI=		library/python/$(COMPONENT_NAME)
COMPONENT_CLASSIFICATION=	Development/Python
COMPONENT_LICENSE=	LGPL v2.1

PYTHON_VERSIONS= 2.7

VARIANT_PYTHON27 = $(BUILD_DIR)/python-27

VARIANTS = $(VARIANT_PYTHON27)

BUILD_32 = $(VARIANTS:%=%/$(MACH32)/.built)
BUILD_64 = $(VARIANTS:%=%/$(MACH64)/.built)

INSTALL_32 = $(VARIANTS:%=%/$(MACH32)/.installed)
INSTALL_64 = $(VARIANTS:%=%/$(MACH64)/.installed)

$(VARIANT_PYTHON27)/$(MACH64)/.configured: BITS=64
$(VARIANT_PYTHON27)/$(MACH64)/.configured: PYTHON=$(PYTHON.2.7.64)
$(VARIANT_PYTHON27)/$(MACH64)/.configured: am_cv_python_pyexecdir=$(PYTHON.2.7.VENDOR_PACKAGES.64)
$(VARIANT_PYTHON27)/$(MACH64)/.configured: am_cv_python_pythondir=$(PYTHON.2.7.VENDOR_PACKAGES.64)

$(VARIANT_PYTHON27)/$(MACH32)/.configured: PYTHON=$(PYTHON.2.7.32)
$(VARIANT_PYTHON27)/$(MACH32)/.configured: am_cv_python_pyexecdir=$(PYTHON.2.7.VENDOR_PACKAGES.32)
$(VARIANT_PYTHON27)/$(MACH32)/.configured: am_cv_python_pythondir=$(PYTHON.2.7.VENDOR_PACKAGES.32)

TEST_TARGET=	$(NO_TESTS)
include $(WS_MAKE_RULES)/common.mk

PATH=$(PATH.gnu)

COMPONENT_PREP_ACTION= (cd $(@D) && autoreconf -f -i)

#CFLAGS += $(gcc_C99_ENABLE)

CONFIGURE_OPTIONS+=	--sysconfdir=/etc
CONFIGURE_OPTIONS+=	--without-ffi

# Disable introspection modules in this package since we ship the modern ones
# in the ../pygobject-3 packages instead, and they'd clash if we didn't disable.
CONFIGURE_OPTIONS += --disable-introspection

CONFIGURE_ENV+=		PYTHON=$(PYTHON)

CONFIGURE_ENV+=         PYTHON=$(PYTHON)
CONFIGURE_ENV+=         am_cv_python_pythondir="$(am_cv_python_pythondir)"
CONFIGURE_ENV+=         am_cv_python_pyexecdir="$(am_cv_python_pyexecdir)"

REQUIRED_PACKAGES += SUNWcs
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/desktop/gobject/gobject-introspection
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += runtime/python-27
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += developer/documentation-tool/gtk-doc
