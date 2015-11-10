#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gdb_legacy
PKG_VERSION:=7.3.1
PKG_RELEASE:=1

PKG_SOURCE:=gdb-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=@GNU/gdb
PKG_MD5SUM:=b89a5fac359c618dda97b88645ceab47

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_LICENSE:=GPL-3.0+

PKG_BUILD_DIR:=$(BUILD_DIR)/gdb-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/gdb_legacy/Default
  SECTION:=devel
  CATEGORY:=Development
  DEPENDS:=+!USE_MUSL:libthread-db +PACKAGE_zlib:zlib @TARGET_mipselsf
  URL:=http://www.gnu.org/software/gdb_legacy/
endef

define Package/gdb_legacy
$(call Package/gdb_legacy/Default)
  TITLE:=GNU Debugger
  DEPENDS+=+libreadline +libncurses +zlib
endef

define Package/gdb_legacy/description
GDB, the GNU Project debugger, allows you to see what is going on `inside'
another program while it executes -- or what another program was doing at the
moment it crashed.
endef

define Package/gdbserver_legacy
$(call Package/gdb_legacy/Default)
  TITLE:=Remote server for GNU Debugger
endef

define Package/gdbserver_legacy/description
GDBSERVER is a program that allows you to run GDB on a different machine than the
one which is running the program being debugged.
endef

# XXX: add --disable-werror to prevent build failure with arm
CONFIGURE_ARGS+= \
	--with-system-readline \
	--without-expat \
	--disable-werror

CONFIGURE_VARS+= \
	ac_cv_search_tgetent="$(TARGET_LDFLAGS) -lncurses -lreadline"

define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		CPPFLAGS="$(TARGET_CPPFLAGS)" \
		all
endef

define Build/Install
	$(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		CPPFLAGS="$(TARGET_CPPFLAGS)" \
		install-gdb
endef

define Package/gdb_legacy/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/gdb $(1)/opt/bin/
endef

define Package/gdbserver_legacy/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/gdbserver $(1)/opt/bin/
endef

$(eval $(call BuildPackage,gdb_legacy))
$(eval $(call BuildPackage,gdbserver_legacy))
