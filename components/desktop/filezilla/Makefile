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

COMPONENT_NAME=		filezilla
COMPONENT_VERSION=	3.44.1
COMPONENT_SUMMARY=	A GUI FTP and SFTP Client
COMPONENT_PROJECT_URL=	https://filezilla-project.org
COMPONENT_FMRI=		network/ftp/filezilla
COMPONENT_CLASSIFICATION=	Applications/Internet
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	FileZilla_$(COMPONENT_VERSION)_src.tar.bz2
COMPONENT_ARCHIVE_URL=	https://download.filezilla-project.org/client/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH=	sha256:c18e64106e80100f77a218f87e72931bdf0e244bddeb628e4e0a50166b934c8e
COMPONENT_LICENSE=	GPLv2.0+

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

GCC_VERSION=	7

CXXFLAGS += -I/usr/include/idn

# Force use of gnutls-3 pkgconfig during 2.x->3.x transition
GNUTLS_PKG_CONFIG_PATH_32 = /usr/lib/pkgconfig/gnutls-3
GNUTLS_PKG_CONFIG_PATH_64 = /usr/lib/$(MACH64)/pkgconfig/gnutls-3
PKG_CONFIG_PATH = $(GNUTLS_PKG_CONFIG_PATH_$(BITS)):$(PKG_CONFIG_PATH.$(BITS))

LD_OPTIONS.32 += -L/usr/lib/gnutls-3 -R/usr/lib/gnutls-3
LD_OPTIONS.64 += -L/usr/lib/$(MACH64)/gnutls-3 -R/usr/lib/$(MACH64)/gnutls-3
LD_OPTIONS += $(LD_OPTIONS.$(BITS))

#COMPONENT_PREP_ACTION = \
#			cd $(@D)/locales && \
#			for LOC in *_*; do mv $$LOC $${LOC/_??} ; done

COMPONENT_PREP_ACTION = cd $(@D) && autoreconf -fi

CONFIGURE_OPTIONS += --disable-static
CONFIGURE_OPTIONS += --disable-manualupdatecheck
CONFIGURE_OPTIONS += --disable-autoupdatecheck
CONFIGURE_OPTIONS += --with-dbus
CONFIGURE_OPTIONS += --with-wx-config=wx-config-3
CONFIGURE_OPTIONS += --with-pugixml=builtin

build:		$(BUILD_64)

install:	$(INSTALL_64)

test:		$(TEST_64)

REQUIRED_PACKAGES += desktop/xdg/xdg-utils
