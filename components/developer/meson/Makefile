# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"). You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2017 Aurelien Larcher
# Copyright 2018 Michal Nowak
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=          meson
COMPONENT_VERSION=       0.48.1
COMPONENT_SUMMARY=       The Meson Build system
COMPONENT_PROJECT_URL=   http://mesonbuild.com/
COMPONENT_FMRI=          developer/build/meson
COMPONENT_CLASSIFICATION=Development/Distribution Tools
COMPONENT_SRC=          $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=      $(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_URL= \
  https://github.com/mesonbuild/meson/releases/download/$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH= \
  sha256:425d12edbb81498314926afa93a3eb2fca4ca6929cbe0f8abeb6ab45d1d9fa8f
COMPONENT_LICENSE=      APLv2

PATCH_LEVEL = 0

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/setup.py.mk
include $(WS_MAKE_RULES)/ips.mk

PYTHON_VERSION =3.5
PYTHON_VERSIONS=3.5

PATH=$(PATH.gnu)

COMPONENT_INSTALL_ARGS = --root $(PROTO_DIR) --force --prefix=/usr --install-lib=$(PYTHON_LIB)

COMPONENT_TEST_ENV +=  CFLAGS="$(CFLAGS) $(XPG6MODE)" CPPFLAGS="$(CPPFLAGS) $(CPP_XPG6MODE)"

COMPONENT_TEST_DIR =    $(COMPONENT_SRC)

COMPONENT_TEST_ENV += \
		LANG=C.UTF-8 \
		MESON_EXE=$(PROTO_DIR)/usr/bin/meson \
		MESON_PRINT_TEST_OUTPUT=1

COMPONENT_TEST_ARGS = run_tests.py

build:          $(BUILD_NO_ARCH)

install:        $(INSTALL_NO_ARCH)

#test:		$(TEST_NO_ARCH)
test:		$(TEST_64)

# Auto-generated dependencies
REQUIRED_PACKAGES += library/python/setuptools-35
REQUIRED_PACKAGES += runtime/python-35
