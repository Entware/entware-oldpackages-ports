#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=unfs3
PKG_REAL_VERSION:=0.10.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2024-09-23
PKG_SOURCE_VERSION:=e032ed86c9a3b5f3206d994e9ec544b8d0968650
PKG_SOURCE_URL:=https://github.com/unfs3/unfs3
PKG_MIRROR_HASH:=1e1dfc6c63d82233adb79fa96c141bdda3c143148c4312b22161d62fa822c18c

PKG_VERSION:=$(PKG_REAL_VERSION)_git$(subst -,,$(PKG_SOURCE_DATE))~$(call version_abbrev,$(PKG_SOURCE_VERSION))

PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/unfs3
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Filesystem
  TITLE:=User-space NFSv3 Server
  URL:=https://unfs3.github.io/
  DEPENDS:=+libacl +libtirpc +rpcbind
endef

define Package/unfs3/description
  UNFS3 is a user-space implementation of the NFS (Network File System)
  version 3 server specification. It provides a daemon that supports both
  the MOUNT and NFS protocol.
endef

define Package/unfs3/conffiles
/opt/etc/exports
endef

define Package/unfs3/install
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S56unfsd $(1)/opt/etc/init.d
	$(INSTALL_DATA) ./files/unfs3.exports $(1)/opt/etc/exports
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/unfsd $(1)/opt/sbin
endef

$(eval $(call BuildPackage,unfs3))
