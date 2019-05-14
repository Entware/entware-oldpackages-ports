#
# Copyright (C) 2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Used by tesseract only

include $(TOPDIR)/rules.mk

PKG_NAME:=leptonica
PKG_VERSION:=1.78.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.leptonica.org/source
PKG_HASH:=e2ed2e81e7a22ddf45d2c05f0bc8b9ae7450545d995bfe28517ba408d14a5a88

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libleptonica
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=A library for efficient image processing and image analysis operations
  URL:=http://www.leptonica.com/
  DEPENDS:=+giflib +libpng +libtiff
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/leptonica $(1)/opt/include
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libleptonica.so* $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/lept.pc $(1)/opt/lib/pkgconfig
endef

define Package/libleptonica/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libleptonica.so* $(1)/opt/lib
endef

$(eval $(call BuildPackage,libleptonica))
