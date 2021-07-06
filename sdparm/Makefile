#
# Copyright (C) 2007-2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# 1.12 requires never kernel (?) with NVME susbsystem
# sg_pt_linux_nvme.c:1913:9: error: 'vb' undeclared (first use in this function)

include $(TOPDIR)/rules.mk

PKG_NAME:=sdparm
PKG_VERSION:=1.11
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=http://sg.danny.cz/sg/p
PKG_HASH:=432fdbfe90f0c51640291faf7602489b0ae56dfb96d0c02ed02308792adc7fb0

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/sdparm
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Disc
  TITLE:=Read or modify SCSI or USB disk parameters
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
