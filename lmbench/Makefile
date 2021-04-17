#
# Copyright (C) 2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lmbench
PKG_VERSION:=3.0-a4
PKG_REV:=701c6c35b0270d4634fb1dc5272721340322b8ed
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/intel/lmbench.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_MIRROR_HASH:=4f763faa66ff789edc17cb710962e2e1ff281121b36c4311238e8c36c769622e

include $(INCLUDE_DIR)/package.mk

define Package/lmbench
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=lmbench microbenchmarks
	URL:=http://sourceforge.net/projects/lmbench
endef

define Package/lmbench/description
 lmbench is a series of micro benchmarks intended to measure basic operating
 system and hardware system metrics.
endef

MAKE_PATH:=src

LMBENCH_FILES:= \
	bw_file_rd \
	bw_mem \
	bw_mmap_rd \
	bw_pipe \
	bw_tcp \
	bw_unix \
	disk \
	enough \
	flushdisk \
	hello \
	lat_connect \
	lat_ctx \
	lat_fcntl \
	lat_fifo \
	lat_fs \
	lat_http \
	lat_mem_rd \
	lat_mmap \
	lat_ops \
	lat_pagefault \
	lat_pipe \
	lat_proc \
	lat_rpc \
	lat_select \
	lat_sem \
	lat_sig \
	lat_syscall \
	lat_tcp \
	lat_udp \
	lat_unix \
	lat_unix_connect \
	line \
	lmdd \
	lmhttp \
	loop_o \
	memsize \
	mhz \
	msleep \
	par_mem \
	par_ops \
	stream \
	timing_o \
	tlb

define Package/lmbench/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(foreach bin,$(LMBENCH_FILES),$(PKG_BUILD_DIR)/bin/entware/$(bin)) $(1)/opt/bin
endef

$(eval $(call BuildPackage,lmbench))
