#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=roc
PKG_VERSION:=0.1.5.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/ddimension/roc.git
PKG_SOURCE_VERSION:=8fabb207460594ac243fd6c6aef92ad09fc1e3b3

PKG_MAINTAINER:=André Valentin <a.valentin@ddimension.net>
PKG_LICENSE:=MPL-2.0

PKG_BUILD_DEPENDS:=scons/host

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include ../../devel/scons/scons.mk

define Package/roc/Default
  DEPENDS+= +openfec +libuv +alsa-lib +libstdcpp +libatomic_ops +libpthread +sox +libunwind +pulseaudio-daemon-avahi $(ICONV_DEPENDS) $(INTL_DEPENDS) 
  URL:=https://roc-project.github.io/
endef

define Package/roc/Default/description
  Roc is a toolkit for real-time audio streaming over the network.
  Basically, Roc is a network transport, highly specialized for the real-time 
  streaming use case. The user writes the stream to the one end and reads it 
  from another end, and Roc deals with all the complexity of the task of 
  delivering data in time and with no loss. Encoding, decoding, adjusting 
  rates, restoring losses - all these are performed transparently under the hood.
  ----YOU MUST INSTALL ragel in your HOST------
endef

define Package/roc
  $(call Package/roc/Default)
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=A toolkit for real-time audio streaming
endef

define Package/roc/description
  $(call Package/roc/Default/description)
  This package contains the roc library and the tools.
endef

SCONS_VARS += \
	LINKFLAGS="$(TARGET_LDFLAGS) -lpulsecommon-13.0"

SCONS_OPTIONS += \
	--with-openfec-includes=$(STAGING_DIR)/usr/include/openfec \
	--with-pulseaudio=$(BUILD_DIR)/pulseaudio-avahi/pulseaudio-13.0 \
	--with-pulseaudio-build-dir=$(BUILD_DIR)/pulseaudio-avahi/pulseaudio-13.0/openwrt-build \
	--enable-pulseaudio-modules \
	--with-includes=$(STAGING_DIR)/usr/include \
	--with-libraries=$(STAGING_DIR)/usr/lib \
	--with-libraries=$(STAGING_DIR)/usr/lib/pulseaudio \
	--disable-doc \
	--host=$(REAL_GNU_TARGET_NAME) \
	--build=$(GNU_HOST_NAME) \
	--prefix=$(PKG_INSTALL_DIR) \
	manbuild=no \
	target="$(TARGET_CROSS:-=)"

define Build/Configure
	(cd $(PKG_BUILD_DIR); \
		$(SCONS_VARS) \
		scons \
			prefix=$(PKG_INSTALL_DIR) \
			$(SCONS_OPTIONS) \
	)
endef

define Package/roc/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/*/roc-send $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/*/roc-recv $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/*/roc-conv $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/*/libroc.so.?.? $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/bin/*/libroc.so $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/bin/*/libroc.so.? $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pulse-13.0/modules
	$(CP) $(PKG_BUILD_DIR)/bin/*/module-roc-sink.so $(1)/usr/lib/pulse-13.0/modules
	$(CP) $(PKG_BUILD_DIR)/bin/*/module-roc-sink-input.so $(1)/usr/lib/pulse-13.0/modules
	$(LN) pulseaudio/libpulsecommon-13.0.so $(1)/usr/lib/libpulsecommon-13.0.so
endef

$(eval $(call BuildPackage,roc))
