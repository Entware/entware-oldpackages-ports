#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=weechat
PKG_VERSION:=1.3
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://www.weechat.org/files/src
PKG_MD5SUM:=d315ceb66b03442ded0715f4277bd65f

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/weechat/default
  SUBMENU:=Instant Messaging
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Lightweight IRC client
  URL:=http://www.weechat.org/
endef

define Package/weechat
    $(call Package/weechat/default)
    DEPENDS:=+libcurl +libgnutls +libgcrypt +libncursesw $(ICONV_DEPENDS) $(INTL_DEPENDS)
endef

define Package/weechat-plugin-aspell
    $(call Package/weechat/default)
    DEPENDS:=+weechat +libaspell
endef

define Package/weechat-plugin-perl
    $(call Package/weechat/default)
    DEPENDS:=+weechat +perl
endef

define Package/weechat-plugin-python
    $(call Package/weechat/default)
    DEPENDS:=+weechat +python-light
endef


define Package/weechat/default/description
 Weechat is fast, light & extensible IRC client.
endef

define Package/weechat/description
 $(call Package/weechat/default/description)
 Weechat and basic plugins.
endef

define Package/weechat-plugin-apsell/description
 $(call Package/weechat/default/description)
 Aspell plugin.
endef

define Package/weechat-plugin-perl/description
 $(call Package/weechat/default/description)
 Perl plugin.
endef

define Package/weechat-plugin-python/description
 $(call Package/weechat/default/description)
 Python plugin.
endef

TARGET_LDFLAGS += \
	-lintl

CMAKE_OPTIONS+= \
	-DWEECHAT_HOME="/opt/var/weechat" \
	-DCA_FILE="/opt/etc/ssl/certs/ca-certificates.crt" \
	-DPYTHON_EXECUTABLE="$(STAGING_DIR)/host/bin/python2.7" \
	-DPYTHON_INCLUDE_PATH="$(STAGING_DIR)/opt/include/python2.7" \
	-DPYTHON_LIBRARY="$(STAGING_DIR)/opt/lib/libpython2.7.so" \
	-DPERL_EXECUTABLE:FILEPATH="$(STAGING_DIR)/host/bin/perl" \
	-DPERL_INCLUDE_PATH="$(STAGING_DIR)/opt/lib/perl5/5.22/CORE" \
	-DPERL_LIBRARY="$(STAGING_DIR)/opt/lib/perl5/5.22/CORE/libperl.so" \
	-DENABLE_JAVASCRIPT=OFF \
	-DENABLE_LUA=OFF \
	-DENABLE_GUILE=OFF \
	-DENABLE_RUBY=OFF \
	-DENABLE_TCL=OFF

define Package/weechat/install
	$(INSTALL_DIR) $(1)/opt/bin $(1)/opt/var/weechat
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/weechat-curses $(1)/opt/bin
	ln -sf weechat-curses $(1)/opt/bin/weechat
	$(INSTALL_DIR) $(1)/opt/lib/weechat/plugins
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/lib/weechat/plugins/{alias,exec,fifo,irc,logger,relay,script,trigger,xfer}.so \
		$(1)/opt/lib/weechat/plugins
endef

define Package/weechat-plugin-aspell/install
	$(INSTALL_DIR) $(1)/opt/lib/weechat/plugins
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/lib/weechat/plugins/aspell.so \
		$(1)/opt/lib/weechat/plugins
endef

define Package/weechat-plugin-perl/install
	$(INSTALL_DIR) $(1)/opt/lib/weechat/plugins
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/lib/weechat/plugins/perl.so \
		$(1)/opt/lib/weechat/plugins
endef

define Package/weechat-plugin-python/install
	$(INSTALL_DIR) $(1)/opt/lib/weechat/plugins
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/lib/weechat/plugins/python.so \
		$(1)/opt/lib/weechat/plugins
endef

$(eval $(call BuildPackage,weechat))
$(eval $(call BuildPackage,weechat-plugin-aspell))
$(eval $(call BuildPackage,weechat-plugin-perl))
$(eval $(call BuildPackage,weechat-plugin-python))
