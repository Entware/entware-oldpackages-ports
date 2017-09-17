#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=eggdrop
PKG_VERSION:=1.8.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://ftp.eggheads.org/pub/eggdrop/source/1.8
PKG_HASH:=c4f836c8423b4d1e8fa0d85a4a3f9245d35509d7385a9e22697a4f400d0296af

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/eggdrop
	SECTION:=lang
	CATEGORY:=Languages
	TITLE:=EggDrop IRC BOT
	DEPENDS:=+tcl +libopenssl +libpthread
	URL:=http://www.eggheads.org
endef

define Package/eggdrop/description
 EggDrop IRC BOT
endef

CONFIGURE_ARGS += \
	--prefix="$(PKG_INSTALL_DIR)/opt/eggdrop" \
	--with-tcllib="$(STAGING_DIR)/opt/lib/libtcl8.5.so" \
	--with-tclinc="$(STAGING_DIR)/opt/include/tcl.h"

define Build/Compile
	$(MAKE) config -C $(PKG_BUILD_DIR)
	$(call Build/Compile/Default)
endef

define Build/Install
	$(call Build/Install/Default)
	rm -Rvf $(PKG_INSTALL_DIR)/opt/eggdrop/doc
endef

define Package/eggdrop/install
	$(INSTALL_DIR) $(1)/opt/eggdrop
	$(CP) $(PKG_INSTALL_DIR)/opt/eggdrop/* $(1)/opt/eggdrop
endef

$(eval $(call BuildPackage,eggdrop))
