#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2007

include $(TOPDIR)/rules.mk

PKG_NAME:=iptraf
PKG_VERSION:=3.0.1
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=ftp://iptraf.seul.org/pub/iptraf/ \
	ftp://the.wiretapped.net/pub/security/network-monitoring/iptraf/
PKG_HASH:=95a069af8c4d22206985f6ce69acc27cfcfef1d58ad6ab8dbb10c698642ac08a

include $(INCLUDE_DIR)/package.mk

define Package/iptraf
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libncurses
  TITLE:=A console-based network monitoring program
  URL:=http://iptraf.seul.org/
endef

define Package/iptraf/description
  IPTraf is a console-based network statistics utility for Linux. It gathers a
  variety of figures such as TCP connection packet and byte counts, interface
  statistics and activity indicators, TCP/UDP traffic breakdowns, and LAN
  station packet and byte counts.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/src \
		$(TARGET_CONFIGURE_OPTS) \
		CFLAGS="$(TARGET_CFLAGS)" \
		DEBUG="" \
		INCLUDEDIR="-I../support $(TARGET_CPPFLAGS)" \
		LDOPTS="$(TARGET_LDFLAGS)" \
		PLATFORM="-DPLATFORM=\\\"Linux/$(ARCH)\\\"" \
		TARGET="/opt/bin" \
		WORKDIR="/opt/var/lib/iptraf" \
		LOGDIR="/opt/var/log/iptraf" \
		all
endef

define Package/iptraf/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/{iptraf,rvnamed} $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/var/{log,lib,run}/iptraf
endef

$(eval $(call BuildPackage,iptraf))
