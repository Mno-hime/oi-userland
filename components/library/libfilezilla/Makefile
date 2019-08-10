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

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		libfilezilla
COMPONENT_VERSION=	0.18.0
COMPONENT_SUMMARY=	C++ library for filezilla
COMPONENT_PROJECT_URL=	https://lib.filezilla-project.org/
COMPONENT_FMRI=		library/filezilla
COMPONENT_CLASSIFICATION=	System/Libraries
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.bz2
COMPONENT_ARCHIVE_URL=	https://download.filezilla-project.org/libfilezilla/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH=	sha256:577a663b5dcf7f44e76a4208f11d6e7c4325c8f45fe15be8588de86eb75f9f3c
COMPONENT_LICENSE=	GPLv2.0+
COMPONENT_LICENSE_FILE=	COPYING

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

# Requires GNU xgettext
PATH=$(PATH.gnu)

GCC_VERSION =	7

# Force use of gnutls-3 pkgconfig during 2.x->3.x transition
GNUTLS_PKG_CONFIG_PATH_32 = /usr/lib/pkgconfig/gnutls-3
GNUTLS_PKG_CONFIG_PATH_64 = /usr/lib/$(MACH64)/pkgconfig/gnutls-3
PKG_CONFIG_PATH = $(GNUTLS_PKG_CONFIG_PATH_$(BITS)):$(PKG_CONFIG_PATH.$(BITS))

LD_OPTIONS.32 += -L/usr/lib/gnutls-3 -R/usr/lib/gnutls-3
LD_OPTIONS.64 += -L/usr/lib/$(MACH64)/gnutls-3 -R/usr/lib/$(MACH64)/gnutls-3
LD_OPTIONS += $(LD_OPTIONS.$(BITS))

# include wcsnrtombs(3c)
CXXFLAGS += -I/usr/include/gmp $(CPP_XPG7MODE)

CONFIGURE_OPTIONS += --disable-static

build:		$(BUILD_64)

install:	$(INSTALL_64)

# ld.so.1: test: fatal: libgnutls.so.30: open failed: No such file or directory
test:		$(TEST_64)

REQUIRED_PACKAGES += system/library/gcc-7-runtime
REQUIRED_PACKAGES += system/library/g++-7-runtime
# Auto-generated dependencies
REQUIRED_PACKAGES += library/gnutls-3
REQUIRED_PACKAGES += library/nettle
REQUIRED_PACKAGES += system/library
