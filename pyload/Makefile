#
# Copyright (C) 2011-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# The newer revs installed as a python package and requires 'setuptools>=0.6.39

include $(TOPDIR)/rules.mk

PKG_NAME:=pyload
PKG_VERSION:=0.4.20
PKG_REV:=1f29cd14d4c3d90d3249d20165a21c2b04ffed26
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/pyload/pyload
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

PYTHON3_PKG_BUILD:=0

include $(INCLUDE_DIR)/package.mk

define Package/pyload
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+python3-curl +python3-sqlite3
  TITLE:=A fast, lightweight and full featured download manager
  URL:=http://pyload.org
endef

Build/Configure:=:
Build/Compile:=:

define Package/pyload/install
	$(INSTALL_DIR) $(1)/opt/share/pyload
	$(CP) $(PKG_BUILD_DIR)/{icons,locale,module,scripts,tests,*.py} \
	    $(1)/opt/share/pyload
	$(INSTALL_DIR) $(1)/opt/bin
	$(LN) ../share/pyload/pyLoadCore.py $(1)/opt/bin/pyload
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S51pyload $(1)/opt/etc/init.d
	# Entware specific: fix exec path in scripts
	$(FIND) $(1)/opt/share -type f | $(XARGS) $(SED) \
		's,^#!.*python,#!/opt/bin/python,'
endef

define Package/pyload/postinst
#!/bin/sh
cat << EOF
Please install optional pyload dependencies first.

* for SSL connection with WebUI:
opkg install python-pyopenssl openssl-util

* for several hosters, ClickNLoad feature:
opkg install duktape

* for captcha recognition for a small amount of plugins:
opkg install pillow tesseract

* for RSDF/CCF/DLC support to decrypt container files:
opkg install python-crypto

* for using ExtractArchive plugin:
opkg install unrar unzip

And only then configure pyload by
pyload --configdir=/opt/var/pyload
EOF
endef

$(eval $(call BuildPackage,pyload))
