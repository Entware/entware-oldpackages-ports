#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pyxdg
PKG_VERSION:=0.28
PKG_RELEASE:=1

PYPI_NAME:=pyxdg
PKG_HASH:=3267bb3074e934df202af2ee0868575484108581e6f3cb006af1da35395e88b4

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-pyxdg
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=a library supporting various freedesktop standards
  URL:=https://freedesktop.org/wiki/Software/pyxdg/
  DEPENDS:=+python3
endef

define Package/python-pyxdg/description
  A Python module to deal with freedesktop.org specifications.
endef

$(eval $(call Py3Package,python3-pyxdg))
$(eval $(call BuildPackage,python3-pyxdg))
