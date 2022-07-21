# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=Mako
PKG_VERSION:=1.2.1
PKG_RELEASE:=1

PYPI_NAME:=$(PKG_NAME)
PKG_HASH:=f054a5ff4743492f1aa9ecc47172cb33b42b9d993cffcc146c9de17e717b0307

PKG_MAINTAINER:=Daniel Golle <daniel@makrotopia.org>
PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE.rst
PKG_CPE_ID:=cpe:/a:palletsprojects:flask

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-mako
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=Mako
  URL:=https://www.makotemplates.org/
  DEPENDS:=+python3-light
endef

define Package/python3-mako/description
 Mako is a template library written in Python.
endef

$(eval $(call Py3Package,python3-mako))
$(eval $(call BuildPackage,python3-mako))
#$(eval $(call BuildPackage,python3-mako-src))
