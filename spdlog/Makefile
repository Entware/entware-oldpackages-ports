#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=spdlog
PKG_VERSION:=1.15.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/gabime/spdlog/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=15a04e69c222eb6c01094b5c7ff8a249b36bb22788d72519646fb85feb267e67

PKG_MAINTAINER:=
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_FLAGS:=lto
CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/spdlog
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=spdlog
  URL:=https://github.com/gabime/spdlog
  DEPENDS:=+libfmt
  BUILDONLY:=1
endef

define Package/spdlog/description
  Very fast, header-only/compiled, C++ logging library.
endef

CMAKE_OPTIONS += \
	-DSPDLOG_BUILD_SHARED=OFF \
	-DSPDLOG_BUILD_EXAMPLE=OFF \
	-DSPDLOG_BUILD_EXAMPLE_HO=OFF \
	-DSPDLOG_BUILD_TESTS=OFF \
	-DSPDLOG_BUILD_TESTS_HO=OFF \
	-DSPDLOG_BUILD_BENCH=OFF \
	-DSPDLOG_SANITIZE_ADDRESS=OFF \
	-DSPDLOG_INSTALL=ON \
	-DSPDLOG_FMT_EXTERNAL=ON \
	-DSPDLOG_FMT_EXTERNAL_HO=OFF \
	-DSPDLOG_NO_EXCEPTIONS=OFF

$(eval $(call BuildPackage,spdlog))
