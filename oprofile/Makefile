#
# Copyright (C) 2009-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=oprofile
PKG_VERSION:=1.3.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/oprofile/
PKG_HASH:=95ded8bde1ec39922f0af015981a67aec63e025a501e4dc04cd65d38f73647e6

PKG_MAINTAINER:=Felix Fietkau <nbd@openwrt.org>

PKG_BUILD_DEPENDS:=binutils
PKG_LICENSE:=GPL-2.0+
PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/nls.mk

define Package/oprofile
  SECTION:=devel
  CATEGORY:=Development
  TITLE:=OProfile System Profiler
  URL:=http://oprofile.sourceforge.net
  DEPENDS:=+libpopt +libstdcpp +objdump +librt @!LINUX_2_6_22
endef

define Package/oprofile/description
 A transparent low-overhead system-wide profiler.
endef

define Package/oprofile-utils
  SECTION:=devel
  CATEGORY:=Development
  TITLE:=OProfile System Profiler (extra utilities)
  URL:=http://oprofile.sourceforge.net
  DEPENDS:=oprofile
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--with-kernel-support \
		--without-x \
	)
endef

TARGET_CXXFLAGS += -fpermissive
TARGET_LDFLAGS := -L$(STAGING_DIR)/opt/lib $(TARGET_LDFLAGS)

define Package/oprofile-utils/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/bin/opannotate \
		$(PKG_INSTALL_DIR)/opt/bin/oparchive \
		$(PKG_INSTALL_DIR)/opt/bin/opgprof \
		$(1)/opt/bin
endef

define Package/oprofile/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/bin/* \
		$(1)/opt/bin

	rm -f \
		$(1)/opt/bin/opannotate \
		$(1)/opt/bin/oparchive \
		$(1)/opt/bin/opgprof

	$(INSTALL_DIR) $(1)/opt/lib/oprofile
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/oprofile/*.so* \
		$(1)/opt/lib/oprofile/

	$(INSTALL_DIR) $(1)/opt/share/oprofile
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/share/oprofile/stl.pat \
		$(PKG_INSTALL_DIR)/opt/share/oprofile/ \
		$(1)/opt/share/oprofile/
endef

$(eval $(call BuildPackage,oprofile))
$(eval $(call BuildPackage,oprofile-utils))
