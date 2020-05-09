#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=openfec
PKG_VERSION:=1.4.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)_v1_4_2.tgz
PKG_SOURCE_URL:=http://openfec.org/files/
PKG_HASH:=ccf1252b548505d198de768609c08c722a35e580c53b843e4372b7c52674ce12
PKG_BUILD_DIR := $(BUILD_DIR)/openfec_v1.4.2
PKG_MAINTAINER:=André Valentin <a.valentin@ddimension.net>
PKG_LICENSE:=CeCILL
PKG_CHECK_FORMAT_SECURITY:=0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_INSTALL:=1

define Package/openfec
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Openfec Library for error correction
  DEPENDS:=
endef

TARGET_CFLAGS += -I$(STAGING_DIR)/usr/include

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/bin/Release/lib*.so $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/bin/Release/lib*.so.1 $(1)/usr/lib/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/Release/lib*.so.1.4.2 $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/include/openfec
	(cd $(PKG_BUILD_DIR)/src/ && tar -c .) | tar -xvC $(1)/usr/include/openfec/
endef

define Build/Install
endef

define Package/openfec/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/bin/Release/lib*.so $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/bin/Release/lib*.so.1 $(1)/usr/lib/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/Release/lib*.so.1.4.2 $(1)/usr/lib/
endef

$(eval $(call BuildPackage,openfec))
