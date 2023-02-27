#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=elinks
PKG_VERSION:=0.16.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=5b51f9621cce6f2a20a06c608bf308384ea4eb83
PKG_SOURCE_URL:=https://github.com/rkd77/elinks.git
PKG_MIRROR_HASH:=1b0aab027cfd31fc6a4316cd36a2fc058d2cf20e1f789f617f13d674f663e40b

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include $(INCLUDE_DIR)/meson.mk

define Package/elinks
	SECTION:=net
	CATEGORY:=Network
	DEPENDS:=+ca-bundle +libevent2 +libexpat +libidn +libncursesw +libopenssl +libzstd +zlib $(ICONV_DEPENDS)
	TITLE:=A text based web browser
	URL:=http://elinks.or.cz/
endef

define Package/elinks/description
 An advanced text based web browser.
endef

MESON_ARGS += \
	-Dbacktrace=false \
	-Dfsp=false \
	-Dgpm=false \
	-Dlibevent=true \
	-Dsmall=true \
	-Dterminfo=true \
	-Dtre=false \
	-Dxterm=true \
	-Dzstd=true

TARGET_LDFLAGS += $(if $(ICONV_FULL),-liconv)

define Package/elinks/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/elinks $(1)/opt/bin
endef

$(eval $(call BuildPackage,elinks))
