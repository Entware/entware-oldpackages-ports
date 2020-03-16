#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python-mako
PKG_VERSION:=1.1.2
PKG_RELEASE:=1

PYPI_NAME:=Mako
PKG_HASH:=3139c5d64aa5d175dbafb95027057128b5fbd05a40c53999f3905ceb53366d9d

PKG_LICENSE:=BSD
PKG_LICENSE_FILES:=LICENSES.txt

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python-package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python-mako/Default
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=Mako Templates
  URL:=https://www.makotemplates.org/
endef

define Package/python-mako
$(call Package/python-mako/Default)
  DEPENDS+=+PACKAGE_python-mako:python-light
  VARIANT:=python
endef

define Package/python3-mako
$(call Package/python-mako/Default)
  DEPENDS+=+PACKAGE_python3-mako:python3-light
  VARIANT:=python3
endef

define Package/python-mako/description
  Mako is a template library written in Python. It provides a familiar, non-XML 
  syntax which compiles into Python modules for maximum performance.
endef

define Package/python3-mako/description
$(call Package/python-mako/description)
.
(Variant for Python3)
endef

$(eval $(call PyPackage,python-mako))
$(eval $(call BuildPackage,python-mako))

$(eval $(call Py3Package,python3-mako))
$(eval $(call BuildPackage,python3-mako))
