#
# Copyright (C) 2007-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=amule
PKG_VERSION:=2.3.3
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/amule-project/amule/tar.gz/$(PKG_VERSION)?
PKG_HASH:=934f79d4dab41c2d1caea31d6c6e10337c409ba5bb8bd6fac6c63e924e82c9b8

PKG_INSTALL:=1

PKG_BUILD_DEPENDS:=libgd

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/amule
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=P2P
	TITLE:=A multi-platform eMule-like ed2k client
	URL:=http://www.amule.org/
	DEPENDS:=+libbfd +libcryptopp +libncurses +libpng +libreadline \
		 +libwxbase $(ICONV_DEPENDS)
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
	--with-libintl-prefix="$(INTL_PREFIX)"

TARGET_LDFLAGS += \
	-liconv

define Build/Configure
	( cd $(PKG_BUILD_DIR); ./autogen.sh )
	$(call Build/Configure/Default)
endef

define Package/amule/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/amule{cmd,d,web} $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/amule $(1)/opt/share
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S57amuled $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/var/amule
endef

$(eval $(call BuildPackage,amule))
