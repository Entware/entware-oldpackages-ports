#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pyxdg
PKG_VERSION:=0.27
PKG_RELEASE:=1

PYPI_NAME:=pyxdg
PKG_HASH:=80bd93aae5ed82435f20462ea0208fb198d8eec262e831ee06ce9ddb6b91c5a5

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

# XXX error: option --single-version-externally-managed not recognized
PYTHON3_PKG_SETUP_ARGS:=

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
