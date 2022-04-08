#
# Copyright (C) 2006-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=dialog
PKG_VERSION:=1.3-20220117
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=ftp://ftp.invisible-island.net/dialog \
	https://invisible-mirror.net/archives/dialog
PKG_HASH:=754cb6bf7dc6a9ac5c1f80c13caa4d976e30a5a6e8b46f17b3bb9b080c31041f

include $(INCLUDE_DIR)/package.mk

define Package/dialog
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libncursesw
  TITLE:=Dialog
  URL:=https://invisible-island.net/dialog/
endef

define Package/dialog/description
 A script-interpreter which provides a set of curses widgets.
endef

CONFIGURE_ARGS += \
	--with-ncursesw

define Package/dialog/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dialog $(1)/opt/bin
endef

$(eval $(call BuildPackage,dialog))
