#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=remind
PKG_VERSION:=04.00.00
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://dianne.skoll.ca/projects/remind/download \
	https://dianne.skoll.ca/projects/remind/download
PKG_HASH:=23b6e6b0edc40149e6a362a8232e66cb15ee641f2dcece640845e91b9e74c7c6

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
