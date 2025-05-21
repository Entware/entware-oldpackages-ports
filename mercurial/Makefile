#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mercurial
PKG_VERSION:=7.0.2
PKG_RELEASE:=1

PYPI_NAME:=$(PKG_NAME)
PKG_HASH:=f7731f1b42acaeaacb8cf7e41c0a472a7aa31a8f47e518baea735f1cb2987e0c

PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING

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

PZSTD_VERSION:=0.23.0
PZSTD_FILE:=python-zstandard-$(PZSTD_VERSION).tar.gz

define Download/pzstd
  FILE:=$(PZSTD_FILE)
  URL:=https://codeload.github.com/indygreg/python-zstandard/tar.gz/refs/tags/$(PZSTD_VERSION)?
  HASH:=f29233338bcef11f233737eb58aba85074f0fd3163bec1a20303de1270e6fb16
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	rm -rf $(PKG_BUILD_DIR)/contrib/python-zstandard/*
	$(TAR) -xf $(DL_DIR)/$(PZSTD_FILE) --strip-components=1 -C $(PKG_BUILD_DIR)/contrib/python-zstandard
endef

define Package/mercurial/postrm
#!/bin/sh

rm -rf $(PYTHON3_PKG_DIR)/hgdemandimport
rm -rf $(PYTHON3_PKG_DIR)/hgext
rm -rf $(PYTHON3_PKG_DIR)/hgext3rd
rm -rf $(PYTHON3_PKG_DIR)/$(PYPI_NAME)
rm -rf $(PYTHON3_PKG_DIR)/$(PYPI_NAME)-$(PKG_VERSION).dist-info
endef

$(eval $(call Download,pzstd))
$(eval $(call Py3Package,mercurial))
$(eval $(call BuildPackage,mercurial))
