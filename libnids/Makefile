#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Used by dsniff only, no need to update it

include $(TOPDIR)/rules.mk

PKG_NAME:=libnids
PKG_VERSION:=1.24
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/libnids
PKG_HASH:=314b4793e0902fbf1fdb7fb659af37a3c1306ed1aad5d1c84de6c931b351d359

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libnids
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libnet-1.2.x
  TITLE:=A network intrusion detection library
  URL:=http://libnids.sourceforge.net/
endef

define Package/libnids/description
	An implementation of an E-component of Network Intrusion Detection
	System.
endef

CONFIGURE_ARGS += \
	--enable-shared \
	--disable-libglib

TARGET_CFLAGS += $(FPIC)

MAKE_FLAGS += \
	install_prefix="$(PKG_INSTALL_DIR)"

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/nids.h $(1)/opt/include
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libnids.{a,so*} $(1)/opt/lib
endef

define Package/libnids/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libnids.so.* $(1)/opt/lib
endef

$(eval $(call BuildPackage,libnids))
