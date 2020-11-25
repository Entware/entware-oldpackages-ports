#
# Copyright (C) 2010-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cksfv
PKG_VERSION:=1.3.15
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://zakalwe.fi/~shd/foss/cksfv/files
PKG_HASH:=a173be5b6519e19169b6bb0b8a8530f04303fe3b17706927b9bd58461256064c

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
