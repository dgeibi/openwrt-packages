include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/package.mk

PKG_NAME:=gdut-drcom
PKG_VERSION:=1.6
PKG_RELEASE:=0
PKG_MAINTAINER:=CHW

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

define Package/gdut-drcom
	SECTION:=utils
	CATEGORY:=Utilities
	DEFAULT:=y
	TITLE:=gdut-drcom -- a third-party drcom client for gdut
#	DEPENDS:=+libgcrypt
#	DEPENDS:=+libopenssl
#	DEPENDS:=+libpolarssl
endef

define Build/Prepare
	@echo "############## Build/Prepare"
	$(Build/Prepare/Default)
	$(CP) ./src/* $(PKG_BUILD_DIR)
endef

define Build/Compile
	@echo "############## Build/Compile"
	export CFLAGS="$CFLAGS -DDEBUG"
#	$(call Build/Compile/Default, cryptlib=openssl)
	$(call Build/Compile/Default)
endef

define Package/gdut-drcom/postinst
#!/bin/sh
echo "post install: patching ppp.sh"
sed -i '/#added by gdut-drcom/d' /lib/netifd/proto/ppp.sh
sed -i '/proto_run_command/i username=$$(echo -e "\\r\\n$$username")    #added by gdut-drcom!' /lib/netifd/proto/ppp.sh
echo "patched!"
endef

define Package/gdut-drcom/prerm
#!/bin/sh
echo "pre remove: unpatching ppp.sh!"
sed -i '/#added by gdut-drcom/d' /lib/netifd/proto/ppp.sh
echo "unpatched!"
endef

define Package/gdut-drcom/install
	@echo "############## Package/gdut-drcom/install"
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/gdut-drcom $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) ./files/gdut-drcom.conf $(1)/etc/gdut-drcom.conf
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/gdut-drcom.init $(1)/etc/init.d/gdut-drcom
	$(INSTALL_DIR)  $(1)/etc/hotplug.d/iface
	$(INSTALL_DATA) ./files/gdut-drcom.hotplug $(1)/etc/hotplug.d/iface/99-gdut-drcom
endef

$(eval $(call BuildPackage,gdut-drcom))
