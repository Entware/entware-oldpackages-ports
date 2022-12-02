#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=remind
PKG_VERSION:=04.02.00
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://dianne.skoll.ca/projects/remind/download \
	https://dianne.skoll.ca/projects/remind/download
PKG_HASH:=a6476cf0dfe71bc4668e774669100c58d68b68dc6ccf08ca7ea9fa3345e72739

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
