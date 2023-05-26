#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=eggdrop
PKG_VERSION:=1.9.5
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=bae93efb6d6d2ee1ee4ce3c1113e4b3b07b8883e
PKG_SOURCE_URL:=https://github.com/eggheads/eggdrop.git
PKG_MIRROR_HASH:=e38e05b0290863cbf0c9d14f25056b8236c8a5680375c4e58cac6602e005808c

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/eggdrop
	SECTION:=lang
	CATEGORY:=Languages
	TITLE:=EggDrop IRC BOT
	DEPENDS:=+tcl +libopenssl
	URL:=http://www.eggheads.org
endef

define Package/eggdrop/description
 EggDrop IRC BOT.
endef

TCL_VERSION:=$(shell grep ^TCL_MAJOR_VERSION ../../packages/lang/tcl/Makefile | cut -d= -f2)

CONFIGURE_ARGS += \
	--prefix="$(PKG_INSTALL_DIR)/opt/eggdrop" \
	--with-tcllib="$(STAGING_DIR)/opt/lib/libtcl$(TCL_VERSION).so" \
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
