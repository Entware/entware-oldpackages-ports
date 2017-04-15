#
# Copyright (C) 2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Used by mcabber only

include $(TOPDIR)/rules.mk

PKG_NAME:=gpgme
PKG_VERSION:=1.9.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://www.gnupg.org/ftp/gcrypt/gpgme
PKG_HASH:=1b29fedb8bfad775e70eafac5b0590621683b2d9869db994568e6401f4034ceb

PKG_INSTALL:=1

PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk

define Package/libgpgme
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=GnuPG Made Easy library
  DEPENDS:=+libassuan
  URL:=http://www.gnupg.org/
endef

define Package/libgpgme/description
  GnuPG Made Easy (GPGME) is a library designed to make access to GnuPG easier for
  applications. It provides a High-Level Crypto API for encryption, decryption, signing,
  signature verification and key management. Currently it uses GnuPG as its backend but
  the API isn't restricted to this engine; in fact we have already developed a backend
  for CMS (S/MIME).
endef

CONFIGURE_ARGS += \
	--enable-shared \
	--disable-static \
	--with-gpg-error-prefix="$(STAGING_DIR)/opt" \
	--with-libassuan-prefix="$(STAGING_DIR)/opt" \
	--enable-languages=cl

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/gpgme.h $(1)/opt/include

	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libgpgme.so* $(1)/opt/lib
	
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/gpgme-config $(1)/opt/bin
endef

define Package/libgpgme/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libgpgme.so* $(1)/opt/lib
endef

$(eval $(call BuildPackage,libgpgme))
