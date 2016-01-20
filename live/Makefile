#
# Copyright (C) 2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=live
PKG_VERSION:=2016.01.16
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME).$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.live555.com/liveMedia/public
PKG_MD5SUM:=6686bc1d28f9d708539805439ccc96fb

include $(INCLUDE_DIR)/package.mk

PKG_UNPACK:=gzip -dc $(DL_DIR)/$(PKG_SOURCE) | $(TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xf -

define Package/openrtsp
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=live555 a command-line RTSP client
  URL:=http://www.live555.com/
  DEPENDS:=+libstdcpp
endef

define Build/Configure
	( cd $(PKG_BUILD_DIR); \
	    $(SED) 's/@CROSS_COMPILE@/$(TARGET_CROSS)/g' \
	    -e 's/@CFLAGS@/$(TARGET_CFLAGS)/g' \
	    config.OpenWrt; \
	./genMakefiles OpenWrt; \
	)
endef

define Package/openrtsp/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/testProgs/openRTSP $(1)/opt/bin
endef

$(eval $(call BuildPackage,openrtsp))
