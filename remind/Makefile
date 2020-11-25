#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=remind
PKG_VERSION:=03.03.03
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://dianne.skoll.ca/projects/remind/download
PKG_HASH:=10f946fd5b5cd83e4ba435ca493d3ebff235a5808aef1f871010942e95ea8e02

include $(INCLUDE_DIR)/package.mk

define Package/remind
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Reminder
	URL:=https://dianne.skoll.ca/projects/remind
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
