#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# The newer versions requires libotr 4.0.0 https://wiki.bitlbee.org/bitlbee-otr

include $(TOPDIR)/rules.mk

PKG_NAME:=bitlbee
PKG_VERSION:=3.2.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://get.bitlbee.org/src \
	http://get.bitlbee.be/src \
	http://get.us.bitlbee.org/src \
	http://ftp.snt.utwente.nl/pub/software/bitlbee/src
PKG_MD5SUM:=6ee7c7a99eb59dfcf0307fcf44c14105

PKG_BUILD_DEPENDS:=glib2

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/bitlbee
  SUBMENU:=Instant Messaging
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libgnutls +glib2 +libgcrypt +libotr $(ICONV_DEPENDS)
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
	PKG_BUILD_DEPENDS+= \
	libgnutls
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
	PKG_BUILD_DEPENDS+= \
	libotr
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
			--plugins=/opt/lib/bitlbee/ \
			--config=/opt/var/lib/bitlbee/ \
			--arch=OpenWrt \
			--cpu="$(ARCH)" \
			--debug=0 \
			--strip=1 \
			--ipv6=1 \
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

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)
endef

define Package/bitlbee/install
	$(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" install-etc install-bin
	$(MAKE) -C $(PKG_BUILD_DIR)/doc/user-guide \
		DESTDIR="$(PKG_INSTALL_DIR)" install
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S72bitlbee $(1)/opt/etc/init.d
	$(CP) $(PKG_INSTALL_DIR)/opt/* $(1)/opt/
endef

$(eval $(call BuildPackage,bitlbee))
