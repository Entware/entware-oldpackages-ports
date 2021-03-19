#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# We are using current snapshot tar ball, because GIT source is too slow
# to rely on it.

include $(TOPDIR)/rules.mk

PKG_NAME:=elinks
PKG_VERSION:=0.13
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-current-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://elinks.or.cz/download
PKG_HASH:=skip

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_UNPACK=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xf $(DL_DIR)/$(PKG_SOURCE)

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/elinks
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libopenssl +libbz2 +libidn
  TITLE:=A text based web browser
  URL:=http://elinks.or.cz/
endef

define Package/elinks/description
An advanced text based web browser
endef

CONFIGURE_ARGS += \
	--enable-small \
	--enable-256-colors \
	--enable-utf-8 \
	--without-lzma

define Package/elinks/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/elinks $(1)/opt/bin
endef

$(eval $(call BuildPackage,elinks))
