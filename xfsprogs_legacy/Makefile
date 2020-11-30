#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# This is the last k2.6 compatible version

include $(TOPDIR)/rules.mk

PKG_NAME:=xfsprogs_legacy
PKG_VERSION:=5.5.0
PKG_RELEASE:=2

PKG_SOURCE:=xfsprogs-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@KERNEL/linux/utils/fs/xfs/xfsprogs
PKG_HASH:=cfbb0b136799c48cb79435facd0969c5a60a587a458e2d16f9752771027efbec

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_CPE_ID:=cpe:/a:sgi:xfsprogs

PKG_BUILD_DIR:=$(BUILD_DIR)/xfsprogs-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/xfsprogs_legacy/default
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Filesystem
  DEPENDS:=+libuuid +libpthread @LINUX_2_6_36
  URL:=https://xfs.org/
endef

define Package/xfs-admin_legacy
$(call Package/xfsprogs_legacy/default)
  TITLE:=Utilities for changing parameters of an XFS filesystems
endef

define Package/xfs-mkfs_legacy
$(call Package/xfsprogs_legacy/default)
  TITLE:=Utility for creating XFS filesystems
endef

define Package/xfs-fsck_legacy
$(call Package/xfsprogs_legacy/default)
  TITLE:=Utilities for checking and repairing XFS filesystems
endef

define Package/xfs-growfs_legacy
$(call Package/xfsprogs_legacy/default)
  TITLE:=Utility for increasing the size of XFS filesystems
endef

CONFIGURE_ARGS += \
	--disable-gettext \
	--disable-blkid \
	--disable-readline \
	--disable-editline \
	--disable-termcap \
	--disable-lib64 \
	--disable-ubisan \
	--disable-addrsan \
	--disable-threadsan \
	--disable-scrub \
	--disable-libicu

TARGET_CFLAGS += -DHAVE_MAP_SYNC
TARGET_CFLAGS += -I$(STAGING_DIR)/opt/include

TARGET_LDFLAGS += -lrt

define Package/xfs-admin_legacy/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/xfs_db $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/xfs_admin $(1)/opt/sbin
endef

define Package/xfs-mkfs_legacy/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/mkfs.xfs $(1)/opt/sbin
endef

define Package/xfs-fsck_legacy/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/xfs_repair $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/xfs_db $(1)/opt/sbin
endef

define Package/xfs-growfs_legacy/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/xfs_growfs $(1)/opt/sbin
endef

$(eval $(call BuildPackage,xfs-admin_legacy))
$(eval $(call BuildPackage,xfs-mkfs_legacy))
$(eval $(call BuildPackage,xfs-fsck_legacy))
$(eval $(call BuildPackage,xfs-growfs_legacy))
