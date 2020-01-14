#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python-pyxdg
PKG_VERSION:=0.26
PKG_RELEASE:=1

PYPI_NAME:=pyxdg
PKG_HASH:=fe2928d3f532ed32b39c32a482b54136fe766d19936afc96c8f00645f9da1a06

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python-package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

# XXX error: option --single-version-externally-managed not recognized
PYTHON_PKG_SETUP_ARGS:=
PYTHON3_PKG_SETUP_ARGS:=

define Package/python-pyxdg/Default
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=a library supporting various freedesktop standards
  URL:=https://freedesktop.org/wiki/Software/pyxdg/
endef

define Package/python-pyxdg
$(call Package/python-pyxdg/Default)
  DEPENDS:=+PACKAGE_python-pyxdg:python
  VARIANT:=python
endef

define Package/python3-pyxdg
$(call Package/python-pyxdg/Default)
  DEPENDS:=+PACKAGE_python3-pyxdg:python3
  VARIANT:=python3
endef

define Package/python-pyxdg/description
  A Python module to deal with freedesktop.org specifications.
endef

define Package/python3-pyxdg/description
$(call Package/python-pyxdg/description)
.
(Variant for Python3)
endef

$(eval $(call PyPackage,python-pyxdg))
$(eval $(call BuildPackage,python-pyxdg))

$(eval $(call Py3Package,python3-pyxdg))
$(eval $(call BuildPackage,python3-pyxdg))
