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
# This file was automatically generated using the following command:
#   $WS_TOOLS/python-integrate-project pycairo
#

BUILD_STYLE = pyproject
# Force setup.py build style - see https://github.com/pygobject/pycairo/issues/312
BUILD_STYLE = setup.py

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME =		pycairo
HUMAN_VERSION =			1.23.0
COMPONENT_SUMMARY =		pycairo - Python interface for cairo
COMPONENT_PROJECT_URL =		https://pycairo.readthedocs.io
COMPONENT_ARCHIVE_URL =		\
	https://files.pythonhosted.org/packages/69/ca/9e9fa2e8be0876a9bbf046a1be7ee33e61d4fdfbd1fd25c76c1bdfddf8c4/pycairo-1.23.0.tar.gz
COMPONENT_ARCHIVE_HASH =	\
	sha256:9b61ac818723adc04367301317eb2e814a83522f07bbd1f409af0dada463c44c
COMPONENT_LICENSE =		LGPL-2.1-only OR MPL-1.1

TEST_STYLE = pytest

# We cannot obsolete pycairo-27 yet because it is needed by pygtk2-27 and
# pygtk2-27 is needed by gimp.
PYTHON_VERSIONS_OBSOLETING := $(filter-out 2.7, $(PYTHON_VERSIONS_OBSOLETING))

# Install common files to /usr
PYTHON_DATA = $(USRDIR)

include $(WS_MAKE_RULES)/common.mk

# The pkgconfig file should go to proper place
COMPONENT_INSTALL_ARGS += install_pkgconfig --pkgconfigdir=$(PKG_CONFIG_PATH.$(BITS))

# Rename headers and pkgconfig files to contain version number
COMPONENT_POST_INSTALL_ACTION += \
	for f in $(PROTOUSRINCDIR)/pycairo/* $(PROTO_DIR)$(PKG_CONFIG_PATH.$(BITS))/* ; do \
		[[ -f $$f ]] || continue ; \
		for v in $(PYTHON_VERSIONS) ; do \
			[[ "$$f" == "$${f%%$$v}" ]] || continue 2 ; \
		done ; \
		$(MV) $$f $$f-$(PYTHON_VERSION) ; \
	done ;

# Testing fails with the checkdocs plugin installed
PYTEST_ADDOPTS += -p no:checkdocs

# Tests are run from build directory which contains cloned copy of sdist.  We
# try to ask Python to find tested modules in the proto area (the PYTHONPATH is
# set accordingly), but Python (< 3.11) always adds the current directory to
# sys.path and there is no known (simple) way how to avoid that.  Except -I,
# but that would cause Python to ignore PYTHONPATH too so we would not have
# access to the proto area either.  The -P option together with PYTHONSAFEPATH
# environment variable were added to Python 3.11 only so we cannot use them yet
# for all Python versions we support.
#
# Since sdist for this project contains the main module in the top-level
# directory we cannot force Python to skip it.  But, unfortunately, this module
# does not contain built dynamic libraries, so Python cannot find them while
# testing.
#
# To workaround this we rename the main module in the build directory during
# testing so Python will need to defer to PYTHONPATH.
COMPONENT_PRE_TEST_ACTION += \
	$(MV) $(@D)/cairo $(@D)/cairo-RENAMED ;
COMPONENT_POST_TEST_ACTION += \
	$(MV) $(@D)/cairo-RENAMED $(@D)/cairo ;

# Replace Python version in header and pkgconfig file names
GENERATE_EXTRA_CMD += | \
	$(GSED) -e 's/\(py3cairo\.[hpc]*-\)3\.[0-9]*$$/\1$$(PYVER)/' | uniq

# Auto-generated dependencies
PYTHON_REQUIRED_PACKAGES += runtime/python
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += system/library
