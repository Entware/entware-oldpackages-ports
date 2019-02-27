#
# Copyright (C) 2006-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=dialog
PKG_VERSION:=1.3-20190211
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=ftp://ftp.invisible-island.net/dialog
PKG_HASH:=49c0e289d77dcd7806f67056c54f36a96826a9b73a53fb0ffda1ffa6f25ea0d3

include $(INCLUDE_DIR)/package.mk

define Package/dialog
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libncursesw
  TITLE:=Dialog
  URL:=http://invisible-island.net/dialog/
endef

define Package/dialog/description
 A script-interpreter which provides a set of curses widgets.
endef

CONFIGURE_ARGS+= \
	--with-ncursesw \

define Package/dialog/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dialog $(1)/opt/bin
endef

$(eval $(call BuildPackage,dialog))
