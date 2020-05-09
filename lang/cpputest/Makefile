include $(TOPDIR)/rules.mk

PKG_NAME:=cpputest
PKG_VERSION:=3.7.x
PKG_RELEASE=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/cpputest/cpputest.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=e25097614e1c4856036366877a02346c4b36bb5b
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

PKG_MAINTAINER:=André Valentin <a.valentin@ddimension.net>
PKG_LICENSE:=free

PKG_FIXUP:=autoreconf
PKG_CHECK_FORMAT_SECURITY:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_HOST_OPTIONS += \
	-DCMAKE_SKIP_RPATH=FALSE \
	-DUSE_RPATH="${STAGING_DIR_HOST}/lib"


define Package/cpputest
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=CppUTest is a C /C++ based unit xUnit test framework.
  DEPENDS:=
  ABI_VERSION:=$(PKG_RELEASE)
endef

define Package/cpputest/description
CppUTest is a C /C++ based unit xUnit test framework for unit testing and for test-driving your code. It is written in C++ but is used in C and C++ projects and frequently used in embedded systems but it works for any C/C++ project.
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/include/CppUTest
	$(CP)	$(PKG_INSTALL_DIR)/usr/include/CppUTest/* $(1)/usr/include/CppUTest/
	$(INSTALL_DIR)  $(1)/usr/lib
	$(CP)	$(PKG_INSTALL_DIR)/usr/lib/libCppUTest*.a $(1)/usr/lib/
	$(INSTALL_DIR)  $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/cpputest.pc $(1)/usr/lib/pkgconfig/
endef

$(eval $(call BuildPackage,cpputest))
