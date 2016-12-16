#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2011

include $(TOPDIR)/rules.mk

PKG_NAME:=unfs3
PKG_VERSION:=0.9.23
PKG_REV:=632f7797f8af69ad3d4bdc53b0d1918ed08f702b
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/allspace/eunfs3.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

PKG_FIXUP:=autoreconf
PKG_BUILD_PARALLEL:=0

include $(INCLUDE_DIR)/package.mk

define Package/unfs3
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Filesystem
  DEPENDS:=+portmap +libacl
  TITLE:=User-space NFSv3 Server
  URL:=http://unfs3.sourceforge.net/
endef

CONFIGURE_ARGS += \
	--without-afp-prefix

define Package/unfs3/description
	UNFS3 is a user-space implementation of the NFSv3 server
	specification. It provides a daemon for the MOUNT and NFS
	protocols, which are used by NFS clients for accessing files
	on the server.
endef

define Package/unfs3/install
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S56unfsd $(1)/opt/etc/init.d
	$(INSTALL_DATA) ./files/$(PKG_NAME).exports $(1)/opt/etc/exports
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/unfsd $(1)/opt/sbin
endef

define Package/unfs3/conffiles
/opt/etc/exports
endef

$(eval $(call BuildPackage,unfs3))
