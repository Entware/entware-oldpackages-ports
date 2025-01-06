#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=remind
PKG_VERSION:=05.01.01
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://dianne.skoll.ca/projects/remind/download
PKG_HASH:=f74e95f507451ca275fae5eff73ac5cfdb307de56bfe4c609202a41acb1c518d

PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYRIGHT

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
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/rem2html/rem2html $(1)/opt/bin
endef

$(eval $(call BuildPackage,remind))
