#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=bitlbee
PKG_VERSION:=3.4.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://get.bitlbee.org/src \
	http://get.bitlbee.be/src \
	http://get.us.bitlbee.org/src \
	http://ftp.snt.utwente.nl/pub/software/bitlbee/src \
	http://bitlbee.intergenia.de/src
PKG_MD5SUM:=dc2d66c0b01d450ce8b44e1f8baf0378

PKG_BUILD_DEPENDS:=glib2

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/bitlbee
  SUBMENU:=Instant Messaging
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+glib2 +libgcrypt +BITLBEE_OTR:libotr +BITLBEE_ENABLE_SSL:libgnutls
  TITLE:=IRC gateway to IM chat networks
  URL:=http://www.bitlbee.org/
endef

define Package/bitlbee/config
  source "$(SOURCE)/Config.in"
endef

define Package/bitlbee/conffiles
/opt/etc/bitlbee/motd.txt
/opt/etc/bitlbee/bitlbee.conf
endef

ifeq ($(CONFIG_BITLBEE_ENABLE_SSL),y)
	EXTRA_CONF_OPTS+= \
	--ssl=gnutls
else
	EXTRA_CONF_OPTS:=--ssl=bogus
endif
ifneq ($(CONFIG_BITLBEE_MSN),y)
	EXTRA_CONF_OPTS+= \
	--msn=0
endif
ifneq ($(CONFIG_BITLBEE_JABBER),y)
	EXTRA_CONF_OPTS+= \
	--jabber=0
endif
ifneq ($(CONFIG_BITLBEE_OSCAR),y)
	EXTRA_CONF_OPTS+= \
	--oscar=0
endif
ifneq ($(CONFIG_BITLBEE_YAHOO),y)
	EXTRA_CONF_OPTS+= \
	--yahoo=0 
endif
ifneq ($(CONFIG_BITLBEE_TWITTER),y)
	EXTRA_CONF_OPTS+= \
	--twitter=0
endif
ifneq ($(CONFIG_BITLBEE_ENABLE_PLUGINS),y)
	EXTRA_CONF_OPTS+= \
	--plugins=0
endif
ifeq ($(CONFIG_BITLBEE_OTR),y)
	EXTRA_CONF_OPTS+= \
	--otr=1
endif

define Build/Configure
	# it's not GNU autoconf stuff
	(cd $(PKG_BUILD_DIR); \
		$(TARGET_CONFIGURE_OPTS) \
		CFLAGS="$(TARGET_CFLAGS)" \
		CPPFLAGS="$(TARGET_CPPFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		STRIP="$(TARGET_CROSS)strip" \
		STAGING_DIR="$(STAGING_DIR)" \
		./configure \
			--prefix=/opt/ \
			--bindir=/opt/sbin/ \
			--etcdir=/opt/etc/bitlbee/ \
			--datadir=/opt/share/bitlbee/ \
			--plugindir=/opt/lib/bitlbee/ \
			--pidfile=/opt/var/run/bitlbee.pid \
			--config=/opt/var/lib/bitlbee/ \
			--debug=0 \
			--strip=1 \
			$(EXTRA_CONF_OPTS) \
	);
	$(SED) 's,^CFLAGS=.*,CFLAGS=$(TARGET_CFLAGS),g'\
		$(PKG_BUILD_DIR)/Makefile.settings
	@echo 'CFLAGS+=-I$(ICONV_PREFIX)/include' >> \
		$(PKG_BUILD_DIR)/Makefile.settings
	@echo 'LFLAGS+=$(TARGET_LDFLAGS)' >> \
		$(PKG_BUILD_DIR)/Makefile.settings
	@echo 'LFLAGS+=-L$(ICONV_PREFIX)/lib' >> \
		$(PKG_BUILD_DIR)/Makefile.settings
	$(SED) 's| -pthread | -lpthread -lc -l:libgcc_s.so.1 |g'\
		$(PKG_BUILD_DIR)/Makefile.settings
	$(SED) 's|-Wl,||g'\
		$(PKG_BUILD_DIR)/Makefile.settings
	$(SED) 's|-rpath,/opt/lib|-rpath /opt/lib|g'\
		$(PKG_BUILD_DIR)/Makefile.settings
endef

define Package/bitlbee/install
	$(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" install-etc install-bin
	$(MAKE) -C $(PKG_BUILD_DIR)/doc/user-guide \
		DESTDIR="$(PKG_INSTALL_DIR)" install
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S72bitlbee $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/etc/bitlbee $(1)/opt/sbin $(1)/opt/share/bitlbee
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/bitlbee/* $(1)/opt/etc/bitlbee
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/bitlbee $(1)/opt/sbin
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/share/bitlbee/help.txt $(1)/opt/share/bitlbee
endef

$(eval $(call BuildPackage,bitlbee))
