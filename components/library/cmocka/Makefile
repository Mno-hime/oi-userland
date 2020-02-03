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
# Copyright 2020, Michal Nowak
#

BUILD_BITS=		32_and_64
BUILD_STYLE=		cmake

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		cmocka
COMPONENT_VERSION_MAJOR=1.1
COMPONENT_VERSION_MINOR=5
COMPONENT_VERSION=	$(COMPONENT_VERSION_MAJOR).$(COMPONENT_VERSION_MINOR)
COMPONENT_SUMMARY=	an elegant unit testing framework for C with support for mock objects
COMPONENT_PROJECT_URL=	https://cmocka.org
COMPONENT_FMRI=		library/cmocka
COMPONENT_CLASSIFICATION=Development/C
COMPONENT_SRC=          $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=      $(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_URL=	https://cmocka.org/files/$(COMPONENT_VERSION_MAJOR)/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH=	sha256:f0ccd8242d55e2fd74b16ba518359151f6f8383ff8aef4976e48393f77bba8b6
COMPONENT_LICENSE=	Apache v2.0
COMPONENT_LICENSE_FILE=	COPYING

include $(WS_MAKE_RULES)/common.mk

CMAKE_OPTIONS += -DCMAKE_SKIP_RPATH=OFF
CMAKE_OPTIONS += -DWITH_STATIC_LIB=ON
CMAKE_OPTIONS += -DWITH_CMOCKERY_SUPPORT=ON
CMAKE_OPTIONS += -DUNIT_TESTING=ON
CMAKE_OPTIONS += -DWITH_STACK_PROTECTOR=OFF
CMAKE_OPTIONS += -DWITH_STACK_PROTECTOR_STRONG=OFF

COMPONENT_TEST_TRANSFORMS += \
	'-e "s/   .* sec//" '

# Auto-generated dependencies
REQUIRED_PACKAGES += system/library
