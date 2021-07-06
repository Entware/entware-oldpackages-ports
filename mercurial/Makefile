#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mercurial
PKG_VERSION:=5.8
PKG_RELEASE:=1

PYPI_NAME:=$(PKG_NAME)
PKG_HASH:=fc5d6a8f6478d88ef83cdd0ab6d86ad68ee722bbdf4964e6a0b47c3c6ba5309f

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

PZSTD=zstandard-0.15.2

define Download/pzstd
  URL:=https://github.com/indygreg/python-zstandard/releases/download/0.15.2
  FILE:=$(PZSTD).tar.gz
  HASH:=52de08355fd5cfb3ef4533891092bb96229d43c2069703d4aff04fdbedf9c92f
endef
$(eval $(call Download,pzstd))

define Build/Prepare
	$(PKG_UNPACK)
	rm -rf $(PKG_BUILD_DIR)/contrib/python-zstandard/*
	tar --strip-components=1 -C $(PKG_BUILD_DIR)/contrib/python-zstandard -xvzf $(DL_DIR)/$(PZSTD).tar.gz
endef

$(eval $(call Py3Package,mercurial))
$(eval $(call BuildPackage,mercurial))
