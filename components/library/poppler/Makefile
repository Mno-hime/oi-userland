#! /usr/bin/sh
#
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
# Copyright 2014 Andrzej Szeszo.  All rights reserved.
# Copyright (c) 2016, 2019, Oracle and/or its affiliates. All rights reserved.
# Copyright 2019 Michal Nowak
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		poppler
COMPONENT_VERSION=	0.79.0
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_HASH= \
	sha256:f985a4608fe592d2546d9d37d4182e502ff6b4c42f8db4be0a021a1c369528c8
COMPONENT_ARCHIVE_URL= \
	http://poppler.freedesktop.org/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL=	http://poppler.freedesktop.org/
COMPONENT_FMRI=		library/libpoppler
COMPONENT_SUMMARY=	Poppler is a PDF rendering library based on the xpdf-3.0 code base
COMPONENT_LICENSE=	GPLv2
COMPONENT_LICENSE_FILE=	COPYING
COMPONENT_CLASSIFICATION=	Desktop (GNOME)/Libraries

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/cmake.mk
include $(WS_MAKE_RULES)/ips.mk

# Uses strcpy_s, etc. c11 functions.
CFLAGS += -std=c11
CXXFLAGS += -std=c++11 -D__STDC_WANT_LIB_EXT1__=1
# Set CC environment variable to the compiler path, it is required by g-ir-scanner.
CMAKE_ENV.32 += CC="$(CC) $(CC_BITS)"
CMAKE_ENV.64 += CC="$(CC) $(CC_BITS)"

CMAKE_OPTIONS += -DCMAKE_C_COMPILER=$(CC)
CMAKE_OPTIONS += -DCMAKE_CXX_COMPILER=$(CXX)
CMAKE_OPTIONS += -DCMAKE_C_FLAGS=$(CFLAGS)
CMAKE_OPTIONS += -DCMAKE_BUILD_TYPE="Release"

# Reduce build time dependencies since we don't ship this
# or can't run it as an automated test.
CMAKE_OPTIONS += -DBUILD_CPP_TESTS=OFF
CMAKE_OPTIONS += -DBUILD_GTK_TESTS=OFF
CMAKE_OPTIONS += -DBUILD_QT5_TESTS=OFF

# Build shared libpoppler libraries.
CMAKE_OPTIONS += -DBUILD_SHARED_LIBS=ON

# Not necessary for the userland consolidation.
CMAKE_OPTIONS += -DENABLE_QT5=OFF
CMAKE_OPTIONS += -DENABLE_GTK_DOC=OFF

# Required by other components.
CMAKE_OPTIONS += -DWITH_Cairo=ON
CMAKE_OPTIONS += -DWITH_Iconv=ON
CMAKE_OPTIONS += -DWITH_GLIB=ON
CMAKE_OPTIONS += -DWITH_GTK=ON
CMAKE_OPTIONS += -DWITH_NSS3=ON
CMAKE_OPTIONS += -DWITH_JPEG=ON
CMAKE_OPTIONS += -DWITH_PNG=ON
CMAKE_OPTIONS += -DWITH_TIFF=ON
CMAKE_OPTIONS += -DWITH_ZLIB=ON
CMAKE_OPTIONS += -DWITH_GObjectIntrospection=ON
CMAKE_OPTIONS += -DENABLE_CPP=ON
CMAKE_OPTIONS += -DENABLE_SPLASH=ON
CMAKE_OPTIONS += -DENABLE_LIBCURL=ON
CMAKE_OPTIONS += -DENABLE_UNSTABLE_API_ABI_HEADERS=ON
CMAKE_OPTIONS += -DENABLE_CMS=lcms2
CMAKE_OPTIONS += -DENABLE_LIBOPENJPEG=openjpeg2
CMAKE_OPTIONS += -DENABLE_DCTDECODER=libjpeg
CMAKE_OPTIONS += -DFONT_CONFIGURATION=fontconfig

# build with the distribution preferred libjpeg implementation
CFLAGS   += $(JPEG_CPPFLAGS) $(JPEG_CFLAGS)
CXXFLAGS += $(JPEG_CPPFLAGS) $(JPEG_CXXFLAGS)
LDFLAGS  += $(JPEG_LDFLAGS)
#LDFLAGS.32 += -L/usr/lib -R/usr/lib
LDFLAGS.64 += -L/usr/lib/$(MACH64) -R/usr/lib/$(MACH64)
LDFLAGS += $(LDFLAGS.$(BITS))

build:		$(BUILD_32_and_64)

install:	$(INSTALL_32_and_64)

#test:		$(NO_TESTS)
test:		$(TEST_32_and_64)

REQUIRED_PACKAGES += image/library/libjpeg8-turbo
REQUIRED_PACKAGES += image/library/libpng16
REQUIRED_PACKAGES += image/library/libtiff
REQUIRED_PACKAGES += image/library/openjpeg
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/lcms2
REQUIRED_PACKAGES += library/nspr
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/fontconfig
REQUIRED_PACKAGES += system/library/freetype-2
REQUIRED_PACKAGES += $(GXX_RUNTIME_PKG)
REQUIRED_PACKAGES += $(GCC_RUNTIME_PKG)
REQUIRED_PACKAGES += system/library/math
REQUIRED_PACKAGES += system/library/mozilla-nss
