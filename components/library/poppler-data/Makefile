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
# Copyright 2014, Andrzej Szeszo
# Copyright 2019, Michal Nowak
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		poppler-data
COMPONENT_VERSION=	0.4.9
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH= \
	sha256:1f9c7e7de9ecd0db6ab287349e31bf815ca108a5a175cf906a90163bdbe32012
COMPONENT_ARCHIVE_URL= \
	http://poppler.freedesktop.org/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL=	http://poppler.freedesktop.org/
COMPONENT_FMRI=		library/libpoppler-data
COMPONENT_SUMMARY=	Poppler is a PDF rendering library based on the xpdf-3.0 code base (encoding data)
COMPONENT_LICENSE=	GPLv2
COMPONENT_LICENSE_FILE=	COPYING
COMPONENT_CLASSIFICATION=	Desktop (GNOME)/Libraries

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/cmake.mk
include $(WS_MAKE_RULES)/ips.mk

build:		$(BUILD_32)

install:	$(INSTALL_32)

test:		$(NO_TESTS)

# Auto-generated dependencies
