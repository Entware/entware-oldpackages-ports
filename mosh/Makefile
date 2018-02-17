#
# Copyright (C) 2011-2016 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mosh
PKG_VERSION:=1.3.2
PKG_REV:=cf73e1f8799b01ad1ed9731c6b3d239b68509222
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_MIRROR_HASH:=e18b5a3557466d056fddf899c9127ab05f9c9f7962efa1154466d527ec26788c
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/mobile-shell/mosh.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/mosh/Default
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Mosh mobile shell
	DEPENDS:=+libncursesw +libopenssl +protobuf
	URL:=http://mosh.mit.edu/
endef

define Package/mosh-client
$(call Package/mosh/Default)
 TITLE+= (client)
endef

define Package/mosh-server
$(call Package/mosh/Default)
 TITLE+= (server)
endef

define Package/mosh-full
$(call Package/mosh/Default)
 TITLE+= (full)
 DEPENDS:= \
    +mosh-client \
    +mosh-server \
    +perlbase-essential \
    +perlbase-socket \
    +perlbase-xsloader \
    +perlbase-getopt \
    +perlbase-errno \
    +perlbase-config \
    +perlbase-io \
    +perlbase-symbol \
    +perlbase-selectsaver \
    +perlbase-posix \
    +perlbase-autoloader \
    +perlbase-fcntl \
    +perlbase-tie
endef


define Package/mosh/Default/description
 Mosh is a remote terminal application that allows roaming, supports
 intermittent connectivity, and provides intelligent local echo and line
 editing of user keystrokes.
endef

define Package/mosh-client/description
$(call Package/mosh/Default/description)
 This is a mosh client.
endef

define Package/mosh-server/description
$(call Package/mosh/Default/description)
 This is a mosh server.
endef

define Package/mosh-full/description
$(call Package/mosh/Default/description)
 This is a full package with perl wrapper script
endef


CONFIGURE_ARGS += \
	--with-ncurses \
	--disable-hardening \
	--without-utempter \

CONFIGURE_VARS += \
	CURSES_LIB="-lncursesw" \
	TINFO_CFLAGS="-I$(STAGING_DIR)/opt/include" \
	TINFO_LDFLAGS="-L$(STAGING_DIR)/opt/lib -lncursesw"

define Package/mosh-client/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/mosh-client $(1)/opt/bin
endef

define Package/mosh-server/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/mosh-server $(1)/opt/bin
endef

define Package/mosh-full/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/mosh $(1)/opt/bin
	$(SED) 's,/usr/bin/env perl,/opt/bin/perl,g' $(1)/opt/bin/mosh
endef

$(eval $(call BuildPackage,mosh-client))
$(eval $(call BuildPackage,mosh-server))
$(eval $(call BuildPackage,mosh-full))
