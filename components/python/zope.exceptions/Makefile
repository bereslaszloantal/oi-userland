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
#   $WS_TOOLS/python-integrate-project zope.exceptions
#

BUILD_STYLE = setup.py

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME =		zope.exceptions
COMPONENT_VERSION =		4.6
COMPONENT_SUMMARY =		zope.exceptions - Zope Exceptions
COMPONENT_PROJECT_URL =		https://github.com/zopefoundation/zope.exceptions
COMPONENT_ARCHIVE_URL =		\
	https://files.pythonhosted.org/packages/07/d7/01ae11fb9b4422f8c05fca69e9cc4be57282f6a93becabf8002e82ec0c24/zope.exceptions-4.6.tar.gz
COMPONENT_ARCHIVE_HASH =	\
	sha256:619d24a4c65bed97b3dd0515e732e82b69f155d42cc94955d1be8c28288683cd
COMPONENT_LICENSE =		ZPL-2.1
COMPONENT_LICENSE_FILE =	LICENSE.txt

#
# Following dependency loops were detected (where 'A --> B' means 'A needs B to
# run tests', and 'A ==> B' means 'A needs B for build and/or run'):
#
# zope.exceptions --> zope.testrunner ==> zope.exceptions
#
# To break loops we need to allow this project to integrate without testing in
# a case the required projects are not available yet (bootstrap).
#
PYTHON_TEST_BOOTSTRAP = yes

include $(WS_MAKE_RULES)/common.mk

# Auto-generated dependencies
PYTHON_REQUIRED_PACKAGES += library/python/setuptools
PYTHON_REQUIRED_PACKAGES += library/python/zope-interface
PYTHON_REQUIRED_PACKAGES += runtime/python
TEST_REQUIRED_PACKAGES.python += library/python/repoze-sphinx-autointerface
TEST_REQUIRED_PACKAGES.python += library/python/sphinx
TEST_REQUIRED_PACKAGES.python += library/python/zope-testrunner
