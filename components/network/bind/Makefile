#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#
# Copyright (c) 2011, 2019, Oracle and/or its affiliates. All rights reserved.
# Copyright (c) 2019, Michal Nowak
#

PREFERRED_BITS=		64

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		bind
COMPONENT_VERSION=	9.11.7
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_PROJECT_URL=	http://www.isc.org/software/bind/
COMPONENT_ARCHIVE_HASH=	 \
	sha256:5b9e86dc5711a1a7448356c02ddb23bb1dd78c9e02a69f9b2e2ce31d39f5a0fd
COMPONENT_ARCHIVE_URL=	\
	http://ftp.isc.org/isc/bind9/$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

#PATH=$(PATH.gnu)

CFLAGS +=		-I/usr/include/idn2

# We don't need -m32 for 32-bit builds, especially when it is passed to ld
LD_BITS=

# Missing files in build dir without this.
COMPONENT_PRE_CONFIGURE_ACTION =	($(CLONEY) $(SOURCE_DIR) $(@D))

# Build.
#
# FYI, The configure options are displayed by 'named -V'.  Previously
# that was overriden by setting CONFIGARGS to hide build server
# pathnames.

# DNS libraries are in usr/lib/dns - Override settings from configure.mk
CONFIGURE_LIBDIR =	$(CONFIGURE_PREFIX)/lib/dns

CONFIGURE_OPTIONS +=	--with-libtool
CONFIGURE_OPTIONS +=	--with-pic
CONFIGURE_OPTIONS +=	--disable-static
CONFIGURE_OPTIONS +=	--enable-shared
CONFIGURE_OPTIONS +=	--without-python
CONFIGURE_OPTIONS +=	--disable-getifaddrs
#CONFIGURE_OPTIONS +=	
CONFIGURE_OPTIONS +=	--sysconfdir=/etc
CONFIGURE_OPTIONS +=	--localstatedir=/var
CONFIGURE_OPTIONS +=	--with-openssl
CONFIGURE_OPTIONS +=	--enable-threads=yes
CONFIGURE_OPTIONS +=	--enable-ipv6
CONFIGURE_OPTIONS +=	--enable-devpoll=yes
CONFIGURE_OPTIONS +=	--enable-fixed-rrset
CONFIGURE_OPTIONS +=	--enable-native-pkcs11
CONFIGURE_OPTIONS +=	--with-pkcs11=/usr/lib/amd64/softhsm/libsofthsm2.so
CONFIGURE_OPTIONS +=	--with-libidn2=yes
CONFIGURE_OPTIONS +=	--with-geoip
# Bind configure will check for libxml2 versions 2.6.x/2.7.x/2.8.x.
# To make it use version 2.9.x we need to skip this check by
# specifying path where libxml2 is installed.
CONFIGURE_OPTIONS +=	--with-libxml2=/usr

CONFIGURE_ENV +=	PYTHON=$(PYTHON)

COMPONENT_BUILD_ENV += PYTHON_VENDOR_DIR=$(PYTHON_VENDOR_PACKAGES)
COMPONENT_INSTALL_ENV += PYTHON_VENDOR_DIR=$(PYTHON_VENDOR_PACKAGES)

# Enable ASLR for this component
ASLR_MODE = $(ASLR_ENABLE)

.PHONY: build
build:		$(BUILD_64)

include $(WS_MAKE_RULES)/shared-targets.mk

# Install.
#
# Currently manual pages are distributed from pkg:/system/manual@.
# While there are some changes in our manuals, for example section
# numbering and additions to named(1M) for SMF - that could be fixed
# by patch.
#
# In addition to BIND deliverables we also deliver SMF files and
# migration notes.  There is no need to install these extras into the
# prototype directory, they are simply referenced in relevant manifest
# (p5m) file.

.PHONY: install
install: $(INSTALL_64)

# Testing.
#
# sumarize nawk script; reads ISC output which is of the form:
# /^T:/ = Start of a test.
# /^I:/ = Info from a test;  colleced for possible use later.
# /^A:/ = About: summary of the test - not used here.
# /^R:/ = Result: If 'PASS' then continue, else print line and collected info.
# Known issues may then be accounted for.
# @ EOF = Display count of RESULTS: i.e. R:PASS=124 R:UNTESTED=26 Total=150
# if not 100% pass rate and issue is not known the word 'issues!' is appended
# to resulting string.
summarize=	'\
		/^T:/ {name=$$0;info="";}\
		/^I:/ {info=sprintf("%s%s\n", info, $$0);}\
		/^R:/ {test++; result[$$1]++;}\
		/^R:PASS/ {next;}\
		/^R:/ {printf("%s: %s\n%s\n", $$1, name, info);}\
		/^R:UNTESTED/ && name ~ /^T:dst:2:A/ {known++;}\
		/^R:UNRESOLVED/ && name ~ /^T:dst:1:A/ {known++;}\
		END{for (item in result)\
				printf("%s=%d ", item, result[item]);\
			printf("(known=%d) Total=%d%s\n", known, test, \
				((result["R:PASS"] + known) < test)? \
				" issues!" : "");\
		}'

isc_ifconfig=	./bin/tests/system/ifconfig.sh

.PHONY: test
test: build $(TEST_64)

# fulltest requires sufficient privileges to configures IP addresses
# 10.53.0.1 through 10.53.0.5 as aliases on the loopback interface.
FULL_TEST_64=	$(TEST_64:%=%_FULL)

.PHONY: fulltest
fulltest: build $(FULL_TEST_64)

$(FULL_TEST_64):
	cd $(COMPONENT_SRC) && $(SHELL)  $(isc_ifconfig) up
	-cd $(@D) && $(MAKE) test 2>&1 | $(TEE) $@
	cd $(COMPONENT_SRC) && $(SHELL) $(isc_ifconfig) down
	$(NAWK) $(summarize) $@

$(TEST_64):
	-cd $(@D) && $(MAKE) test 2>&1 | $(TEE) $@
	$(NAWK) $(summarize) $@

# test-summary shows summary for targets test and fulltest. Use target
# test-clean to remove previous tests.
.PHONY: test-summary
test-summary:
	@for file in $(TEST_64)*; do \
		if [ -f $$file ]; then \
			echo 'Summary for' $$file;\
			$(NAWK) $(summarize) $$file;\
			fi;\
		done

.PHONY: test-version
test-version:
	@echo;echo 64 bit version
	-LD_LIBRARY_PATH=$(PROTO_DIR)$(CONFIGURE_LIBDIR.64) \
		$(PROTO_DIR)$(CONFIGURE_BINDIR.64)/named -V

.PHONY: test-clean
test-clean:
	$(RM) $(TEST_64) $(FULL_TEST_64)

REQUIRED_PACKAGES += library/json-c
REQUIRED_PACKAGES += library/libedit
REQUIRED_PACKAGES += library/libxml2
REQUIRED_PACKAGES += library/security/openssl
REQUIRED_PACKAGES += network/dns/bind
REQUIRED_PACKAGES += service/security/kerberos-5
REQUIRED_PACKAGES += SUNWcs
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/security/gss
