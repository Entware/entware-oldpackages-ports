#
# Copyright (C) 2009-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=btpd
PKG_VERSION:=0.16-20200407
PKG_REV:=a3a10dfe1ece4a726530353a7b208c0cb4ff7e0d
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/btpd/btpd.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_MIRROR_HASH:=9d959e064702da01211eff519115fcafa199e8b374ce5dbdf2b7e6fae7ff462a

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/btpd
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libpthread +librt
  SUBMENU:=BitTorrent
  TITLE:=btpd - BitTorrent Protocol Daemon
  URL:=https://github.com/btpd/btpd/wiki/
endef

define Package/btpd/description
	BTPD is a bittorrent client consisting of a daemon and client commands,
	which can be used to read and/or manipulate the daemon state.
	The daemon is capable of running several torrents simultaneously and
	only uses one tcp port.
	It's fairly low on resource usage and should be perfect for file
	distribution sites.
	Efficient downloads and ease of use makes this client a good choice for
	the casual user as well.
endef

define Package/btpd/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/bt{cli,info,pd} $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S93btpd $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,btpd))
