#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2006

include $(TOPDIR)/rules.mk

PKG_NAME:=oidentd
PKG_VERSION:=2.0.8
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/ojnk
PKG_HASH:=a54cbed187281f8d5a301d1d8fd5cb0f30bfb13a5a8e9ab752ace76c1010fb6f

include $(INCLUDE_DIR)/package.mk

define Package/oidentd
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Identd server
  URL:=http://dev.ojnk.net/
endef

define Package/oidentd/description
	A nat aware identd server that will correctly forwared requests to clients.
endef

define Package/oidentd/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/oidentd $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S39oidentd $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,oidentd))
