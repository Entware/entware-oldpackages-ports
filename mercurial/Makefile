#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mercurial
PKG_VERSION:=5.7
PKG_RELEASE:=1

PYPI_NAME:=$(PKG_NAME)
PKG_HASH:=609c3e7c9276dd75b03b713eccc10f5e0553001f35ae21600bcea1509699c601

PKG_BUILD_DEPENDS:=zstd

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

PZSTD=zstandard-0.15.1

define Download/pzstd
  URL:=https://github.com/indygreg/python-zstandard/releases/download/0.15.1
  FILE:=$(PZSTD).tar.gz
  HASH:=cb7c6a6f7d62350b9f5539045da54422975630e34dd9069584cc776b9917115f
endef
$(eval $(call Download,pzstd))

define Build/Prepare
	$(PKG_UNPACK)
	rm -rf $(PKG_BUILD_DIR)/contrib/python-zstandard/*
	tar --strip-components=1 -C $(PKG_BUILD_DIR)/contrib/python-zstandard -xvzf $(DL_DIR)/$(PZSTD).tar.gz
endef


$(eval $(call Py3Package,mercurial))
$(eval $(call BuildPackage,mercurial))
