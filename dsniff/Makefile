#
# Copyright (C) 2006 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2002

include $(TOPDIR)/rules.mk

PKG_NAME:=dsniff
PKG_VERSION:=2.4b1
PKG_RELEASE:=4a

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.monkey.org/~dugsong/dsniff/beta
PKG_HASH:=a9803a7a02ddfe5fb9704ce86f0ffc48453c321e88db85810db411ba0841152a

PKG_BUILD_DEPENDS:=nfs-kernel-server/host

# Make host rpcgen first
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-2.4

include $(INCLUDE_DIR)/package.mk

define Package/dsniff
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libnids +libopenssl +libgdbm
  TITLE:=A collection of tools for network auditing and penetration testing
  URL:=http://www.monkey.org/~dugsong/dsniff/
endef

define Package/dsniff/description
	A collection of tools for network auditing and penetration testing.
endef

CONFIGURE_ARGS += \
	--with-gdbm="$(STAGING_DIR)/opt" \
	--with-libnids="$(STAGING_DIR)/opt" \
	--with-libpcap="$(STAGING_DIR)/opt" \
	--with-libnet="$(STAGING_DIR)/opt" \
	--with-openssl="$(STAGING_DIR)/opt" \
	--without-db \
	--without-x

TARGET_CFLAGS += -D_DEFAULT_SOURCE

# Modify PATH to use host rpcgen
define Build/Compile
	PATH="$(STAGING_DIR_HOSTPKG)/bin:$(TARGET_PATH)" \
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
		install_prefix="$(PKG_INSTALL_DIR)" \
		all install
endef

define Package/dsniff/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/* $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP)  $(PKG_INSTALL_DIR)/opt/lib/* $(1)/opt/lib
endef

$(eval $(call BuildPackage,dsniff))
