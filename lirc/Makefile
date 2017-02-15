#
# Copyright (C) 2006-2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lirc
PKG_VERSION:=0.9.4b
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=@SF/$(PKG_NAME)
PKG_MD5SUM:=9e3f2869a47bbd7c973dd63f30c13fc2

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_BUILD_DEPENDS:=python3/host

include $(INCLUDE_DIR)/uclibc++.mk
include $(INCLUDE_DIR)/package.mk

define Package/lirc
    SECTION:=utils
    CATEGORY:=Utilities
    DEPENDS:=+libusb-compat +libftdi1 +alsa-lib +libudev +libstdcpp
    TITLE:=LIRC - Linux Infrared Remote Control
    URL:=http://lirc.org/
endef

define Package/lirc/description
 LIRC is a package that allows you to decode and send infra-red signals of many
 (but not all) commonly used remote controls.
endef

CONFIGURE_ARGS += \
	--enable-sandboxed \
	--without-x \
	ac_cv_file__usr_lib_systemd_system=no \

CONFIGURE_VARS += \
	PYTHON=python \

define Package/lirc/conffiles
/opt/etc/lirc_options.conf
/opt/etc/lircd.conf
/opt/etc/lircmd.conf
endef

define Package/lirc/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin
	$(RM) $(1)/opt/bin/{irdb-get,lirc-config-tool,lirc-setup,pronto2lirc}
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/* $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/lirc/lircd.conf.d
	$(INSTALL_CONF) \
	    $(PKG_INSTALL_DIR)/opt/etc/lirc/lirc{_options,d,md}.conf \
	    $(1)/opt/etc/lirc
	$(INSTALL_DIR) $(1)/opt/lib/lirc/plugins
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/*.so* $(1)/opt/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/lib/lirc/plugins/*.so \
	    $(1)/opt/lib/lirc/plugins
	$(INSTALL_DIR) $(1)/opt/var/run/lirc
	$(INSTALL_DIR) $(1)/opt/share/lirc/configs
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/share/lirc/configs/*.conf $(1)/opt/share/lirc/configs
endef

$(eval $(call BuildPackage,lirc))
