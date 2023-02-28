#
# Copyright (C) 2009-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=ink
PKG_VERSION:=0.5.3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/ink
PKG_HASH:=2d318fb6a826ef3a2c7cd1e889f42971fd7ae682e3e0ba471c8a0016375a60ba

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/ink
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=A utility for reading ink levels
  URL:=http://ink.sourceforge.net/
  DEPENDS:=+libinklevel
endef

TARGET_LDFLAGS += \
	-lusb

define Package/ink/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/ink $(1)/opt/bin/
endef

$(eval $(call BuildPackage,ink))
