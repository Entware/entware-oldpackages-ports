#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# 0.17 requires LibCSS

include $(TOPDIR)/rules.mk

PKG_NAME:=elinks
PKG_VERSION:=0.16.1.1
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=c39887cd864782d37a1f9b220d368f0ccd09abba
PKG_SOURCE_URL:=https://github.com/rkd77/elinks.git
PKG_MIRROR_HASH:=0c19dcab7013d2b348c94db63f6d81fac041b278b19c8ea8e752c9de61988730

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
	-Dzstd=true \
	-Dftp=false

TARGET_LDFLAGS += $(if $(ICONV_FULL),-liconv)

define Package/elinks/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/elinks $(1)/opt/bin
endef

$(eval $(call BuildPackage,elinks))
