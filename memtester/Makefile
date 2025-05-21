#
# Copyright (C) 2007-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=memtester
PKG_VERSION:=4.7.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://pyropus.ca./software/memtester/old-versions \
		https://distfiles.gentoo.org/distfiles/99
PKG_HASH:=e427de663f7bd22d1ebee8af12506a852c010bd4fcbca1e0e6b02972d298b5bb

PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk

define Package/memtester
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Utility for testing the memory subsystem
  URL:=https://pyropus.ca/software/memtester/
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
