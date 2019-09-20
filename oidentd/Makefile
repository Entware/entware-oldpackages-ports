#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=oidentd
PKG_VERSION:=2.4.0
PKG_REV:=87181589cb1700a427a0c3b8e440acd39dd33dd7
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/janikrabe/oidentd.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/oidentd
	SECTION:=net
	CATEGORY:=Network
	DEPENDS:=+libnetfilter-conntrack
	TITLE:=Identd server
	URL:=https://github.com/janikrabe/oidentd
endef

define Package/oidentd/description
 A nat aware identd server that will correctly forwared requests to clients.
endef

define Package/oidentd/conffiles
/opt/etc/oidentd.conf
/opt/etc/oidentd_masq.conf
endef

define Package/oidentd/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/oidentd $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/oidentd*.conf $(1)/opt/etc
	$(INSTALL_BIN) ./files/S39oidentd $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,oidentd))
