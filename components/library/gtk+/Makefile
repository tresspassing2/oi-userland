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
# Copyright 2016 Alexander Pyhalov
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME= gtk+

COMPONENT_VERSION= 2.24.30
COMPONENT_SUMMARY= GTK+ - GIMP Toolkit Library for creation of graphical user interfaces
COMPONENT_SRC= $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE= $(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_HASH= \
  sha256:0d15cec3b6d55c60eac205b1f3ba81a1ed4eadd9d0f8e7c508bc7065d0c4ca50
COMPONENT_ARCHIVE_URL= \
  http://ftp.gnome.org/pub/GNOME/sources/$(COMPONENT_NAME)/2.24/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL = http://www.gtk.org/

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

gcc_OPT = -O2
CFLAGS += -I/usr/X11/include

COMPONENT_PRE_CONFIGURE_ACTION =	(chmod -R u+r  $(SOURCE_DIR) && \
					cp -r $(SOURCE_DIR)/* $(@D) && \
                                        cd $(@D) && libtoolize --force &&\
                                        aclocal -I ./m4 &&\
					gtkdocize &&\
                                        autoheader &&\
                                        automake -a -f -c --gnu &&\
                                        autoconf )

CONFIGURE_SCRIPT = $(@D)/configure

CONFIGURE_OPTIONS.32 = --sysconfdir=/etc
CONFIGURE_OPTIONS.64 = --sysconfdir=/etc/$(MACH64)
CONFIGURE_OPTIONS += --enable-shm
CONFIGURE_OPTIONS += --with-gdktarget=x11
CONFIGURE_OPTIONS += --enable-explicit-deps=yes
CONFIGURE_OPTIONS += --without-libjasper
CONFIGURE_OPTIONS += --enable-man

CONFIGURE_ENV    += XGETTEXT=/usr/gnu/bin/xgettext
CONFIGURE_ENV    += MSGFMT=/usr/gnu/bin/msgfmt
CONFIGURE_ENV    += PERL=$(PERL)
CONFIGURE_ENV    += PYTHON=$(PYTHON)

# CFLAGS are not passed to compiler when g-ir-scanner is used
COMPONENT_BUILD_ENV += CFLAGS="$(CFLAGS)"
COMPONENT_BUILD_ENV += CC="$(CC)"

COMPONENT_POST_INSTALL_ACTION.32 = ( $(GSED) -i -e 's:/usr/bin/env python:$(PYTHON):' $(PROTO_DIR)/usr/bin/gtk-builder-convert )
COMPONENT_POST_INSTALL_ACTION.64 = ( $(GSED) -i -e 's:/usr/bin/env python:$(PYTHON):' $(PROTO_DIR)/usr/bin/$(MACH64)/gtk-builder-convert )
COMPONENT_POST_INSTALL_ACTION += $(COMPONENT_POST_INSTALL_ACTION.$(BITS))

build: $(BUILD_32_and_64)

install: $(INSTALL_32_and_64)

test: $(NO_TESTS)

REQUIRED_PACKAGES += library/desktop/atk
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/desktop/gdk-pixbuf
REQUIRED_PACKAGES += library/desktop/gtk2
REQUIRED_PACKAGES += library/desktop/pango
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/print/cups-libs
REQUIRED_PACKAGES += library/print/open-printing
REQUIRED_PACKAGES += runtime/python-26
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/fontconfig
REQUIRED_PACKAGES += system/library/math
REQUIRED_PACKAGES += x11/library/libx11
REQUIRED_PACKAGES += x11/library/libxcomposite
REQUIRED_PACKAGES += x11/library/libxcursor
REQUIRED_PACKAGES += x11/library/libxdamage
REQUIRED_PACKAGES += x11/library/libxext
REQUIRED_PACKAGES += x11/library/libxfixes
REQUIRED_PACKAGES += x11/library/libxinerama
REQUIRED_PACKAGES += x11/library/libxrandr
REQUIRED_PACKAGES += x11/library/libxrender
