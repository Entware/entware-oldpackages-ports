#
# Copyright (C) 2006-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=quagga
PKG_VERSION:=1.2.4
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SAVANNAH/quagga/ \
		https://github.com/Quagga/quagga/releases/download/$(PKG_NAME)-$(PKG_VERSION)/
PKG_HASH:=e364c082c3309910e1eb7b068bf39ee298e2f2f3f31a6431a5c115193bd653d3

PKG_MAINTAINER:=Vasilis Tsiligiannis <acinonyx@openwrt.gr>
PKG_LICENSE:=GPL-2.0-or-later

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_CONFIG_DEPENDS:= \
	CONFIG_IPV6 \
	CONFIG_PACKAGE_quagga-watchquagga \
	CONFIG_PACKAGE_quagga-zebra \
	CONFIG_PACKAGE_quagga-libzebra \
	CONFIG_PACKAGE_quagga-libospf \
	CONFIG_PACKAGE_quagga-bgpd \
	CONFIG_PACKAGE_quagga-isisd \
	CONFIG_PACKAGE_quagga-ospf6d \
	CONFIG_PACKAGE_quagga-ripd \
	CONFIG_PACKAGE_quagga-ripngd \
	CONFIG_PACKAGE_quagga-vtysh

include $(INCLUDE_DIR)/package.mk

define Package/quagga/Default
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Routing and Redirection
  DEPENDS:=quagga
  TITLE:=The Quagga Software Routing Suite
  URL:=https://www.quagga.net
endef

define Package/quagga
  $(call Package/quagga/Default)
  DEPENDS:=+librt
  MENU:=1
endef

define Package/quagga/description
  A routing software package that provides TCP/IP based routing services
  with routing protocols support such as RIPv1, RIPv2, RIPng, OSPFv2,
  OSPFv3, BGP-4, and BGP-4+
endef

define Package/quagga-watchquagga
  $(call Package/quagga/Default)
  TITLE:=Quagga watchdog
  DEPENDS+=+quagga-libzebra
  DEFAULT:=y if PACKAGE_quagga
endef

define Package/quagga-zebra
  $(call Package/quagga/Default)
  TITLE:=Zebra daemon
  DEPENDS+=+quagga-libzebra
  DEFAULT:=y if PACKAGE_quagga
endef

define Package/quagga-libzebra
  $(call Package/quagga/Default)
  TITLE:=zebra library
endef

define Package/quagga-libospf
  $(call Package/quagga/Default)
  DEPENDS+=+quagga-libzebra
  TITLE:=OSPF library
endef

define Package/quagga-bgpd
  $(call Package/quagga/Default)
  DEPENDS+=+quagga-libzebra
  TITLE:=BGPv4, BGPv4+, BGPv4- routing engine
endef

define Package/quagga-isisd
  $(call Package/quagga/Default)
  DEPENDS+=+quagga-libzebra
  TITLE:=IS-IS routing engine
endef

define Package/quagga-ospfd
  $(call Package/quagga/Default)
  DEPENDS+=+quagga-libospf
  TITLE:=OSPFv2 routing engine
endef

define Package/quagga-ospf6d
  $(call Package/quagga/Default)
  DEPENDS+=+quagga-libospf @IPV6
  TITLE:=OSPFv3 routing engine
endef

define Package/quagga-ripd
  $(call Package/quagga/Default)
  DEPENDS+=+quagga-libzebra
  TITLE:=RIP routing engine
endef

define Package/quagga-ripngd
  $(call Package/quagga/Default)
  DEPENDS+=+quagga-libzebra @IPV6
  TITLE:=RIPNG routing engine
endef

define Package/quagga-vtysh
  $(call Package/quagga/Default)
  DEPENDS+=+quagga-libzebra +libreadline +libncurses
  TITLE:=integrated shell for Quagga routing software
endef

define Package/quagga-zebra/conffiles
/opt/etc/quagga/zebra.conf
endef

define Package/quagga-bgpd/conffiles
/opt/etc/quagga/bgpd.conf
endef

define Package/quagga-isisd/conffiles
/opt/etc/quagga/isisd.conf
endef

define Package/quagga-ospfd/conffiles
/opt/etc/quagga/ospfd.conf
endef

define Package/quagga-ospf6d/conffiles
/opt/etc/quagga/ospf6d.conf
endef

define Package/quagga-ripd/conffiles
/opt/etc/quagga/ripd.conf
endef

define Package/quagga-ripngd/conffiles
/opt/etc/quagga/ripngd.conf
endef

ifneq ($(SDK),)
CONFIG_PACKAGE_quagga-libzebra:=m
CONFIG_PACKAGE_quagga-libospf:=m
CONFIG_PACKAGE_quagga-watchquagga:=m
CONFIG_PACKAGE_quagga-zebra:=m
CONFIG_PACKAGE_quagga-bgpd:=m
CONFIG_PACKAGE_quagga-isisd:=m
CONFIG_PACKAGE_quagga-ospf6d:=m
CONFIG_PACKAGE_quagga-ripd:=m
CONFIG_PACKAGE_quagga-ripngd:=m
CONFIG_PACKAGE_quagga-vtysh:=m
endif

CONFIGURE_ARGS+= \
	--localstatedir=/opt/var/run/quagga \
	--sysconfdir=/opt/etc/quagga/ \
	--enable-shared \
	--disable-static \
	--enable-user=network \
	--enable-group=network \
	--enable-multipath=8 \
	--disable-ospfclient \
	--disable-capabilities \
	--disable-doc \
	--disable-nhrpd \
	$(call autoconf_bool,CONFIG_PACKAGE_quagga-libzebra,zebra) \
	$(call autoconf_bool,CONFIG_PACKAGE_quagga-libospf,ospfd) \
	$(call autoconf_bool,CONFIG_PACKAGE_quagga-bgpd,bgpd) \
	$(call autoconf_bool,CONFIG_PACKAGE_quagga-isisd,isisd) \
	$(call autoconf_bool,CONFIG_PACKAGE_quagga-ospf6d,ospf6d) \
	$(call autoconf_bool,CONFIG_PACKAGE_quagga-ripd,ripd) \
	$(call autoconf_bool,CONFIG_PACKAGE_quagga-ripngd,ripngd) \
	$(call autoconf_bool,CONFIG_PACKAGE_quagga-vtysh,vtysh)

MAKE_FLAGS += \
	CFLAGS="$(TARGET_CFLAGS) -std=gnu99"

define Package/quagga/install
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/quagga $(1)/opt/etc/init.d/S50quagga
endef

define Package/quagga-watchquagga/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/watchquagga $(1)/opt/sbin/
endef

define Package/quagga-zebra/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/zebra $(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/etc/quagga
	chmod 0750 $(1)/opt/etc/quagga
	$(INSTALL_CONF) ./files/quagga.conf $(1)/opt/etc/quagga/zebra.conf
endef

define Package/quagga-bgpd/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/bgpd $(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/etc/quagga
	chmod 0750 $(1)/opt/etc/quagga
	$(INSTALL_CONF) ./files/quagga.conf $(1)/opt/etc/quagga/bgpd.conf
endef

define Package/quagga-isisd/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/isisd $(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/etc/quagga
	chmod 0750 $(1)/opt/etc/quagga
	$(INSTALL_CONF) ./files/quagga.conf $(1)/opt/etc/quagga/isisd.conf
endef

define Package/quagga-ospfd/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/ospfd $(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/etc/quagga
	chmod 0750 $(1)/opt/etc/quagga
	$(INSTALL_CONF) ./files/quagga.conf $(1)/opt/etc/quagga/ospfd.conf
endef

define Package/quagga-ospf6d/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/ospf6d $(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/etc/quagga
	chmod 0750 $(1)/opt/etc/quagga
	$(INSTALL_CONF) ./files/quagga.conf $(1)/opt/etc/quagga/ospf6d.conf
endef

define Package/quagga-ripd/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/ripd $(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/etc/quagga
	chmod 0750 $(1)/opt/etc/quagga
	$(INSTALL_CONF) ./files/quagga.conf $(1)/opt/etc/quagga/ripd.conf
endef

define Package/quagga-ripngd/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/ripngd $(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/etc/quagga
	chmod 0750 $(1)/opt/etc/quagga
	$(INSTALL_CONF) ./files/quagga.conf $(1)/opt/etc/quagga/ripngd.conf
endef

define Package/quagga-vtysh/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/vtysh $(1)/opt/bin/
endef

define Package/quagga-libospf/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libospf.so.* $(1)/opt/lib/
endef

define Package/quagga-libzebra/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libzebra.so.* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,quagga))
$(eval $(call BuildPackage,quagga-libzebra))
$(eval $(call BuildPackage,quagga-libospf))
$(eval $(call BuildPackage,quagga-watchquagga))
$(eval $(call BuildPackage,quagga-zebra))
$(eval $(call BuildPackage,quagga-bgpd))
$(eval $(call BuildPackage,quagga-isisd))
$(eval $(call BuildPackage,quagga-ospfd))
$(eval $(call BuildPackage,quagga-ospf6d))
$(eval $(call BuildPackage,quagga-ripd))
$(eval $(call BuildPackage,quagga-ripngd))
$(eval $(call BuildPackage,quagga-vtysh))
