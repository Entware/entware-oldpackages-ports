#
# Copyright (C) 2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=livemedia
PKG_VERSION:=2022.02.07
PKG_RELEASE:=1

PKG_SOURCE:=live.$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.live555.com/liveMedia/public \
	https://download.videolan.org/pub/contrib/live555
PKG_HASH:=6f0c1f8a71ceb506bcbf969b02b4b0c3697b4e15daeb6dcba9872c8745ce92c6

PKG_INSTALL:=1

PKG_BUILD_DEPENDS:=openssl

include $(INCLUDE_DIR)/package.mk

PKG_UNPACK:=gzip -dc $(DL_DIR)/$(PKG_SOURCE) | $(TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xf -

define Package/livemedia/Default
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=LIVE555 Streaming Media
  URL:=http://www.live555.com/
  DEPENDS:=+libstdcpp
endef

define Package/live555mediaserver
$(call Package/livemedia/Default)
  TITLE+= (live555MediaServer)
endef

define Package/live555proxyserver
$(call Package/livemedia/Default)
  TITLE+= (live555ProxyServer)
endef

define Package/openrtsp
$(call Package/livemedia/Default)
  TITLE+= (openRTSP)
endef

define Package/playsip
$(call Package/livemedia/Default)
  TITLE+= (playSIP)
endef

define Package/vobstreamer
$(call Package/livemedia/Default)
  TITLE+= (vobStreamer)
endef

TARGET_CFLAGS += -DNO_OPENSSL=1

define Build/Configure
	$(FIND) $(PKG_BUILD_DIR) -name Makefile.* -exec \
		$(SED) 's|PREFIX =.*$$$$|PREFIX = /opt|g' {} \;
	( cd $(PKG_BUILD_DIR); \
		$(SED) 's|@CROSS_COMPILE@|$(TARGET_CROSS)|g;  \
			s|@CFLAGS@|$(TARGET_CFLAGS)|g' config.OpenWrt; \
		./genMakefiles OpenWrt; \
	)
endef

define Package/live555mediaserver/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/live555MediaServer $(1)/opt/bin
endef

define Package/live555proxyserver/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/live555ProxyServer $(1)/opt/bin
endef

define Package/openrtsp/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/openRTSP $(1)/opt/bin
endef

define Package/playsip/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/playSIP $(1)/opt/bin
endef

define Package/vobstreamer/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/vobStreamer $(1)/opt/bin
endef

$(eval $(call BuildPackage,live555mediaserver))
$(eval $(call BuildPackage,live555proxyserver))
$(eval $(call BuildPackage,openrtsp))
$(eval $(call BuildPackage,playsip))
$(eval $(call BuildPackage,vobstreamer))
