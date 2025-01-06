#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=fetchmail
PKG_VERSION:=6.5.2
PKG_RELEASE:=1

PKG_VERSION_TAG:=$(subst $(space),.,$(wordlist 1,2,$(subst .,$(space),$(PKG_VERSION))))

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@SF/$(PKG_NAME)/branch_$(PKG_VERSION_TAG)
PKG_HASH:=8fd0477408620ae382c1d0ef83d8946a95e5be0c2e582dd4ebe55cba513a45fe

PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

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
