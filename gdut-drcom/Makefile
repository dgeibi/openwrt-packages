#
# Copyright (C) 2006-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gdut-drcom
PKG_VERSION:=1.6.8
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/chenhaowen01/$(PKG_NAME)/archive
PKG_MD5SUM:=86586eacd0540c994c0f194197d6000e
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_LICENSE:=GPL-3.0+

include $(INCLUDE_DIR)/package.mk
MAKE_PATH:=src

define Package/gdut-drcom
  SECTION:=net
  CATEGORY:=Network
  TITLE:=A third party drcom client openwrt.
  MAINTAINER:=chw
endef

define Package/gdut-drcom/description
	gdut-drcom for openwrt is a third party drcom client openwrt.
endef

define Package/gdut-drcom/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/gdut-drcom $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) ./files/gdut-drcom.conf $(1)/etc/gdut-drcom.conf
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/gdut-drcom.init $(1)/etc/init.d/gdut-drcom
	$(INSTALL_BIN) ./files/gdut-drcom-patch.init $(1)/etc/init.d/gdut-drcom-patch
	$(INSTALL_DIR)  $(1)/etc/hotplug.d/iface
	$(INSTALL_DATA) ./files/gdut-drcom.hotplug $(1)/etc/hotplug.d/iface/99-gdut-drcom
endef

$(eval $(call BuildPackage,gdut-drcom))
