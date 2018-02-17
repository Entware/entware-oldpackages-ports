#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=flite
PKG_VERSION:=2.0.0-release
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://www.festvox.org/flite/packed/flite-2.0
PKG_HASH:=678c3860fd539402b5d1699b921239072af6acb4e72dc4720494112807cae411

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/flite
  SECTION:=sound
  CATEGORY:=Sound
  DEPENDS:=+alsa-lib
  TITLE:=Text-to-speech for embedded systems
  URL:=http://www.speech.cs.cmu.edu/flite/index.html
endef

define Package/flite/description
Festival Lite is a stripped down version of Festival,
	the well-developed text-to-speech program written in C++.
	This program is written in C to keep memory usage low.
endef

CONFIGURE_ARGS += \
	--enable-shared \
	--with-audio="alsa" \
	--with-vox="cmu_us_kal16" \

define Package/flite/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/flite* $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libflite*.so* $(1)/opt/lib
endef

$(eval $(call BuildPackage,flite))
