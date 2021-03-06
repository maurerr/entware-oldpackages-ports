#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Dependencies checker was turned off here to avoid pulling optional deps

include $(TOPDIR)/rules.mk

PKG_NAME:=weechat
PKG_VERSION:=2.6
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://weechat.org/files/src
PKG_HASH:=fa9e3130e7afdfb6eff1b7892caac3efdd38a442f9989ca8c061eced2c755148

PKG_BUILD_DEPENDS:=perl python

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/weechat
  SUBMENU:=Instant Messaging
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Lightweight IRC client
  URL:=https://weechat.org/
  DEPENDS:= +libcurl +libgnutls +libgcrypt +libaspell +libncursesw \
	$(ICONV_DEPENDS) $(INTL_DEPENDS)
endef

define Package/weechat/description
 Weechat is fast, light & extensible IRC client.
endef

TARGET_LDFLAGS += \
	-lintl -liconv

CMAKE_OPTIONS+= \
	-DWEECHAT_HOME="/opt/var/weechat" \
	-DCA_FILE="/opt/etc/ssl/certs/ca-certificates.crt" \
	-DPYTHON_EXECUTABLE="$(STAGING_DIR)/host/bin/python2.7" \
	-DPYTHON_INCLUDE_PATH="$(STAGING_DIR)/opt/include/python2.7" \
	-DPYTHON_LIBRARY="$(STAGING_DIR)/opt/lib/libpython2.7.so" \
	-DPERL_EXECUTABLE:FILEPATH="$(STAGING_DIR)/host/bin/perl" \
	-DPERL_INCLUDE_PATH="$(STAGING_DIR)/opt/lib/perl5/5.28/CORE" \
	-DPERL_LIBRARY="$(STAGING_DIR)/opt/lib/perl5/5.28/CORE/libperl.so" \
	-DENABLE_JAVASCRIPT=OFF \
	-DENABLE_LUA=OFF \
	-DENABLE_GUILE=OFF \
	-DENABLE_RUBY=OFF \
	-DENABLE_TCL=OFF

define CheckDependencies
endef

define Package/weechat/install
	$(INSTALL_DIR) $(1)/opt/bin $(1)/opt/var/weechat
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/weechat-curses $(1)/opt/bin
	ln -sf weechat-curses $(1)/opt/bin/weechat
	$(INSTALL_DIR) $(1)/opt/lib/weechat/plugins
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/weechat/plugins/*.so \
		$(1)/opt/lib/weechat/plugins
endef

define Package/weechat/postinst
#!/bin/sh
cat << EOF
Please install optional dependencies first if you want to use weechat scripts.

* for Perl scripts:
opkg install perl

* for Python scripts:
opkg install python-light
EOF
endef

$(eval $(call BuildPackage,weechat))
