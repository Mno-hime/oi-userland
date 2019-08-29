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
# Copyright 2019 Michal Nowak
#

BUILD_BITS=		64

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		simple-scan
COMPONENT_VERSION_MAJOR=3.24
COMPONENT_VERSION_MINOR=1
COMPONENT_VERSION=	$(COMPONENT_VERSION_MAJOR).$(COMPONENT_VERSION_MINOR)
COMPONENT_SUMMARY=	Simple Scanning Utility
COMPONENT_PROJECT_URL=	https://launchpad.net/simple-scan
COMPONENT_FMRI=		image/scanner/simple-scan
COMPONENT_CLASSIFICATION=	Applications/System Utilities
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_URL=	https://download.gnome.org/sources/simple-scan/$(COMPONENT_VERSION_MAJOR)/simple-scan-3.24.1.tar.xz
COMPONENT_ARCHIVE_HASH=	sha256:5eae832b14664183d55aa599801cf32f19ff2174dfba4e3d7e4eb4d55810efb3
COMPONENT_LICENSE=	GPLv3
COMPONENT_LICENSE_FILE=	COPYING

include $(WS_MAKE_RULES)/common.mk

#CONFIGURE_OPTIONS +=	HAVE_COLORD=0

CONFIGURE_OPTIONS +=	--enable-colord=no
CONFIGURE_OPTIONS +=	--enable-packagekit=no

