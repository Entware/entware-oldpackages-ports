#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ssldump
PKG_VERSION:=1.9
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/adulau/ssldump/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=c81ce58d79b6e6edb8d89822a85471ef51cfa7d63ad812df6f470b5d14ff6e48

PKG_LICENSE:=BSD-4-Clause
PKG_LICENSE_FILES:=COPYING COPYRIGHT

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/ssldump
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libjson-c +libnet-1.2.x +libopenssl +libpcap
  TITLE:=a SSLv3/TLS network protocol analyzer
  URL:=http://adulau.github.io/ssldump/
endef

define Package/ssldump/description
  ssldump is an SSLv3/TLS network protocol analyzer.
  It identifies TCP connections on the chosen network interface and attempts to
  interpret them as SSLv3/TLS traffic. When it identifies SSLv3/TLS traffic, it
  decodes the records and displays them in a textual form to stdout. If provided
  with the appropriate keying material, it will also decrypt the connections and
  display the application data traffic.
endef

define Package/ssldump/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/ssldump $(1)/opt/sbin
endef

$(eval $(call BuildPackage,ssldump))
