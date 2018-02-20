#
# Copyright (C) 2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=6relayd
PKG_VERSION:=2013-12-10.1
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/sbyx/6relayd.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=0381cf15e9721054f902354e9c3b9fb0201bab7f

PKG_MAINTAINER:=Steven Barth <steven@midlink.org>

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/6relayd
  SECTION:=net
  CATEGORY:=Network
  TITLE:=DHCPv6(-PD)/RA Server & Relay
endef

define Package/6relayd/description
 6relayd is a daemon for serving and relaying IPv6 management protocols to
 configure clients and downstream routers.

 6relayd provides server services for RA, stateless DHCPv6, DHCPv6-PD and can
 be used to relay RA, DHCPv6 and NDP between routed (non-bridged) interfaces
 in case no delegated prefixes are provided by the upstream router.
endef

define Package/6relayd/install
	$(INSTALL_DIR) $(1)/opt/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/6relayd $(1)/opt/sbin/
endef

$(eval $(call BuildPackage,6relayd))
