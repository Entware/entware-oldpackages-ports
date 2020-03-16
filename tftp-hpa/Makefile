#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2011

include $(TOPDIR)/rules.mk

PKG_NAME:=tftp-hpa
PKG_VERSION:=5.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@KERNEL/software/network/tftp/tftp-hpa
PKG_HASH:=acc04dde662491e3092565ecf9bde504c47dbb1bb0408366009b138fe7754cab

include $(INCLUDE_DIR)/package.mk

define Package/tftp-hpa/Default
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=File Transfer
  DEPENDS:=+libreadline
  URL:=http://www.kernel.org/pub/software/network/tftp
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
	--without-tcpwrappers \
	CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS)"

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
