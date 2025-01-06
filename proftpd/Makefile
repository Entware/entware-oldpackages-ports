#
# Copyright (C) 2009-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=proftpd
PKG_VERSION:=1.3.8b
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/proftpd/proftpd/tar.gz/refs/tags/v$(PKG_VERSION)?
PKG_HASH:=183ab7c6107de271a2959ff268f55c9b6c76b2cf0029e6584fccc019686601e0

PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/proftpd
  SUBMENU:=File Transfer
  SECTION:=net
  CATEGORY:=Network
  TITLE:=ProFTPD FTP server
  URL:=http://www.proftpd.org/
  MAINTAINER:=Cezary Jackiewicz <cezary@eko.one.pl>
  DEPENDS:=+libattr +libidn +libidn2 +libncursesw +libopenssl +libsodium \
	$(ICONV_DEPENDS) $(INTL_DEPENDS)
endef

define Package/proftpd/conffiles
/opt/etc/proftpd.conf
endef

MAKE_FLAGS += \
	INSTALL_USER=$(shell id -u) \
	INSTALL_GROUP=$(shell id -g)

CONFIGURE_ARGS += \
	--disable-cap \
	--disable-auth-pam \
	--disable-strip \
	--with-lastlog=/opt/var/log \
	--enable-nls \
	--enable-openssl \
	--with-modules=mod_digest:mod_sftp

define Package/proftpd/install
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/proftpd.conf $(1)/opt/etc
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/ftp{count,dctl,top,who} $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/{ftpscrub,ftpshut,proftpd} $(1)/opt/sbin
	$(LN) proftpd $(1)/opt/sbin/in.proftpd
	$(INSTALL_BIN) ./files/S66proftpd $(1)/opt/etc/init.d
	$(INSTALL_DIR) $(1)/opt/var/run/proftpd
endef

$(eval $(call BuildPackage,proftpd))
