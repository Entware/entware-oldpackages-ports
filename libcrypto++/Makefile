#
# Copyright (C) 2009-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Used by amule only
# -O2 flag breaks library

include $(TOPDIR)/rules.mk

PKG_NAME:=libcrypto++
PKG_VERSION:=5.6.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION).orig.tar.xz
PKG_SOURCE_URL:=http://ftp.de.debian.org/debian/pool/main/libc/libcrypto++
PKG_HASH:=9f43f03afb1c135d6bb9a83b5143049b26fb172e7d0a0defccf723adc1dba71c

PKG_FIXUP:=autoreconf
PKG_REMOVE_FILES:=GNUmakefile
PKG_INSTALL:=1

#include $(INCLUDE_DIR)/uclibc++.mk
include $(INCLUDE_DIR)/package.mk

define Package/libcryptoxx
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libstdcpp +libpthread
  TITLE:=Crypto++ is library for creating C++ programs which use cryptographic algorithms
  URL:=https://www.cryptopp.com/
endef

define Package/package/libcryptoxx
  Crypto++ is library for creating C++ programs which use cryptographic algorithms.
  The library uses a Pipes & Filters architecture with heavy use of templates and
  abstract base classes.
endef

CONFIGURE_ARGS += \
	--enable-static \
	--enable-shared

TARGET_LDFLAGS += \
	-lpthread

TARGET_CFLAGS := $(subst -O2,-O1,$(TARGET_CFLAGS))

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include/crypto++
	$(CP) $(PKG_INSTALL_DIR)/opt/include/crypto--/* $(1)/opt/include/crypto++
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcrypto++.{a,so*} $(1)/opt/lib
endef

define Package/libcryptoxx/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcrypto++.so* $(1)/opt/lib
endef

$(eval $(call BuildPackage,libcryptoxx))
