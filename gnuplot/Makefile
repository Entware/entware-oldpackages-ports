#
# Copyright (C) 2010-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gnuplot
PKG_VERSION:=5.4.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/gnuplot
PKG_HASH:=eb4082f03a399fd1e9e2b380cf7a4f785e77023d8dcc7e17570c1b5570a49c47

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/gnuplot
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libncurses +libstdcpp +libgd +libreadline $(ICONV_DEPENDS)
  TITLE:=A portable command-line driven graphing utility
  URL:=http://sourceforge.net/projects/gnuplot/
endef

define Package/gnuplot/description
  Gnuplot is a portable command-line driven graphing utility for linux, OS/2,
  MS Windows, OSX, VMS, and many other platforms.
endef

CONFIGURE_ARGS += \
	--without-libcerf \
	--without-x \
	--without-row-help \
	--disable-wxwidgets \
	--without-lua \
	--without-cairo \
	--without-qt \
	LIBS="-liconv"

define Package/gnuplot/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/gnuplot $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/* $(1)/opt/share
endef

$(eval $(call BuildPackage,gnuplot))
