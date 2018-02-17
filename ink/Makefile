#
# Copyright (C) 2009-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=ink
PKG_VERSION:=0.5.2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/ink
PKG_HASH:=65af1e7d886125889076cd52c0bb09101da1a8811cb8150af0a46afe90ccbbbb

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

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
