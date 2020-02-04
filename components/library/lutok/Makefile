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

COMPONENT_NAME=		lutok
COMPONENT_VERSION=	0.4
COMPONENT_SUMMARY=	A lightweight C++ API library for Lua
COMPONENT_PROJECT_URL=	https://github.com/jmmv/lutok
COMPONENT_FMRI=		library/lutok
COMPONENT_CLASSIFICATION= System/Libraries
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_URL=	https://github.com/jmmv/lutok/releases/download/$(COMPONENT_SRC)/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH=	sha256:2cec51efa0c8d65ace8b21eaa08384b77abc5087b46e785f78de1c21fb754cd5
COMPONENT_LICENSE=	BSD-3-Clause
COMPONENT_LICENSE_FILE=	COPYING

include $(WS_MAKE_RULES)/common.mk

CONFIGURE_OPTIONS += --disable-static
CONFIGURE_OPTIONS += --without-doxygen

REQUIRED_PACKAGES += developer/atf
# Auto-generated dependencies
REQUIRED_PACKAGES += $(GCC_RUNTIME_PKG)
REQUIRED_PACKAGES += $(GXX_RUNTIME_PKG)
REQUIRED_PACKAGES += runtime/lua
REQUIRED_PACKAGES += system/library
