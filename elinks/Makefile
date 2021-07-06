#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=elinks
PKG_VERSION:=0.14.1
PKG_REV:=9e0c85e5480dfa10aeae35656c004a9262be0b3a
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/rkd77/elinks.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_MIRROR_HASH:=330f53ef1a084756c5efdf00ceee3a9a2e76de111174eb5d1831b8405197b084

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
