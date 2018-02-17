#
# Copyright (C) 2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 1996

include $(TOPDIR)/rules.mk

PKG_NAME:=time
PKG_VERSION:=1.7
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@GNU/time
PKG_HASH:=e37ea79a253bf85a85ada2f7c632c14e481a5fd262a362f6f4fd58e68601496d

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/time
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=The GNU time utility
  URL:=http://www.gnu.org/software/time/
endef

define Package/time/description
  `time' is a program that measures many of the CPU resources, such as time and
  memory, that other programs use.  The GNU version can format the output in
  arbitrary ways by using a printf-style format string to include various
  resource measurements.  Some systems do not provide much information about
  program resource use; `time' reports unavailable information as zero values.
endef

define Package/time/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/time $(1)/opt/bin
endef

$(eval $(call BuildPackage,time))
