#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Used by rrdtool only, no reason to update.

include $(TOPDIR)/rules.mk

PKG_NAME:=cgilib
PKG_VERSION:=0.7
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.infodrom.org/projects/cgilib/download
PKG_HASH:=09b7d71bd1eea10bb404cd665fd5abe69282144ce01d96f2863c85fd42d5d692

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/cgilib
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Simple CGI Library
  URL:=http://www.infodrom.org/projects/cgilib/
endef

TARGET_CFLAGS += $(FPIC)

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/cgi.h $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcgi.{a,so*} $(1)/opt/lib/
endef

define Package/cgilib/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcgi.so.* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,cgilib))
