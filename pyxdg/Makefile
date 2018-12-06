#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pyxdg
PKG_VERSION:=0.26
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://files.pythonhosted.org/packages/47/6e/311d5f22e2b76381719b5d0c6e9dc39cd33999adae67db71d7279a6d70f4
PKG_HASH:=fe2928d3f532ed32b39c32a482b54136fe766d19936afc96c8f00645f9da1a06

PKG_BUILD_DEPENDS:=python

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python-package.mk

define Package/pyxdg
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=pyxdg
  URL:=http://freedesktop.org/wiki/Software/pyxdg
  DEPENDS:=+python
endef

define Package/pyxdg/description
  A Python module to deal with freedesktop.org specifications
endef

define Build/Compile
        $(call Build/Compile/PyMod,,install \
            --prefix=/opt \
            --root=$(PKG_INSTALL_DIR) \
        )
endef

define Package/pyxdg/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) \
	    $(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
	    $(1)$(PYTHON_PKG_DIR)
endef

$(eval $(call BuildPackage,pyxdg))
