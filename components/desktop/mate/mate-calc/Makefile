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
# Copyright 2016 Till Wegmueller
# Copyright 2019 Michal Nowak
#

BUILD_BITS=		64

include ../../../../make-rules/shared-macros.mk

COMPONENT_NAME=		mate-calc
COMPONENT_MJR_VERSION=	1.22
COMPONENT_MNR_VERSION=	2
COMPONENT_VERSION=	$(COMPONENT_MJR_VERSION).$(COMPONENT_MNR_VERSION)
COMPONENT_PROJECT_URL=	http://www.mate-desktop.org
COMPONENT_SUMMARY=	MATE Calculator App
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_HASH=	\
	sha256:efe6818d0a89b5456246412ac3af2c9fea8b6c6a32226cfd26c8b1e6a17e44ab
COMPONENT_ARCHIVE_URL=	http://pub.mate-desktop.org/sources/$(COMPONENT_NAME)/$(COMPONENT_MJR_VERSION)/$(COMPONENT_ARCHIVE)
COMPONENT_FMRI=		desktop/mate/$(COMPONENT_NAME)
COMPONENT_CLASSIFICATION=	Applications/Accessories
COMPONENT_LICENSE=	GPLv2
COMPONENT_LICENSE_FILE=	COPYING

TEST_TARGET=		$(NO_TESTS)

include $(WS_MAKE_RULES)/common.mk

PATH=$(PATH.gnu)

CONFIGURE_OPTIONS+=	--sysconfdir=/etc
CONFIGURE_OPTIONS+=	--libexecdir=/usr/lib/mate
CONFIGURE_OPTIONS+=	--disable-static

# Build dependencies
REQUIRED_PACKAGES += library/desktop/mate/mate-common
# Auto-generated dependencies
REQUIRED_PACKAGES += library/desktop/atk
REQUIRED_PACKAGES += library/desktop/gtk3
REQUIRED_PACKAGES += library/desktop/pango
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/libxml2
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
