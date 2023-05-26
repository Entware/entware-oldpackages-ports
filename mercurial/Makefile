#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mercurial
PKG_VERSION:=6.4.3
PKG_RELEASE:=1

PYPI_NAME:=$(PKG_NAME)
PKG_HASH:=a77fb62d325934a83a00b2fc6db109f44c67b86768fc40490366f513640c7f64

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

PZSTD=zstandard-0.20.0

define Download/pzstd
  URL:=https://github.com/indygreg/python-zstandard/releases/download/0.20.0
  FILE:=$(PZSTD).tar.gz
  HASH:=613daadd72c71b1488742cafb2c3b381c39d0c9bb8c6cc157aa2d5ea45cc2efc
endef
$(eval $(call Download,pzstd))

define Build/Prepare
	$(PKG_UNPACK)
	rm -rf $(PKG_BUILD_DIR)/contrib/python-zstandard/*
	tar --strip-components=1 -C $(PKG_BUILD_DIR)/contrib/python-zstandard -xvzf $(DL_DIR)/$(PZSTD).tar.gz
endef

$(eval $(call Py3Package,mercurial))
$(eval $(call BuildPackage,mercurial))
