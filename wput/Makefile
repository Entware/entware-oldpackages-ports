#
# Copyright (C) 2007-2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2008

include $(TOPDIR)/rules.mk

PKG_NAME:=wput
PKG_VERSION:=0.6.2
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=@SF/wput
PKG_HASH:=229d8bb7d045ca1f54d68de23f1bc8016690dc0027a16586712594fbc7fad8c7

include $(INCLUDE_DIR)/package.mk

define Package/wput
  SUBMENU:=File Transfer
  SECTION:=net
  CATEGORY:=Network
  TITLE:=A tiny wget-like ftp-client for uploading files
  URL:=http://wput.sourceforge.net/
endef

define Package/wput/description
 Wput is a tiny ftp-client, that uploads files or directories
 to a remote ftp-server.  Main features are: resuming,
 time-stamping, wget-like interface, proxy-support and
 speed-limit.
endef

CONFIGURE_ARGS += \
	--disable-g-switch \
	--without-ssl \
	--disable-rpath \
	--without-libintl-prefix \

MAKE_FLAGS += \
	CC="$(TARGET_CC) -D_XOPEN_SOURCE=600 $(TARGET_CXXFLAGS) $(TARGET_LDFLAGS)"

define Package/wput/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/wput $(1)/opt/bin
endef

$(eval $(call BuildPackage,wput))
