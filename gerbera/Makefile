#
# Copyright (C) 2011-2020 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gerbera
PKG_VERSION:=1.12.1
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/gerbera/gerbera/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=2144a7c4a13e8b43aa0c911fbeae65f05e2c42254ddd03be5c41f5fcf103a93c

PKG_MAINTAINER:=
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=LICENSE.md

PKG_BUILD_DEPENDS:=libmatroska pugixml spdlog

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/gerbera
  SECTION:=multimedia
  CATEGORY:=Multimedia
  DEPENDS:=+libmagic +libupnp +libsqlite3 +libexif +libuuid +libfmt +curl +duktape +libffmpegthumbnailer
  TITLE:=A free media server
  URL:=https://gerbera.io
endef

define Package/gerbera/description
 Gerbera - UPnP Media Server based on Mediatomb.
endef

define Package/gerbera/conffiles
/opt/etc/gerbera/config.xml
endef

CMAKE_OPTIONS += \
	-DWITH_MYSQL=0 \
	-DWITH_TAGLIB=0 \
	-DWITH_AVCODEC=1 \
	-DWITH_FFMPEGTHUMBNAILER=1 \
	-DWITH_SYSTEMD=0 \
	-DWITH_DEBUG=0

define Package/gerbera/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/gerbera $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/gerbera $(1)/opt/share
	$(INSTALL_DIR) $(1)/opt/etc/gerbera
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S90gerbera $(1)/opt/etc/init.d
endef

define Package/gerbera/postinst
#!/bin/sh

GERBERA_CFG=/opt/etc/gerbera/config.xml
if [ ! -f $$GERBERA_CFG ]; then
    gerbera --create-config > $$GERBERA_CFG
    echo "Please, edit $$GERBERA_CFG first."
fi
endef

$(eval $(call BuildPackage,gerbera))
