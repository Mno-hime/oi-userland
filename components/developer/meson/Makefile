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

PREFERRED_BITS= 64

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=          meson
COMPONENT_VERSION=       0.48.0
COMPONENT_SUMMARY=       The Meson Build system
COMPONENT_PROJECT_URL=   http://mesonbuild.com/
COMPONENT_FMRI=          developer/build/meson
COMPONENT_CLASSIFICATION=Development/Distribution Tools
COMPONENT_SRC=          $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=      $(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_URL= \
  https://github.com/mesonbuild/meson/releases/download/$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH= \
  sha256:982937ba5b380abe13f3a0c4dff944dd19d08b72870e3b039f5037c91f82835f
COMPONENT_LICENSE=      APLv2

PATCH_LEVEL = 0

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/setup.py.mk
include $(WS_MAKE_RULES)/ips.mk

PYTHON_VERSION =3.5
PYTHON_VERSIONS=3.5
VARIANT_PYTHON35 = $(BUILD_DIR)/python-35

PATH=$(PATH.gnu)

COMPONENT_TEST_ENV +=  CFLAGS="$(CFLAGS) $(XPG6MODE)" CPPFLAGS="$(CPPFLAGS) $(CPP_XPG6MODE)"

COMPONENT_INSTALL_ARGS = --root $(PROTO_DIR) --force --prefix=/usr --install-lib=$(PYTHON_LIB)

COMPONENT_TEST_DIR =    $(COMPONENT_SRC)

COMPONENT_TEST_ENV += \
		LANG=C.UTF-8 \
		MESON_EXE=$(PROTO_DIR)/usr/bin/meson \
		MESON_PRINT_TEST_OUTPUT=1

COMPONENT_TEST_ARGS = run_tests.py

build:          $(BUILD_NO_ARCH)

install:        $(INSTALL_NO_ARCH)

REQUIRED_PACKAGES += library/python/setuptools-35
REQUIRED_PACKAGES += runtime/python-35
