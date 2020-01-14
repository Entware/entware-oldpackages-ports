#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mercurial
PKG_VERSION:=5.2
PKG_RELEASE:=1

PYPI_NAME:=$(PKG_NAME)
PKG_HASH:=ff030e923f03ee15c91191996fcb099bfcfa60c7df263be227f67b6a65d36194

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
  VARIANT:=python3
endef

define Package/mercurial/description
  A fast, lightweight Source Control Management system designed for efficient
  handling of very large distributed projects.
endef

$(eval $(call Py3Package,mercurial))
$(eval $(call BuildPackage,mercurial))
