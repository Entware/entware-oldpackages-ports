#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=rdiff-backup
PKG_VERSION:=1.3.3
PKG_REV:=4864f2fcc195a1a0b3d303766505b58f16223bff
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_MIRROR_HASH:=da777d91c4e13541a32a3a944520b0375d8be5c126812e739f2494f4cc496cce
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/sol1/rdiff-backup.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

PKG_BUILD_DEPENDS:=python

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python-package.mk

define Package/rdiff-backup
  SUBMENU:=backup
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Incremental backup utility
  URL:=http://www.nongnu.org/rdiff-backup
  DEPENDS:=+python +librsync +openssl-util
endef

define Package/rdiff-backup/description
	rdiff-backup backs up one directory to another, possibly over a
	network. The target directory ends up a copy of the source directory,
	but extra reverse diffs are stored in a special subdirectory of that
	target directory, so you can still recover files lost some time ago.
	The idea is to combine the best features of a mirror and an incremental
	backup.
endef

define Build/Configure
	mv $(PKG_BUILD_DIR)/rdiff-backup $(PKG_BUILD_DIR)/rdiff-backup.src
	mv $(PKG_BUILD_DIR)/rdiff-backup.src/* $(PKG_BUILD_DIR)
	mv $(PKG_BUILD_DIR)/dist/setup.py $(PKG_BUILD_DIR)
	mv $(PKG_BUILD_DIR)/rdiff_backup/*.c $(PKG_BUILD_DIR)
	mv $(PKG_BUILD_DIR)/FAQ-body.html $(PKG_BUILD_DIR)/FAQ.html
	$(call Build/Configure/Default)
endef

define PyPackage/rdiff-backup/filespec
+|/opt/bin/rdiff-backup
+|/opt/bin/rdiff-backup-statistics
+|$(PYTHON_PKG_DIR)/rdiff_backup
endef

define Build/Compile
	$(if $(Build/Compile/PyMod),,@echo Python packaging code not found.; false)
	$(call Build/Compile/PyMod,., \
		build --librsync-dir="$(STAGING_DIR)/opt" , \
	)
	$(call Build/Compile/PyMod,., \
		install --prefix="$(PKG_INSTALL_DIR)/opt", \
	)
endef

$(eval $(call PyPackage,rdiff-backup))
$(eval $(call BuildPackage,rdiff-backup))
