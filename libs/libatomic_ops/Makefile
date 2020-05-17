include $(TOPDIR)/rules.mk

PKG_NAME:=libatomic_ops
PKG_VERSION:=7.6.10
PKG_RELEASE=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/ivmai/libatomic_ops.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=7702826f7a8a0aa1b08293322adf49510f4438d1
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

PKG_MAINTAINER:=André Valentin <a.valentin@ddimension.net>
PKG_LICENSE:=free

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_CHECK_FORMAT_SECURITY:=1

include $(INCLUDE_DIR)/package.mk

CONFIGURE_ARGS += \
	--enable-shared

TARGET_CFLAGS += $(FPIC)
MAKE_FLAGS += CFLAGS_O="$(TARGET_CFLAGS)"


define Package/libatomic_ops
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Provides semi-portable access to hardware-provided atomic memory update operations.
  DEPENDS:=
  ABI_VERSION:=$(PKG_RELEASE)
endef

define Package/libatomic_ops/description
This package provides semi-portable access to hardware-provided atomic memory update operations on a number of architectures.
endef

### TO Fix me
define Build/InstallDev
	$(INSTALL_DIR) $(1)
	(cd $(PKG_INSTALL_DIR) && tar -c usr ) | tar -xvC $(1)/
#	$(INSTALL_DIR)  $(1)/usr/lib/pkgconfig
#	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libatomic_ops.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libatomic_ops/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libatomic_ops*so* $(1)/usr/lib/
endef


$(eval $(call BuildPackage,libatomic_ops))
