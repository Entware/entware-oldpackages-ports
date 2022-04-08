#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=elinks
PKG_VERSION:=0.15.0
PKG_REV:=90cc102d68c3e43aca9c6acd304a1e44c34dc14a
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/rkd77/elinks.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_MIRROR_HASH:=4262a70449711acf26d66e262ccf8e1d32e039642a6865c60d4f7bd6d52721ab

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/elinks
	SECTION:=net
	CATEGORY:=Network
	DEPENDS:=+ca-bundle +libbz2 +libevent2 +libexpat +libopenssl +libidn +libzstd $(ICONV_DEPENDS)
	TITLE:=A text based web browser
	URL:=http://elinks.or.cz/
endef

define Package/elinks/description
 An advanced text based web browser.
endef

CONFIGURE_ARGS += \
	--enable-256-colors \
	--enable-utf-8 \
	--with-libevent \
	--with-libiconv-prefix="$(ICONV_PREFIX)" \
	--with-libintl-prefix="$(INTL_PREFIX)"

define Package/elinks/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/elinks $(1)/opt/bin
endef

$(eval $(call BuildPackage,elinks))
