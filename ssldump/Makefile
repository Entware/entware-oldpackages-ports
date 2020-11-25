#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ssldump
PKG_VERSION:=1.2
PKG_RELEASE:=1
PKG_REV:=df9d6f282c5254e82c7a5f94e395027ac4b967d1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/adulau/ssldump.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/ssldump
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libopenssl +libpcap
  TITLE:=a SSLv3/TLS network protocol analyzer
  URL:=http://ssldump.sourceforge.net/
endef

define Package/ssldump/description
 ssldump is an SSLv3/TLS network protocol analyzer. It identifies TCP connections on the chosen network interface
 and attempts to interpret them as SSLv3/TLS traffic. When it identifies SSLv3/TLS traffic, it decodes
 the records and displays them in a textual form to stdout. If provided with the appropriate keying material,
 it will also decrypt the connections and display the application data traffic.
endef

define Package/ssldump/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ssldump $(1)/opt/sbin
endef

$(eval $(call BuildPackage,ssldump))
