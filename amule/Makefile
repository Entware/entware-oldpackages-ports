#
# Copyright (C) 2007-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=amule
PKG_VERSION:=2.3.2
PKG_REV:=20f3a3b3b6f5163d93cafcb98364f36956e72afa
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_MIRROR_HASH:=12225a419c4ca757629a99093d235a30a36d9617334751daeda26ac51786c5fa
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/amule-project/amule.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

PKG_BUILD_DEPENDS:=libgd

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/amule
  SUBMENU:=P2P
  SECTION:=net
  CATEGORY:=Network
  TITLE:=A multi-platform eMule-like ed2k client
  URL:=http://www.amule.org/
  DEPENDS:=+libpng +libncurses +libreadline +libwxbase +libcryptoxx +libbfd
endef

CONFIGURE_ARGS+= \
	--disable-nls \
	--disable-static \
	--disable-rpath \
	--with-gnu-ld \
	--disable-ccache \
	--disable-debug \
	--disable-optimize \
	--disable-profile \
	--disable-monolithic \
	--enable-amule-daemon \
	--enable-amulecmd \
	--enable-webserver \
	--disable-amule-gui \
	--disable-cas \
	--disable-wxcas \
	--disable-ed2k \
	--disable-alc \
	--disable-alcc \
	--disable-fileview \
	--disable-plasmamule \
	--without-wxdebug \
	\
	--with-zlib="$(STAGING_DIR)/opt" \
	--with-gdlib-prefix="$(STAGING_DIR)/opt" \
	--with-libpng-prefix="$(STAGING_DIR)/opt" \
	--with-wx-prefix="$(STAGING_DIR)/opt" \
	--with-crypto-prefix="$(STAGING_DIR)/opt" \
	--with-libiconv-prefix="$(ICONV_PREFIX)" \
	--with-libintl-prefix="$(INTL_PREFIX)" \

TARGET_LDFLAGS += \
	-liconv

TARGET_CFLAGS += \
	-O1

define Build/Configure
	( cd $(PKG_BUILD_DIR); ./autogen.sh )
	$(call Build/Configure/Default)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		HOSTCC="$(HOSTCC)" \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

define Package/amule/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/amule{cmd,d,web} $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/amule $(1)/opt/share/
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S57amuled $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/var/amule
endef

$(eval $(call BuildPackage,amule))
