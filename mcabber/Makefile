#
# Copyright (C) 2011-2016 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mcabber
PKG_VERSION:=1.1.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://mcabber.com/files
PKG_HASH:=d789ceb33eaa78967c172241e941d43f91300ee0235a33f826f3df6f1163f959

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/mcabber
  SUBMENU:=Instant Messaging
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libncursesw +loudmouth +libcharset +libidn +libgpgme +libotr
  TITLE:=Jabber console client
  URL:=http://mcabber.com
  MAINTAINER:=Peter Wagner <tripolar@gmx.at>
endef

define Package/mcabber/description
  mcabber is a small Jabber console client.
  mcabber includes features such as SASL/SSL/TLS support, MUC (Multi-User Chat) support,
  history logging, command completion, OpenPGP encryption, OTR (Off-the-Record
  Messaging) support, dynamic modules and external action triggers.
endef

CONFIGURE_ARGS += \
	--with-libidn=$(STAGING_DIR)/opt/lib \
	--with-gpgme-prefix=$(STAGING_DIR)/opt \
	--enable-otr \
	--disable-hgcset

define Package/mcabber/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/mcabber $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib/mcabber
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/lib/mcabber/*.so $(1)/opt/lib/mcabber
	$(INSTALL_DIR) $(1)/opt/share/mcabber/help
	$(CP) $(PKG_INSTALL_DIR)/opt/share/mcabber/help/en $(1)/opt/share/mcabber/help
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/mcabberrc.example $(1)/opt/share/mcabber
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/contrib/events/eventcmd $(1)/opt/share/mcabber/eventcmd.example
endef

$(eval $(call BuildPackage,mcabber))
