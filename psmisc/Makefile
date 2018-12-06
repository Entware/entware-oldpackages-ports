#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=psmisc
PKG_VERSION:=23.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@SF/psmisc
PKG_HASH:=4b7cbffdc9373474da49b85dc3457ae511c43dc7fa7d94513fe06f89dcb87880

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/psmisc
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libncurses
  TITLE:=proc utilities
  URL:=http://psmisc.sourceforge.net/
endef

define Package/psmisc/description
 psmisc is a set of additional small useful utilities that use
 the proc filesystem: fuser, killall, pstree, and prtstat
endef

CONFIGURE_ARGS += \
	--disable-harden-flags \
	--localedir=/opt/share/locale

ifeq ($(ARCH),mips)
CONFIGURE_VARS += \
	ac_cv_member_struct_pt_regs_regs=no
endif

ifneq (,$(filter aarch64 mips,$(ARCH)))
	PEEK:=
else
	PEEK:=peekfd,
endif

MAKE_FLAGS += \
	CFLAGS="$(TARGET_CFLAGS)" \
	CPPFLAGS="$(TARGET_CPPFLAGS)" \
	LDFLAGS="$(TARGET_LDFLAGS)"

define Package/psmisc/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/bin/{fuser,killall,prtstat,pstree,$(PEEK)pslog} \
		$(1)/opt/bin
endef

$(eval $(call BuildPackage,psmisc))
