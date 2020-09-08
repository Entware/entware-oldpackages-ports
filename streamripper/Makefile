#
# Copyright (C) 2007-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2015

include $(TOPDIR)/rules.mk

PKG_NAME:=streamripper
PKG_VERSION:=1.65.0-alpha-20150804
PKG_REV:=248f771250998e38a2d8212aa43ccc4a516f853b
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/streamripper/streamripper.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk
include $(INCLUDE_DIR)/nls.mk

define Package/streamripper
	SECTION:=multimedia
	CATEGORY:=Multimedia
	DEPENDS:=+libmad +libvorbis +glib2
	TITLE:=streamripper
	URL:=https://github.com/streamripper/streamripper
endef

define Package/streamripper/description
 Streamripper is an Open Source application that lets you record streaming
 mp3 to your hard drive.
endef

TARGET_CFLAGS += -pthread -I$(STAGING_DIR)/opt/include

define Package/streamripper/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/streamripper $(1)/opt/bin
endef

$(eval $(call BuildPackage,streamripper))
