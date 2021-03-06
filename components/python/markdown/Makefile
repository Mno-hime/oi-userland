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
# Copyright 2016, Aurelien Larcher.
# Copyright 2019, Michal Nowak
#
include ../../../make-rules/shared-macros.mk


COMPONENT_NAME=		Markdown
COMPONENT_VERSION=	3.1
COMPONENT_SUMMARY=	'Python implementation of Markdown'
COMPONENT_FMRI=		library/python/markdown
COMPONENT_PROJECT_URL=	https://python-markdown.github.io
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC_NAME)-$(COMPONENT_VERSION).tar.gz
COMPONENT_ARCHIVE_HASH=	\
	sha256:fc4a6f69a656b8d858d7503bda633f4dd63c2d70cf80abdc6eafa64c4ae8c250
COMPONENT_ARCHIVE_URL=	$(call pypi_url)
COMPONENT_LICENSE=	BSD
COMPONENT_LICENSE_FILE=	LICENSE.md

PYTHON_VERSIONS=	2.7 3.4 3.5

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/setup.py.mk
include $(WS_MAKE_RULES)/ips.mk

build:		$(BUILD_NO_ARCH)

install:	$(INSTALL_NO_ARCH)

test:		$(NO_TESTS)

# Auto-generated dependencies
REQUIRED_PACKAGES += library/python/setuptools-35
REQUIRED_PACKAGES += runtime/python-27
REQUIRED_PACKAGES += runtime/python-34
REQUIRED_PACKAGES += runtime/python-35
