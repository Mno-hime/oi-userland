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

COMPONENT_NAME=		libgusb
COMPONENT_VERSION=	0_2_11
IPS_COMPONENT_VERSION=	0.2.11
COMPONENT_SUMMARY=	A GObject wrapper for libusb-1
COMPONENT_PROJECT_URL=	https://github.com/hughsie/libgusb/
COMPONENT_FMRI=		library/libgusb
COMPONENT_CLASSIFICATION=	Development/C
COMPONENT_SRC=		$(COMPONENT_NAME)-gusb_$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	gusb_$(COMPONENT_VERSION).tar.gz
COMPONENT_ARCHIVE_URL=	https://github.com/hughsie/libgusb/archive/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH=	sha256:090eb605e75f8a5b0b3df7ff29d96dd51730850ac89417378d4a8d39fab13702
COMPONENT_LICENSE=	LGPLv2
COMPONENT_LICENSE_FILE=	COPYING

include $(WS_MAKE_RULES)/common.mk

CONFIGURE_OPTIONS +=	--disable-static

COMPONENT_PRE_CONFIGURE_ACTION +=	cd $(SOURCE_DIR) && gtkdocize && autoreconf --force --install --verbose ;
COMPONENT_PRE_CONFIGURE_ACTION +=	$(CLONEY) $(SOURCE_DIR) $(@D) ;

unexport SHELLOPTS

# Auto-generated dependencies
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/libusb-1
REQUIRED_PACKAGES += system/library
