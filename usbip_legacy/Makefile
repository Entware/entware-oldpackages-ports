#
# Copyright (C) 2010-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# This is the last version, working on kernel 2.6.22

include $(TOPDIR)/rules.mk

PKG_NAME:=usbip_legacy
PKG_VERSION:=0.1.7
PKG_RELEASE:=4

PKG_SOURCE:=usbip-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/usbip
PKG_HASH:=a2dfd3b8c6a3a0c72ddf0cf3f01ed20b4ed9eb97c3a859542b6932ee44deb628

PKG_BUILD_DIR:=$(BUILD_DIR)/usbip-$(PKG_VERSION)

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

PKG_BUILD_DEPENDS:=glib2 sysfsutils

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/usbip_legacy/Common
  TITLE:=USB-over-IP
  URL:=http://usbip_legacy.sourceforge.net/
  MAINTAINER:=Nuno Goncalves <nunojpg@gmail.com>
  DEPENDS += @LINUX_2_6_36
endef

define Package/usbip_legacy/Default
$(call Package/usbip_legacy/Common)
  SECTION:=net
  CATEGORY:=Network
endef

define Package/usbip_legacy
$(call Package/usbip_legacy/Default)
  TITLE+= (common)
  DEPENDS+= +libsysfs +libwrap +usbids
endef

define Package/usbip_legacy-client
$(call Package/usbip_legacy/Default)
  TITLE+= (client)
  DEPENDS+= usbip_legacy +glib2
endef

define Package/usbip_legacy-server
$(call Package/usbip_legacy/Default)
  TITLE+= (server)
  DEPENDS+= usbip_legacy +glib2
endef

CONFIGURE_PATH:= src
MAKE_PATH:= src
LIBTOOL_PATHS:= src

CONFIGURE_ARGS += \
	CFLAGS="$(TARGET_CFLAGS)" \
	CPPFLAGS="$(TARGET_CPPFLAGS)"

define Package/usbip_legacy/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libusbip.so.* $(1)/opt/lib/
endef

define Package/usbip_legacy-client/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/usbip $(1)/opt/bin/
endef

define Package/usbip_legacy-server/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/usbipd $(1)/opt/bin/
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/bind_driver $(1)/opt/bin/usbip_bind_driver
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(CP) ./files/S74usbipd $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,usbip_legacy))
$(eval $(call BuildPackage,usbip_legacy-client))
$(eval $(call BuildPackage,usbip_legacy-server))
