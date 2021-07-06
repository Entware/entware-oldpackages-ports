#
# Copyright (C) 2007-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=memtester
PKG_VERSION:=4.5.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://pyropus.ca/software/memtester/old-versions
PKG_HASH:=1c5fc2382576c084b314cfd334d127a66c20bd63892cac9f445bc1d8b4ca5a47

include $(INCLUDE_DIR)/package.mk

define Package/memtester
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Userspace utility for testing the memory subsystem for faults
  URL:=http://pyropus.ca/software/memtester/
endef

define Package/memtester/description
 A userspace utility for testing the memory subsystem for faults.
endef

define Build/Configure
	$(SED) 's|^cc|$(TARGET_CC) $(TARGET_CFLAGS)|' $(PKG_BUILD_DIR)/conf-cc
	$(SED) 's|^cc|$(TARGET_CC) $(TARGET_LDFLAGS)|' $(PKG_BUILD_DIR)/conf-ld
endef

define Package/memtester/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/memtester $(1)/opt/sbin
endef

$(eval $(call BuildPackage,memtester))
