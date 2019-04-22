#
# Copyright (C) 2008-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Depends on nagios 3.x only, no need to update it in future

include $(TOPDIR)/rules.mk

PKG_NAME:=nagios-plugins
PKG_VERSION:=2.0.3
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://nagios-plugins.org/download
PKG_HASH:=8f0021442dce0138f0285ca22960b870662e28ae8973d49d439463588aada04a

PKG_BUILD_DEPENDS:=bind
PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/nagios-plugins
  SECTION:=admin
  CATEGORY:=Administration
  DEPENDS:=+libopenssl +libpthread +librt +bash
  TITLE:=plugins for Nagios checks
  URL:=http://nagiosplug.sourceforge.net/
endef

CONFIGURE_ARGS += \
	--with-trusted-path="/bin:/sbin:/usr/bin:/usr/sbin:/opt/bin:/opt/sbin" \
	--with-perl="/opt/bin/perl" \
	--with-openssl="$(STAGING_DIR)/opt" \
	--without-pgsql \
	--without-radius \
	--without-ldap \
	--without-mysql \
	--without-dbi \
	$(call autoconf_bool,CONFIG_IPV6,ipv6) \
	--with-ping-command="/bin/ping -w %d -c %d %s" \
	--with-ping6-command="/bin/ping6 -w %d -c %d %s" \
	--with-ps-command="/bin/ps w" \
	--with-ps-cols="6" \
	--with-ps-format="%d %s %d %s %s %n" \
	--with-ps-varlist="&procpid$(comma)&procuid$(comma)&procvsz$(comma)procstat$(comma)procprog$(comma)&pos" \
	--with-uptime-command="/usr/bin/uptime" \
	--with-ssh-command="/usr/bin/ssh" \
	--with-nslookup-command="/usr/bin/nslookup" \
	--with-dig-command="/opt/bin/dig"

define Package/nagios-plugins/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/* $(1)/opt/lib
	$(SED) 's,/bin/bash,/opt/bin/bash,g' \
	    $(1)/opt/lib/check_{log,oracle,sensors}
endef

$(eval $(call BuildPackage,nagios-plugins))
