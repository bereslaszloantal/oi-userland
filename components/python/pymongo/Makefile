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
#   $WS_TOOLS/python-integrate-project pymongo
#

BUILD_STYLE = setup.py

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME =		pymongo
HUMAN_VERSION =			4.3.3
COMPONENT_SUMMARY =		pymongo - Python driver for MongoDB <http://www.mongodb.org>
COMPONENT_PROJECT_URL =		http://github.com/mongodb/mongo-python-driver
COMPONENT_ARCHIVE_URL =		\
	https://files.pythonhosted.org/packages/9a/31/482f7401e7bbbeb66ab6b4ac263e2b50435f4329cce1e72378972d48f6b5/pymongo-4.3.3.tar.gz
COMPONENT_ARCHIVE_HASH =	\
	sha256:34e95ffb0a68bffbc3b437f2d1f25fc916fef3df5cdeed0992da5f42fae9b807
COMPONENT_LICENSE =		Apache-2.0
COMPONENT_LICENSE_FILE =	LICENSE

TEST_STYLE = pytest

#
# Following dependency loops were detected (where 'A --> B' means 'A needs B to
# run tests', and 'A ==> B' means 'A needs B for build and/or run'):
#
# pymongo --> mockupdb ==> pymongo
#
# To break loops we need to allow this project to integrate without testing in
# a case the required projects are not available yet (bootstrap).
#
PYTHON_TEST_BOOTSTRAP = yes

include $(WS_MAKE_RULES)/common.mk

# Auto-generated dependencies
PYTHON_REQUIRED_PACKAGES += library/python/dnspython
PYTHON_REQUIRED_PACKAGES += runtime/python
REQUIRED_PACKAGES += system/library
