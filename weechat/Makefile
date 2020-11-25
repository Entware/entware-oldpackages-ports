#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Dependencies checker was turned off here to avoid pulling optional deps

include $(TOPDIR)/rules.mk

PKG_NAME:=weechat
PKG_VERSION:=3.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://weechat.org/files/src
PKG_HASH:=6cb7d25a363b66b835f1b9f29f3580d6f09ac7d38505b46a62c178b618d9f1fb

PKG_BUILD_DEPENDS:=perl python3

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk
include $(INCLUDE_DIR)/nls.mk
include $(TOPDIR)/feeds/packages/lang/perl/perlver.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-version.mk

define Package/weechat
  SUBMENU:=Instant Messaging
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Lightweight IRC client
  URL:=https://weechat.org/
  DEPENDS:= +libcurl +libgnutls +libgcrypt +libaspell +libncursesw \
	$(ICONV_DEPENDS) $(INTL_DEPENDS)
endef

define Package/weechat/description
 Weechat is fast, light & extensible IRC client.
endef

TARGET_LDFLAGS += $(if $(ICONV_FULL),-liconv)
TARGET_LDFLAGS += $(if $(INTL_FULL),-lintl)

CMAKE_OPTIONS += \
	-DWEECHAT_HOME="/opt/var/weechat" \
	-DCA_FILE="/opt/etc/ssl/certs/ca-certificates.crt" \
	-DPYTHON_EXECUTABLE="$(STAGING_DIR_HOSTPKG)/bin/python3" \
	-DPYTHON_INCLUDE_DIRS="$(STAGING_DIR)/opt/include/python$(PYTHON3_VERSION)" \
	-DPYTHON_LIBRARIES="$(STAGING_DIR)/opt/lib/libpython$(PYTHON3_VERSION).so" \
	-DPERL_EXECUTABLE="$(STAGING_DIR_HOSTPKG)/usr/bin/perl" \
	-DPERL_INCLUDE_PATH="$(STAGING_DIR)/opt/lib/perl5/$(PERL_VERSION2)/CORE" \
	-DPERL_LIBRARY="$(STAGING_DIR)/opt/lib/perl5/$(PERL_VERSION2)/CORE/libperl.so" \
	-DENABLE_JAVASCRIPT=OFF \
	-DENABLE_GUILE=OFF \
	-DENABLE_LUA=OFF \
	-DENABLE_PHP=OFF \
	-DENABLE_RUBY=OFF \
	-DENABLE_TCL=OFF

define CheckDependencies
endef

define Package/weechat/install
	$(INSTALL_DIR) $(1)/opt/bin $(1)/opt/var/weechat
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/weechat-curses $(1)/opt/bin
	ln -sf weechat-curses $(1)/opt/bin/weechat
	$(INSTALL_DIR) $(1)/opt/lib/weechat/plugins
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/weechat/plugins/*.so \
		$(1)/opt/lib/weechat/plugins
endef

define Package/weechat/postinst
#!/bin/sh
cat << EOF
Please install optional dependencies first if you want to use weechat scripts.

* for Perl scripts:
opkg install perl

* for Python scripts:
opkg install python3-light
EOF
endef

$(eval $(call BuildPackage,weechat))
