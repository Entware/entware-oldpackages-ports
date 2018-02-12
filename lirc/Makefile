#
# Copyright (C) 2006-2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lirc
PKG_VERSION:=0.10.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=@SF/$(PKG_NAME)
PKG_HASH:=8b753c60df2a7f5dcda2db72c38e448ca300c3b4f6000c1501fcb0bd5df414f2

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_BUILD_DEPENDS:=python3/host

#include $(INCLUDE_DIR)/uclibc++.mk
include $(INCLUDE_DIR)/package.mk

define Package/lirc
    SECTION:=utils
    CATEGORY:=Utilities
    DEPENDS:=+libusb-compat +libftdi1 +alsa-lib +libstdcpp +USE_GLIBC:libudev
    TITLE:=LIRC - Linux Infrared Remote Control
    URL:=http://lirc.org/
endef

define Package/lirc/description
 LIRC is a package that allows you to decode and send infra-red signals of many
 (but not all) commonly used remote controls.
endef

CONFIGURE_ARGS += \
	--with-lockdir=/opt/var/lock/lockdev \
	--without-x \
	ac_cv_file__usr_lib_systemd_system=no \

CONFIGURE_VARS += \
	PYTHON=python \
	HAVE_WORKING_POLL=yes \

define Package/lirc/conffiles
/opt/etc/lirc/lirc_options.conf
/opt/etc/lirc/lircd.conf
/opt/etc/lirc/lircmd.conf
endef

define Package/lirc/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin
	$(RM) $(1)/opt/bin/{irdb-get,irtext2udp,lirc-config-tool,lirc-init-db,lirc-setup,pronto2lirc}
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/* $(1)/opt/sbin
	$(RM) $(1)/opt/sbin/lircd-setup
	$(INSTALL_DIR) $(1)/opt/etc
	$(CP) \
	    $(PKG_INSTALL_DIR)/opt/etc/lirc \
	    $(1)/opt/etc
	$(INSTALL_DIR) $(1)/opt/lib/lirc/plugins
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/*.so* $(1)/opt/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/lib/lirc/plugins/*.so \
	    $(1)/opt/lib/lirc/plugins
	$(INSTALL_DIR) $(1)/opt/var/run/lirc $(1)/opt/share/lirc/configs
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/share/lirc/configs/*.conf \
	    $(1)/opt/share/lirc/configs
endef

$(eval $(call BuildPackage,lirc))
