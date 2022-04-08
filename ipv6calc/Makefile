#
# Copyright (C) 2008-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ipv6calc
PKG_VERSION:=4.0.1
PKG_REV:=2b882e6cb5f6f9a2ca61f96b37bbb44c40dae2a8
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/pbiering/ipv6calc.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_MIRROR_HASH:=11186ee93ff19eb27ee455fcce7dbe4b47018787535f987f1015eb7f157c5374

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/ipv6calc/Default
  SECTION:=net
  CATEGORY:=Network
  URL:=https://www.deepspace6.net/projects/ipv6calc.html
endef

define Package/ipv6calc/Default/description
  ipv6calc is a small utility written in programming languate C to manipulate
  (not only) IPv6 addresses. Intentions were convering a given IPv6 address
  into compressed format, convering a given IPv6 address into the same format
  like shown in /proc/net/if_inet6 and (because it was not difficulty)
  migrating the Perl program ip6_int into. Now only one utiltity is needed to
  do a lot.
endef

define Package/ipv6calc
  $(call Package/ipv6calc/Default)
  TITLE:=IPv6 addresses calculations
endef

define Package/ipv6calc/description
  $(call Package/ipv6calc/Default/description)
  This package contains an ipv6calc with the internal databases enabled.
endef

define Package/ipv6log
  $(call Package/ipv6calc/Default)
  TITLE:=Webserver log helper programs
endef

define Package/ipv6log/description
  $(call Package/ipv6calc/Default/description)
  This package contains webserver log anonymization, conversion, and statistics
  helper programs with the internal databases enabled.
endef

CONFIGURE_ARGS += \
	--disable-compiler-warning-to-error \
	--with-dbip-db=/opt/share/DBIP \
	--with-external-db=/opt/share/ipv6calc/db \
	--with-ip2location-db=/opt/share/IP2Location \
	--with-geoip-db=/opt/share/GeoIP \
	--enable-bundled-md5 \
	--enable-bundled-getopt

define Package/ipv6calc/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/ipv6calc $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/share/{ipv6calc/db,GeoIP,IP2Location,DBIP}
endef

define Package/ipv6log/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/ipv6log* $(1)/opt/bin
endef

$(eval $(call BuildPackage,ipv6calc))
$(eval $(call BuildPackage,ipv6log))
