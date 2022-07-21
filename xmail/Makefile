#
# Copyright (C) 2007-2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2010

include $(TOPDIR)/rules.mk

PKG_NAME:=xmail
PKG_VERSION:=1.27
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.xmailserver.org/
PKG_HASH:=e91341b779ffd3d70af6f00028bcd7f65ae664fedf947a27c42311102a84784e

include $(INCLUDE_DIR)/package.mk

define Package/xmail
	SECTION:=mail
	CATEGORY:=Mail
	DEPENDS:=+libopenssl +libpthread +libstdcpp
	TITLE:=advanced, fast and reliable ESMTP/POP3 mail server
	URL:=http://www.xmailserver.org/
endef

define Package/xmail/description
 XMail is an Internet mail server featuring an SMTP, POP3 and finger server.
 It's incredibly easy to set up and has lots of features including :
 multiple domains, virtual users and spam protection.
endef

define Build/Compile
	CFLAGS="$(TARGET_CFLAGS)" \
	$(MAKE) -C $(PKG_BUILD_DIR) -f Makefile.lnx \
		$(TARGET_CONFIGURE_OPTS) \
		CPPFLAGS="$(TARGET_CPPFLAGS) -Wno-narrowing" \
		LDFLAGS="$(TARGET_LDFLAGS) -lpthread -lssl -ldl -lcrypto" \
		LD="$(TARGET_CXX)" \
		all
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/xmail $(PKG_BUILD_DIR)/MailRoot
	tar -cjf $(PKG_BUILD_DIR)/MailRoot.tar.bz2 -C $(PKG_BUILD_DIR)/MailRoot --exclude bin .
endef

define Package/xmail/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/{CtrlClnt,MkUsers,XMCrypt,XMail,sendmail} $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/MailRoot.tar.bz2 $(1)/opt/etc
endef

$(eval $(call BuildPackage,xmail))
