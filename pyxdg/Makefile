#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pyxdg
PKG_VERSION:=0.25
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://pypi.python.org/packages/source/p/pyxdg
PKG_HASH:=81e883e0b9517d624e8b0499eb267b82a815c0b7146d5269f364988ae031279d

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
