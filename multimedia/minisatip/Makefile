#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=minisatip
PKG_VERSION:=1.0.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/catalinii/minisatip/tar.gz/$(PKG_VERSION)?
PKG_HASH:=04d208369331ef0ee165766438a80ed826bb6a6552bbc56a38a6f2dd04603da3

PKG_MAINTAINER:=Daniel Kucera <github@danman.eu>
PKG_LICENSE:=GPL-2.0-or-later

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/minisatip
  TITLE:=SATIP server
  URL:=https://github.com/catalinii/minisatip
  SECTION:=multimedia
  CATEGORY:=Multimedia
  DEPENDS:=+MINISATIP_AES:libopenssl
endef

define Package/minisatip/config
	if PACKAGE_minisatip

		config MINISATIP_AES
			bool "OpenSSL (AES as part of DVBAPI)"
			default n

		config MINISATIP_CLIENT
			bool "SatIP Client"
			default y

	endif
endef

ifeq ($(CONFIG_MINISATIP_AES),)
	CONFIGURE_ARGS += --disable-dvbaes
endif

ifeq ($(CONFIG_MINISATIP_CLIENT),)
	CONFIGURE_ARGS += --disable-satipc
endif

define Package/minisatip/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/minisatip $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/share/minisatip/html/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/html/* $(1)/usr/share/minisatip/html
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/minisatip.init $(1)/etc/init.d/minisatip
endef

$(eval $(call BuildPackage,minisatip))
