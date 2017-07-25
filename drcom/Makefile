include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/package.mk

PKG_NAME:=drcom
PKG_VERSION:=1.0.0
PKG_RELEASE:=2

define Build/Compile
endef

define Package/drcom
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=DRCOM 3rd client
	PKGARCH:=all
	DEPENDS:=+python-logging +python-openssl +python-codecs
endef

define Package/drcom/description
	DRCOM 3rd client
endef

define Package/drcom/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) ./files/drcom $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) ./files/drcom.conf $(1)/etc/drcom.conf
	$(INSTALL_DIR) $(1)/etc/hotplug.d/iface
	$(INSTALL_DATA) ./files/drcom.hotplug $(1)/etc/hotplug.d/iface/99-drcom
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/drcom.init $(1)/etc/init.d/drcom
endef

$(eval $(call BuildPackage,drcom))
