#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=tftp-hpa
PKG_VERSION:=6.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://git.kernel.org/pub/scm/network/tftp/tftp-hpa.git
PKG_SOURCE_VERSION:=a17da7d1f191394f15dbf10e5b27e2d73f10dcae
PKG_MIRROR_HASH:=c28f57dce59a9c8b3b28f9a7bd0b15d11219a213ef183d5a3b9d5f2d11f00fb2

include $(INCLUDE_DIR)/package.mk

define Package/tftp-hpa/Default
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=File Transfer
  DEPENDS:=+libreadline
  URL:=https://git.kernel.org/pub/scm/network/tftp/tftp-hpa.git/about/
endef

define Package/tftp-hpa
  $(call Package/tftp-hpa/Default)
  TITLE:=An enhanced version of the BSD TFTP client
endef

define Package/tftpd-hpa
  $(call Package/tftp-hpa/Default)
  TITLE:=An enhanced version of the BSD TFTP server
endef

CONFIGURE_ARGS += \
	CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS)"

define Build/Prepare
	$(call Build/Prepare/Default)
	(cd $(PKG_BUILD_DIR); \
		AUTOCONF=$(STAGING_DIR_HOST)/bin/autoconf \
		AUTOMAKE=$(STAGING_DIR_HOST)/bin/automake \
		ACLOCAL=$(STAGING_DIR_HOST)/bin/aclocal \
		AUTOHEADER=$(STAGING_DIR_HOST)/bin/autoheader \
		./autogen.sh; \
	)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)
endef

define Package/tftp-hpa/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tftp/tftp $(1)/opt/bin/tftp-hpa
endef

define Package/tftpd-hpa/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tftpd/tftpd $(1)/opt/sbin/tftpd-hpa
endef

$(eval $(call BuildPackage,tftp-hpa))
$(eval $(call BuildPackage,tftpd-hpa))
