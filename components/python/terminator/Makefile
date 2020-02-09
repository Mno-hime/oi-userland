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
# Copyright (c) 2014 Alexander Pyhalov
# Copyright 2020, Michal Nowak
#

BUILD_BITS=		64
BUILD_STYLE=		setup.py

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		terminator
COMPONENT_VERSION=	1.91
COMPONENT_REVISION=	1
COMPONENT_PROJECT_URL=	http://www.tenshu.net/terminator/
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	\
    sha256:95f76e3c0253956d19ceab2f8da709a496f1b9cf9b1c5b8d3cd0b6da3cc7be69
COMPONENT_ARCHIVE_URL=	http://launchpad.net/terminator/gtk3/$(COMPONENT_VERSION)/+download/$(COMPONENT_ARCHIVE)

PYTHON_VERSIONS=	3.5

include $(WS_MAKE_RULES)/common.mk

PATH=$(PATH.gnu)

PYTHON_DATA=/usr

COMPONENT_POST_INSTALL_ACTION += \
        (cd $(PROTO_DIR)/usr/bin && \
	  $(MV) -f terminator terminator-$(PYTHON_VERSION) && \
	  $(MV) -f remotinator remotinator-$(PYTHON_VERSION) \
	) ;
COMPONENT_POST_INSTALL_ACTION += \
	$(GSED) -i '/\#! \?\/usr.*/d' $(PROTO_DIR)/usr/lib/python$(PYTHON_VERSION)/vendor-packages/terminatorlib/*.py

REQUIRED_PACKAGES += library/python/pycairo-35
# Auto-generated dependencies
REQUIRED_PACKAGES += library/python/psutil-35
REQUIRED_PACKAGES += library/python/pygobject-3-35
REQUIRED_PACKAGES += library/python/python-dbus-35
REQUIRED_PACKAGES += runtime/python-35
