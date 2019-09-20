#
# Copyright (C) 2006-2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=openswan
PKG_VERSION:=2.6.51.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.openswan.org/download
PKG_HASH:=4124f4ce970089f301c34b9c48f54b021cf6b2b8813877942337f8022104f70d

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/openswan
  SUBMENU:=VPN
  SECTION:=net
  CATEGORY:=Network
  TITLE+= Openswan (daemon)
  DEPENDS+= +libgmp
  URL:=http://www.openswan.org/
endef

define Package/openswan/description
 Openswan is an IPsec implementation for Linux.
 This package contains the Openswan user-land daemon.
endef

OPENSWAN_MAKEFLAGS:= \
	-C $(PKG_BUILD_DIR) \
	$(TARGET_CONFIGURE_OPTS) \
	ARCH=$(CONFIG_ARCH) \
	USERCOMPILE="$(TARGET_CFLAGS) -I$(PKG_BUILD_DIR)/ports/linux/include -I$(PKG_BUILD_DIR)/linux/include -I$(PKG_BUILD_DIR)/include $(TARGET_CPPFLAGS) $(TARGET_LDFLAGS)" \
	USERLINK="$(TARGET_LDFLAGS)" \
	IPSECDIR="/opt/etc/ipsec.d" \
	INC_USRLOCAL="/opt" \
	FINALCONFDIR="/opt/etc" \
	INC_RCDEFAULT="/opt/etc/init.d" \
	MODPROBE="/sbin/insmod" \
	FINALCONFFILE="/opt/etc/ipsec.conf" \
	FINALVARDIR="/opt/var" \
	DESTDIR="$(PKG_INSTALL_DIR)"

define Build/Compile
	+$(MAKE) $(PKG_JOBS) $(OPENSWAN_MAKEFLAGS) programs
endef

define Build/Install
	$(MAKE) $(OPENSWAN_MAKEFLAGS) install
endef

define Package/openswan/conffiles
/opt/etc/ipsec.conf
/opt/etc/ipsec.conf
/opt/etc/ipsec.d/policies/private
/opt/etc/ipsec.d/policies/clear
/opt/etc/ipsec.d/policies/private-or-clear
/opt/etc/ipsec.d/policies/block
/opt/etc/ipsec.d/policies/clear-or-private
endef

define Package/openswan/install
	$(CP) $(PKG_INSTALL_DIR)/opt $(1)
	$(RM) -rf \
	    $(1)/opt/etc/init.d \
	    $(1)/opt/etc/ipsec.d/examples \
	    $(1)/opt/libexec/ipsec/setup \
	    $(1)/opt/man \
	    $(1)/opt/share
endef

$(eval $(call BuildPackage,openswan))
