#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=fetchmail
PKG_VERSION:=6.4.19
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@SF/$(PKG_NAME)/branch_6.4
PKG_HASH:=cd8d11a3d103e50caa2ec64bcda6307eb3d0783a4d4dfd88e668b81aaf9d6b5f

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/fetchmail/Default
	SECTION:=mail
	CATEGORY:=Mail
	TITLE:=Remote mail retriever
	MAINTAINER:=Peter Wagner <tripolar@gmx.at>
	URL:=https://www.fetchmail.info/
endef

define Package/fetchmail/Default/description
 Retrieves remote mail via POP/IMAP.
 Very useful in conjunction with mutt.
endef

define Package/fetchmail
	$(call Package/fetchmail/Default)
	DEPENDS+= +libopenssl
	TITLE+= (with SSL support)
	VARIANT:=ssl
endef

define Package/fetchmail/description
	$(call Package/fetchmail/Default/description)
	This package is built with SSL support.
endef

define Package/fetchmail-nossl
	$(call Package/fetchmail/Default)
	TITLE+= (without SSL support)
	VARIANT:=nossl
endef

define Package/fetchmail-nossl/description
	$(call Package/fetchmail/Default/description)
	This package is built without SSL support.
endef

CONFIGURE_ARGS += \
	--enable-fallback=procmail \
	--without-hesiod

ifeq ($(BUILD_VARIANT),ssl)
	CONFIGURE_ARGS += \
		--with-ssl="$(STAGING_DIR)/opt"
endif

ifeq ($(BUILD_VARIANT),nossl)
	CONFIGURE_ARGS += \
		--with-ssl=no
endif

CONFIGURE_VARS += \
	ac_cv_path_procmail=/opt/sbin/procmail

define Package/fetchmail/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/fetchmail $(1)/opt/bin/
endef

Package/fetchmail-nossl/install = $(Package/fetchmail/install)

$(eval $(call BuildPackage,fetchmail))
$(eval $(call BuildPackage,fetchmail-nossl))
