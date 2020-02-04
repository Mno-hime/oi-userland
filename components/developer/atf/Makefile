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

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		atf
COMPONENT_VERSION=	0.21
COMPONENT_SUMMARY=	Automated Testing Framework
COMPONENT_PROJECT_URL=	https://github.com/jmmv/atf
COMPONENT_FMRI=		developer/atf
COMPONENT_CLASSIFICATION=Development/C
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_URL=	https://github.com/jmmv/atf/releases/download/$(COMPONENT_SRC)/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH=	sha256:92bc64180135eea8fe84c91c9f894e678767764f6dbc8482021d4dde09857505
COMPONENT_LICENSE=	BSD
COMPONENT_LICENSE_FILE=	COPYING

include $(WS_MAKE_RULES)/common.mk

#sed -i 's|^hardcode_libdir_flag_spec=.*|hardcode_libdir_flag_spec=""|g' libtool
#sed -i 's|^runpath_var=LD_RUN_PATH|runpath_var=DIE_RPATH_DIE|g' libtool

CONFIGURE_OPTIONS += --disable-static

CONFIGURE_ENV += INSTALL="$(INSTALL) -p"

# Auto-generated dependencies
REQUIRED_PACKAGES += $(GCC_RUNTIME_PKG)
REQUIRED_PACKAGES += $(GXX_RUNTIME_PKG)
REQUIRED_PACKAGES += system/library
