#
# Copyright (C) 2007 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=empty
PKG_VERSION:=0.6.21b
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=@SF/empty
PKG_HASH:=2fccd0faa1b3deaec1add679cbde3f34250e45872ad5df463badd4bb4edeb797

PKG_UNPACK=$(HOST_TAR) -C $(PKG_BUILD_DIR) -xzf $(DL_DIR)/$(PKG_SOURCE)

include $(INCLUDE_DIR)/package.mk

define Package/empty
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Run applications under pseudo-terminal sessions
  URL:=http://empty.sourceforge.net
endef

define Package/empty/description
 empty is an utility that provides an interface to execute and/or interact
 with processes under pseudo-terminal sessions (PTYs). This tool is
 definitely useful in programming of shell scripts designed to communicate
 with interactive programs like telnet, ssh, ftp, etc. In some cases, empty
 can be the simplest replacement for TCL/expect or other similar
 programming tools.
endef

TARGET_CFLAGS+=$(TARGET_LDFLAGS)

define Package/empty/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/opt/sbin
endef

$(eval $(call BuildPackage,empty))
