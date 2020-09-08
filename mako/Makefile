#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mako
PKG_VERSION:=1.1.3
PKG_RELEASE:=1

PYPI_NAME:=Mako
PKG_HASH:=8195c8c1400ceb53496064314c6736719c6f25e7479cd24c77be3d9361cddc27

PKG_LICENSE:=BSD
PKG_LICENSE_FILES:=LICENSES.txt

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-mako
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=Mako Templates
  URL:=https://www.makotemplates.org/
  DEPENDS:=+python3-light
endef

define Package/python3-mako/description
  Mako is a template library written in Python. It provides a familiar, non-XML 
  syntax which compiles into Python modules for maximum performance.
endef

$(eval $(call Py3Package,python3-mako))
$(eval $(call BuildPackage,python3-mako))
