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
# Copyright (c) 2017 - 2019 Andreas Wacknitz
#

BUILD_BITS=			32_and_64
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		libsass
COMPONENT_VERSION=	3.6.3
COMPONENT_PROJECT_URL=	http://libsass.org
COMPONENT_SUMMARY=	LibSass is a C/C++ port of the Sass engine
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_VERSION).tar.gz
COMPONENT_ARCHIVE_HASH=	\
  sha256:dadb470bb9141e91b437119d367654427180ed2b3d04b8000eab5b0ca47cd5bb
COMPONENT_ARCHIVE_URL=	https://github.com/sass/libsass/archive/$(COMPONENT_ARCHIVE)
COMPONENT_FMRI =	library/libsass
COMPONENT_LICENSE=	MIT
COMPONENT_LICENSE_FILE=	LICENSE
COMPONENT_CLASSIFICATION =	System/Libraries

TESTS=	$(NO_TESTS)
include $(WS_MAKE_RULES)/common.mk

PATH=$(PATH.gnu)

COMPONENT_PREP_ACTION = \
			( cd $(@D) && $(CONFIG_SHELL) autoreconf --force --install )

CONFIGURE_OPTIONS += --disable-static
CONFIGURE_OPTIONS += --enable-shared

# Auto-generated dependencies
REQUIRED_PACKAGES += $(GCC_RUNTIME_PKG)
REQUIRED_PACKAGES += $(GXX_RUNTIME_PKG)
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
