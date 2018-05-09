#
# Copyright (C) 2009-2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=xtables-addons_legacy
PKG_VERSION:=1.47.1
PKG_RELEASE:=1a
PKG_HASH:=06535dbefaa7725870750048842b4b53f5a4f8d8b16d5ce61bb4cc28e0b99326

PKG_SOURCE:=xtables-addons-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@SF/xtables-addons
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_CHECK_FORMAT_SECURITY:=0
PKG_BUILD_DIR:=$(BUILD_DIR)/xtables-addons-$(PKG_VERSION)

PKG_MAINTAINER:=Jo-Philipp Wich <jow@openwrt.org>

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/xtables-addons_legacy
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Firewall
  DEPENDS:=+iptables
  TITLE:=Extensions not distributed in the main Xtables (1.47.1 legacy version)
  URL:=http://xtables-addons.sourceforge.net/
endef

# uses GNU configure

CONFIGURE_ARGS+= \
	--without-kbuild \
	--with-xtables="$(STAGING_DIR)/opt" \
	--with-xtlibdir="/opt/lib/iptables" \

define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) \
		ARCH="$(LINUX_KARCH)" \
		CROSS_COMPILE="$(TARGET_CROSS)" \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		DEPMOD="/bin/true" \
		all install
endef

define Package/xtables-addons_legacy/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(CP) $(PKG_INSTALL_DIR)/opt/sbin/iptaccount $(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libxt_ACCOUNT_cl.so* $(1)/opt/lib/
	$(INSTALL_DIR) $(1)/opt/lib/iptables
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/iptables/* $(1)/opt/lib/iptables/
	$(INSTALL_DIR) $(1)/opt/lib/xtables-addons/
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/xtables-addons/* $(1)/opt/lib/xtables-addons/
	$(SED) 's,/usr/bin/perl,/opt/bin/perl,g' $(1)/opt/lib/xtables-addons/xt_geoip_build
endef

$(eval $(call BuildPackage,xtables-addons_legacy))
