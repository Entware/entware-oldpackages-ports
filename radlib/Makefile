#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Used by wview only

include $(TOPDIR)/rules.mk

PKG_NAME:=radlib
PKG_VERSION:=2.12.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/radlib
PKG_HASH:=82b98bb5e08a500dea1e4252843b9c772fa1fb67ac8ab89ed64abdd5e22eca66

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

PKG_CONFIG_DEPENDS := \
	CONFIG_RADLIB_SQLITE

include $(INCLUDE_DIR)/package.mk

define Package/radlib
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+RADLIB_SQLITE:libsqlite3
  TITLE:=Rapid Application Development Library
  URL:=http://www.radlib.teel.ws/
endef

define Package/radlib/description
  radlib is a rapid application development library for unix multi-process applications.
endef

define Package/radlib/config
choice
	prompt "sqlite support"
	default RADLIB_SQLITE

	config RADLIB_NONE
		bool "None"

	config RADLIB_SQLITE
		bool "sqlite"
endchoice
endef

CONFIGURE_ARGS += \
	--enable-sqlite=$(if $(CONFIG_RADLIB_SQLITE),yes,no) \
	CPPFLAGS="$(TARGET_CPPFLAGS)" \
	LDFLAGS="$(TARGET_LDFLAGS)"

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/*.h $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/librad.{a,so*} $(1)/opt/lib/
endef

define Package/radlib/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/radmrouted $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/librad.so.* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,radlib))
