#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ssldump
PKG_VERSION:=1.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/adulau/ssldump/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=10540233ebf4af3fe276ae4adce3f9ac6f7d795731268862d6da4151e6e1fda9

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/ssldump
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libjson-c +libnet-1.2.x +libopenssl +libpcap
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
