#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Entware specific: keep 2.2.1 version, kernels are too old

include $(TOPDIR)/rules.mk

PKG_NAME:=keepalived
PKG_VERSION:=2.2.1
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://www.keepalived.org/software
PKG_HASH:=91186f20c83ffc48d7a15a9a6e2329ed4feeb2dcb51f4aa9672c8840190ea741

PKG_CPE_ID:=cpe:/a:keepalived:keepalived
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING
PKG_MAINTAINER:=Ben Kelly <ben@benjii.net> \
		Florian Eckert <fe@dev.tdt.de>

PKG_CONFIG_DEPENDS:= \
	KEEPALIVED_LEGACY_VRRP \
	KEEPALIVED_LEGACY_LVS \
	KEEPALIVED_LEGACY_IPTABLES \
	KEEPALIVED_LEGACY_BFD \
	KEEPALIVED_LEGACY_SNMP_VRRP \
	KEEPALIVED_LEGACY_SNMP_CHECKER \
	KEEPALIVED_LEGACY_SNMP_RFC2 \
	KEEPALIVED_LEGACY_SNMP_RFC3 \
	KEEPALIVED_LEGACY_SNMP_REPLY_V3_FOR_V2 \
	KEEPALIVED_LEGACY_DBUS \
	KEEPALIVED_LEGACY_JSON \
	KEEPALIVED_LEGACY_ROUTES \
	IPV6

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/kernel.mk

define Package/keepalived-legacy/config
	source "$(SOURCE)/Config.in"
endef

# specifying +(IPV6&&KEEPALIVED_IPTABLES) in the DEPENDS definition doesn't work
ifeq ($(CONFIG_KEEPALIVED_LEGACY_IPTABLES)$(CONFIG_IPV6),yy)
  KEEPALIVED_LEGACY_DEPENDS_LIBIP6TC=+iptables
endif

# The +kmod-nf-ipvs line should be +KEEPALIVED_LVS:kmod-nf-ipvs,
# but make menuconfig then reports :error: recursive dependency detected!
# !!FIXME DEPENDS:= +KEEPALIVED_LVS:kmod-nf-ipvs
define Package/keepalived-legacy
  SECTION:=net
  CATEGORY:=Network
  TITLE:=VRRP with failover and monitoring daemon for LVS clusters
  URL:=http://www.keepalived.org/
  DEPENDS:= \
    @LINUX_3_2 \
    +libnl-genl \
    +libmagic \
    +KEEPALIVED_LEGACY_VRRP:libnl-route \
    +KEEPALIVED_LEGACY_VRRP:libnfnetlink \
    +KEEPALIVED_LEGACY_SHA1:libopenssl \
    +KEEPALIVED_LEGACY_IPTABLES:iptables \
    $(KEEPALIVED_LEGACY_DEPENDS_LIBIP6TC) \
    +KEEPALIVED_LEGACY_IPTABLES:libipset \
    +(KEEPALIVED_LEGACY_SNMP_VRRP||KEEPALIVED_LEGACY_SNMP_CHECKER||KEEPALIVED_LEGACY_SNMP_RFC2||KEEPALIVED_LEGACY_SNMP_RFC3):libnetsnmp \
    +KEEPALIVED_LEGACY_JSON:libjson-c \
    +KEEPALIVED_LEGACY_DBUS:glib2
  PROVIDES:=keepalived
endef

define Package/keepalived-legacy/description
 VRRP with failover and monitoring daemon for Linux Virtual Server (LVS) clusters.
endef

define Package/keepalived-legacy/conffiles
/opt/etc/keepalived/keepalived.conf
endef

CONFIGURE_ARGS+= \
	--with-init=SYSV \
	--disable-nftables \
	--disable-track-process \
	--with-run-dir="/opt/var/run" \
	--with-default_config_file="/opt/etc/keepalived/keepalived.conf"

CONFIGURE_VARS+= \
	ac_cv_func_setns=yes

ifeq ($(CONFIG_KEEPALIVED_LEGACY_VRRP),)
CONFIGURE_ARGS += \
	--disable-vrrp
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_LVS),)
CONFIGURE_ARGS += \
	--disable-lvs
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_BFD),y)
CONFIGURE_ARGS += \
	--enable-bfd
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_SHA1),y)
CONFIGURE_ARGS += \
	--enable-sha1
endif


ifeq ($(CONFIG_KEEPALIVED_LEGACY_VRRP),y)
ifeq ($(CONFIG_KEEPALIVED_LEGACY_IPTABLES),)
CONFIGURE_ARGS += \
	--disable-iptables
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_IPSETS),)
CONFIGURE_ARGS += \
	--disable-libipset-dynamic
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_SNMP_VRRP),y)
CONFIGURE_ARGS += \
	--enable-snmp-vrrp
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_SNMP_RFC2),y)
CONFIGURE_ARGS += \
	--enable-snmp-rfcv2
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_SNMP_RFC3),y)
CONFIGURE_ARGS += \
	--enable-snmp-rfcv3
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_SNMP_RFC3),y)
ifeq ($(CONFIG_KEEPALIVED_LEGACY_SNMP_REPLY_V3_FOR_V2),)
CONFIGURE_ARGS += \
	--disable-snmp-reply-v3-for-v2
endif
endif # CONFIG_KEEPALIVED_LEGACY_SNMP_RFC3

ifeq ($(CONFIG_KEEPALIVED_LEGACY_JSON),y)
CONFIGURE_ARGS += \
	--enable-json
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_VRRP_AUTH),)
CONFIGURE_ARGS += \
	--disable-vrrp-auth
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_CHECKSUM_COMPAT),)
CONFIGURE_ARGS += \
	--disable-checksum-compat
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_DBUS),y)
CONFIGURE_ARGS += \
	--enable-dbus
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_LINKBEAT),)
CONFIGURE_ARGS += \
	--disable-linkbeat
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_ROUTES),)
CONFIGURE_ARGS += \
	--disable-routes
endif
endif # CONFIG_KEEPALIVED_LEGACY_VRRP


ifeq ($(CONFIG_KEEPALIVED_LEGACY_LVS),y)
ifeq ($(CONFIG_KEEPALIVED_LEGACY_LVS_SYNCD),)
CONFIGURE_ARGS += \
	--disable-lvs-syncd
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_LVS_64BIT_STATS),)
CONFIGURE_ARGS += \
	--disable-lvs-64bit-stats
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_FWMARK),)
CONFIGURE_ARGS += \
	--disable-fwmark
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_SNMP_CHECKER),y)
CONFIGURE_ARGS += \
	--enable-snmp-checker
endif

endif # CONFIG_KEEPALIVED_LEGACY_LVS


MAKE_FLAGS += STRIP="/bin/true"
TARGET_CFLAGS += -I$(LINUX_DIR)

define Package/keepalived-legacy/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/keepalived \
		$(1)/opt/sbin/

ifeq ($(CONFIG_KEEPALIVED_LEGACY_LVS),y)
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/genhash \
		$(1)/opt/bin/
endif

	$(INSTALL_DIR) $(1)/opt/etc/keepalived
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/opt/etc/keepalived/keepalived.conf \
		$(1)/opt/etc/keepalived/

#	$(INSTALL_DIR) $(1)/etc/uci-defaults
#	$(INSTALL_BIN) ./files/etc/uci-defaults/keepalived \
#		$(1)/etc/uci-defaults/keepalived

#	$(INSTALL_DIR) $(1)/etc/init.d
#	$(INSTALL_BIN) ./files/keepalived.init \
#		$(1)/etc/init.d/keepalived

#	$(INSTALL_DIR) $(1)/etc/config
#	$(INSTALL_CONF) ./files/keepalived.config \
#		$(1)/etc/config/keepalived

#	$(INSTALL_DIR) $(1)/etc
#	$(INSTALL_CONF) ./files/keepalived.user \
#		$(1)/etc/keepalived.user

#	$(INSTALL_DIR) $(1)/etc/hotplug.d/keepalived
#	$(INSTALL_DATA) ./files/hotplug-user \
#		$(1)/etc/hotplug.d/keepalived/01-user

ifneq ($(CONFIG_KEEPALIVED_LEGACY_SNMP_VRRP)$(CONFIG_KEEPALIVED_LEGACY_SNMP_CHECKER)$(CONFIG_KEEPALIVED_LEGACY_SNMP_RFC2)$(CONFIG_KEEPALIVED_LEGACY_SNMP_RFC3),)
	$(INSTALL_DIR) $(1)/opt/share/snmp/mibs
endif

ifneq ($(CONFIG_KEEPALIVED_LEGACY_SNMP_VRRP)$(CONFIG_KEEPALIVED_LEGACY_SNMP_CHECKER),)
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/share/snmp/mibs/KEEPALIVED-MIB.txt \
		$(1)/opt/share/snmp/mibs/KEEPALIVED-MIB.txt
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_SNMP_RFC2),y)
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/share/snmp/mibs/VRRP-MIB.txt \
		$(1)/opt/share/snmp/mibs/VRRP-MIB.txt
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_SNMP_RFC3),y)
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/share/snmp/mibs/VRRPv3-MIB.txt \
		$(1)/opt/share/snmp/mibs/VRRPv3-MIB.txt
endif

ifeq ($(CONFIG_KEEPALIVED_LEGACY_DBUS),y)
	$(INSTALL_DIR) $(1)/opt/etc/dbus-1/system.d
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/etc/dbus-1/system.d/org.keepalived.Vrrp1.conf \
		$(1)/opt/etc/dbus-1/system.d/org.keepalived.Vrrp1.conf

	$(INSTALL_DIR) $(1)/opt/share/dbus-1/interfaces
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/share/dbus-1/interfaces/org.keepalived.Vrrp1.Instance.xml \
		$(1)/opt/share/dbus-1/interfaces/org.keepalived.Vrrp1.Instance.xml
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/share/dbus-1/interfaces/org.keepalived.Vrrp1.Vrrp.xml \
		$(1)/opt/share/dbus-1/interfaces/org.keepalived.Vrrp1.Vrrp.xml
endif

endef

$(eval $(call BuildPackage,keepalived-legacy))
