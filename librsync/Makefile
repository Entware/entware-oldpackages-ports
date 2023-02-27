#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=librsync
PKG_VERSION:=2.3.4
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=e364852674780e43d578e4239128ff7014190ed3
PKG_SOURCE_URL:=https://github.com/librsync/librsync.git
PKG_MIRROR_HASH:=337f589a49319fec06eb7f07edb3ed6b97d5e262c037cec1ffe7b526adcb1e78

CMAKE_INSTALL:=1

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

define Package/librsync/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/librsync.so* $(1)/opt/lib
endef

$(eval $(call BuildPackage,librsync))
