#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libinklevel
PKG_VERSION:=0.9.7
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/libinklevel
PKG_HASH:=819d3bb4c2578722c1057c9f3da999a1a3eb46628f0fe91aeb52bfccd3884675

PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libinklevel
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Printers Ink Level Library
  URL:=https://libinklevel.sourceforge.net/
  DEPENDS:=+libusb-compat +libxml2
endef

define Package/libinklevel/description
  Libinklevel is a library for checking the ink level of your printer
  on a system which runs Linux.
endef

TARGET_CFLAGS += \
	$(FPIC) \
	-I"$(STAGING_DIR)/opt/include/libusb-1.0"

MAKE_ARGS += LIBS="$(TARGET_LIBS)"

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/inklevel.h $(1)/opt/include
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libinklevel.so* $(1)/opt/lib
endef

define Package/libinklevel/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libinklevel.so* $(1)/opt/lib
endef

$(eval $(call BuildPackage,libinklevel))
