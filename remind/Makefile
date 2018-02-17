#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=remind
PKG_VERSION:=03.01.15
PKG_RELEASE:=1

PKG_SOURCE:=remind-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://www.roaringpenguin.com/files/download/
PKG_HASH:=8adab4c0b30a556c34223094c5c74779164d5f3b8be66b8039f44b577e678ec1

PKG_BUILD_DIR:=$(BUILD_DIR)/remind-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/remind
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Reminder
	URL:=https://www.roaringpenguin.com/products/remind
endef

define Package/remind/description
 Remind is a powerfull commadline reminder.
endef

define Package/remind/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/{remind,rem2ps} $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/www/rem2html $(1)/opt/bin
endef

$(eval $(call BuildPackage,remind))
