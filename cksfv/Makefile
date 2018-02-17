#
# Copyright (C) 2010-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2009

include $(TOPDIR)/rules.mk

PKG_NAME:=cksfv
PKG_VERSION:=1.3.14
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://zakalwe.fi/~shd/foss/cksfv/files
PKG_HASH:=010facce85b317b7b9f952c84cd59ce03476a2b685db33a49b6ea0d1b38378ea

include $(INCLUDE_DIR)/package.mk

define Package/cksfv
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=cksfv CRC32 checksum verification tool
  URL:=http://zakalwe.fi/~shd/foss/cksfv/
endef

define Package/cksfv/description
  cksfv is a tool for verifying CRC32 checksums.
endef

define Package/cksfv/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/cksfv $(1)/opt/sbin/cksfv
endef

$(eval $(call BuildPackage,cksfv))
