#
# Copyright (C) 2006 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2008

include $(TOPDIR)/rules.mk

PKG_NAME:=dtach
PKG_VERSION:=0.9
PKG_REV:=7acac922770597f5da5df7b290078770d20dac32
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/crigler/dtach.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

define Package/dtach
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=A program that emulates the dtach feature of screen
  URL:=http://dtach.sourceforge.net/
endef

define Package/dtach/description
	dtach is a tiny program that emulates the detach feature of screen,
	allowing you to run a program in an environment that is protected from
	the controlling terminal and attach to it later. dtach does not keep
	track of the contents of the screen, and thus works best with programs
	that know how to redraw themselves.
endef

define Package/dtach/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dtach $(1)/opt/bin
endef

$(eval $(call BuildPackage,dtach))
