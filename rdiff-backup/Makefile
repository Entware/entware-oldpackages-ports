#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=rdiff-backup
PKG_VERSION:=2.0.5
PKG_RELEASE:=1

PYPI_NAME:=rdiff-backup
PKG_HASH:=54d16038e62014ed916c71c8303b07d2fa61a6a68038ca189fc2d31534b0f38b

PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/rdiff-backup/Default
  SUBMENU:=Backup
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Incremental backup utility
  URL:=https://rdiff-backup.net/
endef

define Package/python3-rdiff-backup
$(call Package/rdiff-backup/Default)
  DEPENDS+=+python3-light +librsync
  VARIANT:=python3
endef

define Package/python3-rdiff-backup/description
	rdiff-backup backs up one directory to another, possibly over a
	network. The target directory ends up a copy of the source directory,
	but extra reverse diffs are stored in a special subdirectory of that
	target directory, so you can still recover files lost some time ago.
	The idea is to combine the best features of a mirror and an incremental
	backup.
endef

$(eval $(call Py3Package,python3-rdiff-backup))
$(eval $(call BuildPackage,python3-rdiff-backup))
