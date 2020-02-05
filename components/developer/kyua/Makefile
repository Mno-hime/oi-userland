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

BUILD_BITS=		64

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		kyua
COMPONENT_VERSION=	0.13
COMPONENT_SUMMARY=	Testing framework for infrastructure software
COMPONENT_PROJECT_URL=	https://github.com/jmmv/kyua
COMPONENT_FMRI=		developer/kyua
COMPONENT_CLASSIFICATION=Development/C
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_URL=	https://github.com/jmmv/kyua/releases/download/$(COMPONENT_SRC)/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH=	sha256:db6e5d341d5cf7e49e50aa361243e19087a00ba33742b0855d2685c0b8e721d6
COMPONENT_LICENSE=	BSD 3-Clause
COMPONENT_LICENSE_FILE=	LICENSE

include $(WS_MAKE_RULES)/common.mk

CXXFLAGS += -fpermissive

CONFIGURE_OPTIONS += --with-doxygen=no
CONFIGURE_OPTIONS += --with-atf=yes

REQUIRED_PACKAGES += developer/atf
# Auto-generated dependencies
REQUIRED_PACKAGES += $(GCC_RUNTIME_PKG)
REQUIRED_PACKAGES += $(GXX_RUNTIME_PKG)
REQUIRED_PACKAGES += database/sqlite-3
REQUIRED_PACKAGES += library/lutok
REQUIRED_PACKAGES += system/library
