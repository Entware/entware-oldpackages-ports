#
# Copyright (C) 2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=dstat
PKG_VERSION:=0.7.3
PKG_REV:=b24547b52ecc7d3a699c50e9ebd45fb36395fbc2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_MIRROR_HASH:=7b96cc03b9e274509e6448d4a6ffa0bed1bf4444f0428a0226a2ab34817d6eb9
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/dagwieers/dstat.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

define Package/dstat
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Versatile resource statistics tool
  URL:=http://dag.wieers.com/home-made/dstat/
  DEPENDS:=+python
endef

define Package/dstat/description
  Dstat is a versatile replacement for vmstat, iostat, netstat
  and ifstat. Dstat overcomes some of their limitations and
  adds some extra features, more counters and flexibility.
  Dstat is handy for monitoring systems during performance
  tuning tests, benchmarks or troubleshooting.
endef

define Build/Compile
endef

define Package/dstat/install
	$(INSTALL_DIR) $(1)/opt/share/dstat
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dstat $(1)/opt/share/dstat/dstat.py
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/plugins/dstat_*.py $(1)/opt/share/dstat/
	$(INSTALL_DIR) $(1)/opt/bin
	$(LN) -sf ../share/dstat/dstat.py $(1)/opt/bin/dstat
endef

$(eval $(call BuildPackage,dstat))
