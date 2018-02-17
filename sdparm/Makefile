#
# Copyright (C) 2007-2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=sdparm
PKG_VERSION:=1.10
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=http://sg.danny.cz/sg/p
PKG_HASH:=1ea1ed1bb1ee2aef62392618fa42da9ed027d5e655f174525c39235778292ab3

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/sdparm
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Read or modify SCSI or USB disk parameters
  SUBMENU:=Disc
  URL:=http://sg.danny.cz/sg/sdparm.html
endef

define Package/sdparm/description
 The sdparm utility outputs and in some cases modifies SCSI device parameters.
endef

define Package/sdparm/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/$(PKG_NAME) $(1)/opt/bin
endef

$(eval $(call BuildPackage,sdparm))
