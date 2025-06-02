#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=eggdrop
PKG_VERSION:=1.10.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/eggheads/eggdrop
PKG_MIRROR_HASH:=541cb2c525cdac9a75f92ec680005c0e81752ce3065dfa31b2947c8aacff654d

PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_AUTOMAKE_PATHS:=. src/mod/compress.mod src/mod/dns.mod src/mod/python.mod

PKG_REMOVE_FILES:= \
	src/mod/compress.mod/configure \
	src/mod/dns.mod/configure \
	src/mod/python.mod/configure

include $(INCLUDE_DIR)/package.mk

define Package/eggdrop
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Instant Messaging
  TITLE:=IRC Bot
  URL:=https://www.eggheads.org/
  DEPENDS:=+libopenssl +tcl
endef

define Package/eggdrop/description
  Eggdrop is the oldest Internet Relay Chat (IRC) bot still in active
  development.
endef

CONFIGURE_ARGS += \
	--prefix="$(PKG_INSTALL_DIR)/opt/eggdrop" \
	--with-python-config='' \
	--with-sslinc="$(STAGING_DIR)/opt/include" \
	--with-ssllib="$(STAGING_DIR)/opt/lib" \
	--with-tcl="$(STAGING_DIR)/opt/lib"

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
