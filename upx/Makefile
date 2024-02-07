#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=upx
PKG_VERSION:=4.2.2
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=099c3d829e80488af7395a4242b318877e980da4
PKG_SOURCE_URL:=https://github.com/upx/upx.git
PKG_MIRROR_HASH:=8bee3cd1ada2e4bfbe396348d2aecb3e044f92cdae2b7010838e36997fe6b3c3

CMAKE_BINARY_SUBDIR:=openwrt-build

PKG_BUILD_FLAGS:=no-mips16

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

TAR_CMD:=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components 1 $(TAR_OPTIONS)

define Package/upx
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libucl +libstdcpp +zlib
  TITLE:=The Ultimate Packer for eXecutables
  URL:=https://upx.github.io
endef

define Package/upx/description
UPX is a free, portable, extendable, high-performance executable packer for
several different executable formats. It achieves an excellent compression ratio
and offers very fast decompression. Your executables suffer no memory overhead
or other drawbacks for most of the formats supported, because of in-place
decompression.
endef

MAKE_PATH:= src
MAKE_VARS += exeext=""

TARGET_CXXFLAGS += -DUCL_NO_ASM
TARGET_LDFLAGS += $(if $(CONFIG_GCC_LIBSSP),-lssp)

define Package/upx/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(CMAKE_BINARY_SUBDIR)/upx $(1)/opt/bin
endef

$(eval $(call BuildPackage,upx))
