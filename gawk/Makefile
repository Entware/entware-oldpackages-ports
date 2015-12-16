#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gawk
PKG_VERSION:=4.1.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@GNU/$(PKG_NAME)
PKG_MD5SUM:=55d37f4069502677f25d1340df8eec97
PKG_CAT:=zcat

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/gawk
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=GAWK
	URL:=http://www.gnu.org/software/gawk/
endef

define Package/gawk/description
	GNU version of AWK.
endef

CONFIGURE_ARGS += \
	--without-readline

define Package/gawk/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/{gawk,igawk} $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/lib/{awk,gawk}
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/lib/awk/{gr,pw}cat $(1)/opt/lib/awk
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/lib/gawk/*.so $(1)/opt/lib/gawk
	$(INSTALL_DIR) $(1)/opt/share/awk
	$(CP) $(PKG_INSTALL_DIR)/opt/share/awk/*.awk $(1)/opt/share/awk
endef

$(eval $(call BuildPackage,gawk))
