#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mako
PKG_VERSION:=1.1.0
PKG_RELEASE:=1

PKG_SOURCE:=Mako-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://files.pythonhosted.org/packages/b0/3c/8dcd6883d009f7cae0f3157fb53e9afb05a0d3d33b3db1268ec2e6f4a56b
PKG_HASH:=a36919599a9b7dc5d86a7a8988f23a9a3a3d083070023bab23d64f7f1d1e0a4b

PKG_BUILD_DIR:=$(BUILD_DIR)/$(subst .tar.gz,,$(PKG_SOURCE))

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python-package.mk

define Package/mako
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Mako Templates for Python
  URL:=http://www.makotemplates.org/
  DEPENDS:=+python
endef

define Package/mako/description
Mako is a template library written in Python. It provides a familiar,
non-XML syntax which compiles into Python modules for maximum
performance. Mako's syntax and API borrows from the best ideas of many
others, including Django templates, Cheetah, Myghty, and
Genshi. Conceptually, Mako is an embedded Python (i.e. Python Server
Page) language, which refines the familiar ideas of componentized
layout and inheritance to produce one of the most straightforward and
flexible models available, while also maintaining close ties to Python
calling and scoping semantics.
endef

define Build/Compile
	$(call Build/Compile/PyMod,,install --prefix=/opt --root=$(PKG_INSTALL_DIR))
endef

define Package/mako/install
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) \
	    $(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
	    $(1)$(PYTHON_PKG_DIR)/
endef

$(eval $(call BuildPackage,mako))
