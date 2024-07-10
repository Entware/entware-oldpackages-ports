#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mercurial
PKG_VERSION:=6.8
PKG_RELEASE:=1

PYPI_NAME:=$(PKG_NAME)
PKG_HASH:=08e4d0e5da8af1132b51e6bc3350180ad57adcd935f097b6d0bc119a2c2c0a10

PKG_BUILD_DEPENDS:=zstd python-wheel/host

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/mercurial
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Version Control Systems
  TITLE:=Mercurial Source Control Management (SCM) system
  URL:=https://www.mercurial-scm.org/
  DEPENDS:=+python3
endef

define Package/mercurial/description
  A fast, lightweight Source Control Management system designed for efficient
  handling of very large distributed projects.
endef

PZSTD=zstandard-0.22.0

define Download/pzstd
  URL:=https://github.com/indygreg/python-zstandard/releases/download/0.22.0
  FILE:=$(PZSTD).tar.gz
  HASH:=8226a33c542bcb54cd6bd0a366067b610b41713b64c9abec1bc4533d69f51e70
endef
$(eval $(call Download,pzstd))

define Build/Prepare
	$(call Build/Prepare/Default)
	rm -rf $(PKG_BUILD_DIR)/contrib/python-zstandard/*
	tar --strip-components=1 -C $(PKG_BUILD_DIR)/contrib/python-zstandard -xvzf $(DL_DIR)/$(PZSTD).tar.gz
endef

$(eval $(call Py3Package,mercurial))
$(eval $(call BuildPackage,mercurial))
