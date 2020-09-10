#
# Copyright (C) 2006-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# The newer versions includes copy of kernel headers in separate uapi folder,
# which is incompatible with our current k2.6 toolchain

include $(TOPDIR)/rules.mk

PKG_NAME:=ethtool_legacy
PKG_VERSION:=5.4
PKG_RELEASE:=1

PKG_MAINTAINER:=Felix Fietkau <nbd@nbd.name>
PKG_SOURCE:=ethtool-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@KERNEL/software/network/ethtool_legacy
PKG_HASH:=22f81e4927d6eb6a13a259d705248a96005fce2005e15257f639f5a1c8c52b6b

PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_CONFIG_DEPENDS:=CONFIG_ethtool_legacy_PRETTY_DUMP

PKG_BUILD_DIR:=$(BUILD_DIR)/ethtool-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/ethtool_legacy
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=@LINUX_2_6_36
  TITLE:=Display or change ethernet card settings
  URL:=http://www.kernel.org/pub/software/network/ethtool_legacy/
endef

define Package/ethtool_legacy/description
 ethtool_legacy is a small utility for examining and tuning your ethernet-based
 network interface
endef

define Package/ethtool_legacy/config
	config ethtool_legacy_PRETTY_DUMP
		depends on PACKAGE_ethtool_legacy
		bool "Enable pretty printing"
endef

ifeq ($(CONFIG_ethtool_legacy_PRETTY_DUMP),y)
CONFIGURE_ARGS += --enable-pretty-dump
else
CONFIGURE_ARGS += --disable-pretty-dump
endif

define Package/ethtool_legacy/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ethtool $(1)/opt/sbin
endef

$(eval $(call BuildPackage,ethtool_legacy))
