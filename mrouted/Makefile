#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mrouted
PKG_VERSION:=4.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/troglobit/mrouted/tar.gz/$(PKG_VERSION)?
PKG_HASH:=0c8fa7e871c9d31b3a5739705e22ba6f54e2ac9c0817bc6e66640c9d2e10c095

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/mrouted
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Routing and Redirection
  TITLE:=multicast routing daemon
  URL:=https://github.com/troglobit/mrouted
endef

define Package/mrouted/description
 routed is a 3-clause BSD licensed implementation of the DVMRP multicast
 routing protocol. It can run on any UNIX based system, from embedded Linux
 systems to workstations, turning them into multicast routers with tunnel
 support, which can be used to cross non-multicast-aware routers.
endef

define Package/mrouted/conffiles
/opt/etc/mrouted.conf
endef

define Package/mrouted/install
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/mrouted.conf $(1)/opt/etc
	$(INSTALL_BIN) ./files/S69mrouted $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/{map-mbone,mrinfo,mroutectl,mrouted,mtrace} \
		$(1)/opt/sbin
endef

$(eval $(call BuildPackage,mrouted))
