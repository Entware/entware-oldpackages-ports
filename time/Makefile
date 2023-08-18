#
# Copyright (C) 2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=time
PKG_VERSION:=1.9
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@GNU/time
PKG_HASH:=fbacf0c81e62429df3e33bda4cee38756604f18e01d977338e23306a3e3b521e

include $(INCLUDE_DIR)/package.mk

define Package/time
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=The GNU time utility
  URL:=http://www.gnu.org/software/time/
  ALTERNATIVES:=300:/opt/bin/time:/opt/libexec/time-gnu
endef

define Package/time/description
  "time" is a program that measures many of the CPU resources, such as time and
  memory, that other programs use.  The GNU version can format the output in
  arbitrary ways by using a printf-style format string to include various
  resource measurements.  Some systems do not provide much information about
  program resource use; "time" reports unavailable information as zero values.
endef

define Package/time/install
	$(INSTALL_DIR) $(1)/opt/libexec
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/time $(1)/opt/libexec/time-gnu
endef

$(eval $(call BuildPackage,time))
