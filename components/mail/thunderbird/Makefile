#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright (c) 2015, 2019, Oracle and/or its affiliates. All rights reserved.
# Copyright 2017 Alexander Pyhalov
# Copyright 2019 Michal Nowak
#

PREFERRED_BITS=		64

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		thunderbird
COMPONENT_VERSION=	60.6.1
COMPONENT_PROJECT_URL=	https://www.thunderbird.net/
COMPONENT_SUMMARY= 	Mozilla Thunderbird Email/Newsgroup Client
COMPONENT_SRC= 		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE= 	$(COMPONENT_SRC).source.tar.xz
COMPONENT_ARCHIVE_HASH= \
    sha256:17aef9232a76bdc812422883c02b01b4ecb7633c3ee9870da5e4ec0e20ba5f67
ifndef CANDIDATE_BUILD
MOZILLA_FTP = 		http://ftp.mozilla.org/pub/$(COMPONENT_NAME)/releases/$(COMPONENT_VERSION)
else
MOZILLA_FTP = 		http://ftp.mozilla.org/pub/$(COMPONENT_NAME)/candidates/$(COMPONENT_VERSION)-candidates/build$(CANDIDATE_BUILD)
endif
COMPONENT_ARCHIVE_URL=	$(MOZILLA_FTP)/source/$(COMPONENT_ARCHIVE)

LANG_LIST=	ar bg ca cs da de el es-AR es-ES et fi fr he hr hu id is it ja ko lt nl nn-NO pl pt-BR pt-PT ro ru sk sl sq sr sv-SE tr uk vi zh-CN zh-TW
LANG_FILES_LOCATION=	http://ftp.mozilla.org/pub/mozilla.org/thunderbird/releases/$(COMPONENT_VERSION)/linux-i686/xpi/

LIGHTNING_VERSION=6.2
LIGHTNING_DIR="$(PROTO_DIR)/usr/lib/thunderbird-$(COMPONENT_VERSION)/extensions/{e2fda1a4-762b-4020-b5ad-a41df1933103}"
GDATA_PROVIDER_DIR="$(PROTO_DIR)/usr/lib/thunderbird/extensions/{a62ef8ec-5fdc-40c2-873c-223b8a6925cc}"

COMPONENT_ARCHIVE_1=		lightning-$(LIGHTNING_VERSION)-sm+tb-linux.xpi
COMPONENT_ARCHIVE_HASH_1=	sha256:f858e650a0564fdcea57e3e295c4afce07a4f23aa508d745a4a9e4285b297e38
COMPONENT_ARCHIVE_URL_1=	https://addons.cdn.mozilla.net/user-media/addons/_attachments/2313/$(COMPONENT_ARCHIVE_1)
COMPONENT_ARCHIVE_URL_1=	https://addons.thunderbird.net/thunderbird/downloads/file/1012321/$(COMPONENT_ARCHIVE_1)

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

# because we touched old-configure.in and js/src/old-configure.in
COMPONENT_PRE_CONFIGURE_ACTION += (cd $(COMPONENT_NAME)-$(COMPONENT_VERSION); autoreconf; touch configure; cd js/src; autoreconf; touch configure);

COMPONENT_POST_BUILD_ACTION = \
        (cd $(@D)/mail/installer ; $(ENV) $(COMPONENT_BUILD_ENV) \
                $(GMAKE) $(COMPONENT_BUILD_ARGS) $(COMPONENT_BUILD_TARGETS))

PATH=$(USRBINDIR.64):$(PATH.illumos)

GNU_ARCH=               x86_64-sun-solaris


FIREFOX_LIBDIR =        $(CONFIGURE_LIBDIR.$(BITS))

MOZCONFIG=		$(SOURCE_DIR)/mozconfig

CONFIGURE_OPTIONS=
# build/amd64/dist/system_wrappers/event.h:3:24: fatal error: event.h: No such file or directory
#CONFIGURE_OPTIONS +=	--enable-system-libevent
#CONFIGURE_OPTIONS +=	--enable-system-nspr
#CONFIGURE_OPTIONS +=	--enable-system-nss
# xpcshell: Undefined symbol sqlite3_expanded_sql referenced in ../../../toolkit/library/libxul.so
#CONFIGURE_OPTIONS +=	--enable-system-sqlite

COMPONENT_PRE_CONFIGURE_ACTION += \
	echo "ac_add_options --prefix=$(CONFIGURE_PREFIX)" >> $(MOZCONFIG) ; \
	echo "ac_add_options --libdir=$(FIREFOX_LIBDIR)" >> $(MOZCONFIG) ; \
	echo "ac_add_options --host=$(GNU_ARCH)" >> $(MOZCONFIG) ; \
	echo "ac_add_options --target=$(GNU_ARCH)" >> $(MOZCONFIG) ; \
	echo "ac_add_options MOZILLA_OFFICIAL=1" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-application=comm/mail" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-calendar" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-default-toolkit=cairo-gtk3" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-optimize=\"-O2 -fno-schedule-insns2 -fno-lifetime-dse -fno-delete-null-pointer-checks\"" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-install-strip" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-official-branding" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-update-channel=esr" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-release" >> $(MOZCONFIG) ; \
	echo "ac_add_options --disable-debug" >> $(MOZCONFIG) ; \
	echo "ac_add_options --disable-debug-symbols" >> $(MOZCONFIG) ; \
	echo "ac_add_options --disable-tests" >> $(MOZCONFIG) ; \
	echo "ac_add_options --disable-updater" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-system-bz2" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-system-ffi" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-system-pixman" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-system-zlib" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-dbus" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-intl-api" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-libproxy" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-pthreads" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-pulseaudio" >> $(MOZCONFIG) ; \
	echo "ac_add_options --enable-startup-notification" >> $(MOZCONFIG) ; \
	echo "ac_add_options --disable-alsa" >> $(MOZCONFIG) ; \
	echo "ac_add_options --disable-crashreporter" >> $(MOZCONFIG) ; \
	echo "ac_add_options --disable-dtrace" >> $(MOZCONFIG) ; \
	echo "ac_add_options --disable-jemalloc" >> $(MOZCONFIG) ; \
	echo "ac_add_options --disable-webrtc" >> $(MOZCONFIG) ; \

COMPONENT_BUILD_ARGS += $(JOBS:%=-j%)

CXXFLAGS +=	-Wno-invalid-offsetof -fpermissive

ENV +=  SHELL=/usr/bin/sh
ENV +=	CC=$(CC)
ENV +=	CXX=$(CXX)
ENV +=	MOZILLA_OFFICIAL=1
ENV +=	MOZ_PKG_FORMAT=BZ2
ENV +=	PKG_SKIP_STRIP=1
ENV +=	MOZILLA_PKG_NAME=thunderbird
ENV +=	CXXFLAGS="$(CXXFLAGS)"
ENV +=  OS_DEFINES="-D__USE_LEGACY_PROTOTYPES__"
ENV +=  LDFLAGS="-L$(BUILD_DIR_64)/dist/lib -L$(BUILD_DIR_64)/dist/bin"

CONFIGURE_ENV =	$(ENV)
COMPONENT_BUILD_ENV =	$(ENV)
COMPONENT_INSTALL_ENV += HOME=/tmp

LANG_FILES=$(addsuffix .xpi,$(LANG_LIST))

CLEAN_PATHS += $(LANG_FILES)

#COMPONENT_BUILD_ARGS =

$(LANG_FILES): 
	$(FETCH) --file $@  --url $(LANG_FILES_LOCATION)/$@

COMPONENT_POST_INSTALL_ACTION += \
	$(RM) -r $(LIGHTNING_DIR) ; \
	$(CP) -r $(BUILD_DIR_64)/dist/bin/distribution/extensions/{e2fda1a4-762b-4020-b5ad-a41df1933103} \
	  $(LIGHTNING_DIR) ; \
	unzip -u -d $(LIGHTNING_DIR) $(USERLAND_ARCHIVES)$(COMPONENT_ARCHIVE_1); \
	for file in $(PROTO_DIR)/usr/lib/thunderbird-$(COMPONENT_VERSION)/*.so \
          $(PROTO_DIR)/usr/lib/thunderbird-$(COMPONENT_VERSION)/plugin-container; do \
	  /usr/bin/elfedit -e 'dyn:value -s  RUNPATH "$(GCC_ROOT)/lib:/usr/lib/thunderbird"' $$file ;\
	  /usr/bin/elfedit -e 'dyn:value -s  RPATH "$(GCC_ROOT)/lib:/usr/lib/thunderbird"' $$file ;\
	done ;


COMPONENT_POST_INSTALL_ACTION += \
	list1='$(LANG_LIST)' ; for f in $$list1 ; do \
	  $(CP) $$f.xpi \
	    $(PROTOUSRLIBDIR)/thunderbird-$(COMPONENT_VERSION)/extensions/langpack-$$f@thunderbird.mozilla.org.xpi ; \
	done ;

COMPONENT_TEST_DIR =    $(@D)/js/src
COMPONENT_TEST_TARGETS=check-jit-test
COMPONENT_TEST_TRANSFORMS += \
	'-e "/\(^TEST-PASS\).*/d" '

$(SOURCE_DIR)/.patched-firefox-%: GPATCH_FLAGS += -d $(@D)

download prep:: $(LANG_FILES)

build:		$(BUILD_64)

install:	$(INSTALL_64)

test:		$(TEST_64)

# Auto-generated dependencies
REQUIRED_PACKAGES += developer/build/autoconf-213
REQUIRED_PACKAGES += $(GCC_RUNTIME_PKG)
REQUIRED_PACKAGES += $(GXX_RUNTIME_PKG)
REQUIRED_PACKAGES += library/desktop/atk
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/desktop/gdk-pixbuf
REQUIRED_PACKAGES += library/desktop/gtk2
REQUIRED_PACKAGES += library/desktop/pango
REQUIRED_PACKAGES += library/desktop/startup-notification
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/graphics/pixman
REQUIRED_PACKAGES += library/libffi
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += SUNWcs
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/fontconfig
REQUIRED_PACKAGES += system/library/freetype-2
REQUIRED_PACKAGES += system/library/libdbus
REQUIRED_PACKAGES += system/library/libdbus-glib
REQUIRED_PACKAGES += system/library/math
REQUIRED_PACKAGES += x11/library/libx11
REQUIRED_PACKAGES += x11/library/libxcb
REQUIRED_PACKAGES += x11/library/libxcomposite
REQUIRED_PACKAGES += x11/library/libxcursor
REQUIRED_PACKAGES += x11/library/libxdamage
REQUIRED_PACKAGES += x11/library/libxext
REQUIRED_PACKAGES += x11/library/libxfixes
REQUIRED_PACKAGES += x11/library/libxinerama
REQUIRED_PACKAGES += x11/library/libxrandr
REQUIRED_PACKAGES += x11/library/libxrender
REQUIRED_PACKAGES += x11/library/toolkit/libxt
