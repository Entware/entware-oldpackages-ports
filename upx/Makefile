#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=upx
PKG_VERSION:=4.2.4
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/upx/upx
PKG_MIRROR_HASH:=351f83879d0a65a25e0eb1b0761bbc5fad9c521601e4b05e7006b394da9bb8b0

PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING LICENSE

PKG_BUILD_FLAGS:=no-mips16

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/upx
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=The Ultimate Packer for eXecutables
  URL:=https://upx.github.io
  DEPENDS:=+libstdcpp
endef

define Package/upx/description
  UPX is a free, portable, extendable, high-performance executable
  packer for several different executable formats. It achieves an excellent
  compression ratio and offers very fast decompression. Your executables suffer
  no memory overhead or other drawbacks for most of the formats supported,
  because of in-place decompression.
endef

TARGET_CXXFLAGS += -DUCL_NO_ASM
TARGET_LDFLAGS += $(if $(CONFIG_GCC_LIBSSP),-lssp)

define Package/upx/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/upx $(1)/opt/bin
endef

$(eval $(call BuildPackage,upx))
