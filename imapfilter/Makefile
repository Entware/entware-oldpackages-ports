#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=imapfilter
PKG_VERSION:=2.7.6
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/lefcha/imapfilter/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=e9063ca210cefe6c47771b400c9f3620bd7a5dce2dfd4d46aeaa86f4cac1d87d

include $(INCLUDE_DIR)/package.mk

define Package/imapfilter
  SECTION:=mail
  CATEGORY:=Mail
  DEPENDS:=+liblua +libopenssl +libpcre2
  TITLE:=IMAP server based email filtering
  URL:=http://github.com/lefcha/imapfilter
endef

define Package/imapfilter/description
	IMAPFilter is a mail filtering utility. It connects to remote mail
	servers using the Internet Message Access Protocol (IMAP), sends
	searching queries to the server and processes mailboxes based on the
	results. It can be used to delete, copy, move, flag, etc. messages
	residing in mailboxes at the same or different mail servers. The 4rev1
	and 4 versions of the IMAP protocol are supported.

	IMAPFilter uses the Lua programming language as a configuration and
	extension language.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
		INCDIRS="$(TARGET_CPPFLAGS)" \
		LIBDIRS="$(TARGET_LDFLAGS)" \
		MYCFLAGS="$(TARGET_CFLAGS) -std=gnu99" \
		PREFIX="/opt" \
		SSLCAPATH="/opt/etc/ssl/certs" \
		SSLCAFILE="/opt/etc/ssl/cert.pem"
endef

define Package/imapfilter/conffiles
/opt/etc/imapfilter/config.lua
/opt/etc/imapfilter/extend.lua
endef

define Package/imapfilter/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/imapfilter $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/etc/imapfilter
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/samples/{config,extend}.lua $(1)/opt/etc/imapfilter
	$(INSTALL_DIR) $(1)/opt/share/imapfilter
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/src/*.lua $(1)/opt/share/imapfilter/
endef

$(eval $(call BuildPackage,imapfilter))
