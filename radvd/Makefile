#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=radvd
PKG_VERSION:=2.19
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.litech.org/radvd/dist
PKG_HASH:=c36470706fec3a9e6bed394ffea08acaff5dac647848d26b96bb9b9c65d58da0

PKG_MAINTAINER:=QshenX <q@xd8.cn>
PKG_LICENSE:=GPL-2.0

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/radvd/Default
  SECTION:=net
  CATEGORY:=Network
  TITLE:=IPv6 Routing Advertisement
  URL:=http://v6web.litech.org/radvd/
  DEPENDS:=+libdaemon
endef

define Package/radvd
  $(call Package/radvd/Default)
  TITLE+= Daemon
endef

define Package/radvd/description
radvd is the router advertisement daemon for IPv6. It listens to router
solicitations and sends router advertisements as described in "Neighbor
Discovery for IP Version 6 (IPv6)" (RFC 4861).  With these advertisements hosts
can automatically configure their addresses and some other parameters. They also
can choose a default router based on these advertisements.
endef

define Package/radvdump
  $(call Package/radvd/Default)
  TITLE+= Dumper
endef

define Package/radvdump/description
radvdump prints out the contents of incoming router advertisements sent by radvd
or some other software implementing (parts of) "Neighbor Discovery for IP
Version 6 (IPv6)" (RFC 4861).
endef

CONFIGURE_ARGS += \
	--with-configfile=/opt/etc/radvd.conf \
	--with-logfile=/opt/var/log/radvd.log \
	--with-pidfile=/opt/var/run/radvd.pid

TARGET_CFLAGS += \
	-std=gnu99

TARGET_LDFLAGS += \
	-lssp

define Package/radvd/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/radvd $(1)/opt/sbin
endef

define Package/radvdump/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/radvdump $(1)/opt/sbin
endef

$(eval $(call BuildPackage,radvd))
$(eval $(call BuildPackage,radvdump))
