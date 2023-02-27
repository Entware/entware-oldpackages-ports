#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=eggdrop
PKG_VERSION:=1.9.4
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=e01fd930e5004b9d44b9e2f68403273edd984612
PKG_SOURCE_URL:=https://github.com/eggheads/eggdrop.git
PKG_MIRROR_HASH:=afaba4ba553b1991a870f5db5d7604017c3812734f4fc074ceeb8b61c55038d1

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
