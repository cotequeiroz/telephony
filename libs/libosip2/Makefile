#
# Copyright (C) 2014 - 2018 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libosip2
PKG_VERSION:=5.1.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@GNU/osip
PKG_HASH:=2bc0400f21a64cf4f2cbc9827bf8bdbb05a9b52ecc8e791b4ec0f1f9410c1291

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_LICENSE:=LGPL-2.1+
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk

define Package/libosip2
  SUBMENU:=Telephony
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=GNU oSIP library
  URL:=http://www.gnu.org/software/osip/
  ABI_VERSION:=13
  DEPENDS:=+librt
endef

define Package/libosip2/description
 GNU oSIP library, a Session Initiation Protocol (SIP) implementation.
endef

# toolchain __arc__ define conflicts with libosip2 source
TARGET_CFLAGS += $(if $(CONFIG_arc),-U__arc__)

CONFIGURE_ARGS += \
	--enable-shared \
	--enable-static \
	--disable-silent-rules \
	--disable-trace \
	--disable-mpatrol \
	--disable-gprof \
	--disable-mt \
	--enable-pthread \
	--enable-semaphore \
	--disable-gperf \
	--disable-test \
	--disable-minisize

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/osip{,parser}2 $(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libosip{,parser}2.{a,so*} $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libosip2.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libosip2/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libosip{,parser}2.so.$(ABI_VERSION)* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libosip2))
