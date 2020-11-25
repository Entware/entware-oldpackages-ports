#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mercurial
PKG_VERSION:=5.6
PKG_RELEASE:=1

PYPI_NAME:=$(PKG_NAME)
PKG_HASH:=dfa7b3b5082783763710504f242ec487a5d801dc4bcd701cdad4b6ffc1f062c2

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

$(eval $(call Py3Package,mercurial))
$(eval $(call BuildPackage,mercurial))
