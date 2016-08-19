#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=librsync
PKG_VERSION:=2.0.0
PKG_REV:=26164eeeb34334e66fa4f3d22f296ab407d84507
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/librsync/librsync.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/librsync
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=implementation of the rolling-checksum algorithm
  DEPENDS:=+libbz2 +zlib
  URL:=http://librsync.sourceforge.net/
endef

define Package/librsync/description
	librsync implements the rolling-checksum algorithm of remote file
	synchronization that was popularized by the rsync utility and is
	used in rproxy. This algorithm transfers the differences between 2
	files without needing both files on the same system.
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/librsync{,-config}.h $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/librsync.so* $(1)/opt/lib/
endef

define Package/librsync/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/librsync.so* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,librsync))
