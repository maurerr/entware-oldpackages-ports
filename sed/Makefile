#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=sed
PKG_VERSION:=4.7
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@GNU/$(PKG_NAME)
PKG_HASH:=2885768cd0a29ff8d58a6280a270ff161f6a3deb5690b2be6c49f46d4c67bd6a

include $(INCLUDE_DIR)/package.mk

define Package/sed
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=GNU streams editor
  URL:=http://sed.sf.net
endef

define Package/sed/description
 Sed (streams editor) takes text input and performs some operation
 (or set of operations) on it and outputs the modified text.
endef

CONFIGURE_ARGS += \
	--without-libiconv-prefix \
	--without-libintl-prefix \
	--disable-acl

MAKE_FLAGS += \
	CFLAGS="$(TARGET_CFLAGS) -I$(STAGING_DIR)/opt/include" \
	PREFIX="/opt" \
	HOST="$(GNU_TARGET_NAME)" \

define Package/sed/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sed/sed $(1)/opt/bin
endef

$(eval $(call BuildPackage,sed))
