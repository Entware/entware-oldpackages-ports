# Abandoned in 2016
# Used by mcabber only

include $(TOPDIR)/rules.mk

PKG_NAME:=libotr
PKG_VERSION:=4.1.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://otr.cypherpunks.ca
PKG_HASH:=8b3b182424251067a952fb4e6c7b95a21e644fbb27fbd5f8af2b2ed87ca419f5

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libotr
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=OTR Messaging Library
  URL:=http://www.cypherpunks.ca/otr/
  DEPENDS:=+libgcrypt
  MAINTAINER:=Peter Wagner <tripolar@gmx.at>
endef

define Package/libotr/description
  Off-the-Record (OTR) Messaging allows you to have private conversations over
  instant messaging.
endef

TARGET_LDFLAGS += \
	-lssp

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include $(1)/opt/lib $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/include/libotr $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libotr.{a,so*} $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libotr.pc $(1)/opt/lib/pkgconfig
endef

define Package/libotr/install
	$(INSTALL_DIR) $(1)/opt/lib $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libotr.so* $(1)/opt/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/otr_* $(1)/opt/bin
endef

$(eval $(call BuildPackage,libotr))
