#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2006

include $(TOPDIR)/rules.mk

PKG_NAME:=arpwatch
PKG_VERSION:=2.1a15
PKG_RELEASE:=4

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=ftp://ftp.free.fr/.mirrors1/ftp.gentoo.org/distfiles/
PKG_MD5SUM:=cebfeb99c4a7c2a6cee2564770415fe7

# use a subdirectory to prevent configure for finding libpcap build dir
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/arpwatch
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libpcap
  TITLE:=Ethernet station activity monitor
  URL:=http://www-nrg.ee.lbl.gov/
endef

define Package/arpwatch/description
	Ethernet monitor program for keeping track of ethernet/ip address
	pairings.
endef

CONFIGURE_VARS += \
	ac_cv_path_V_SENDMAIL="/opt/sbin/sendmail"

MAKE_FLAGS += \
	CCOPT="$(TARGET_CFLAGS)" \
	INCLS="-I. $(TARGET_CPPFLAGS)"

define Package/arpwatch/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/arp{watch,snmp} $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/{lib,share}/arpwatch
	$(CP) $(PKG_BUILD_DIR)/ethercodes.dat $(1)/opt/share/arpwatch
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S04arpwatch $(1)/opt/etc/init.d
endef

$(eval $(call BuildPackage,arpwatch))
