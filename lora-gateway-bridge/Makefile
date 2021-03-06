include $(TOPDIR)/rules.mk

PKG_NAME:=lora-gateway-bridge
PKG_VERSION:=3.2.1
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://codeload.github.com/brocaar/lora-gateway-bridge/tar.gz/v$(PKG_VERSION)?
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz

PKG_HASH:=833650be9fb8d1125ddbb99d33fb580c0c96bb19ca8021a8fde368f4c5fac917
PKG_MAINTAINER:=Xue Liu <liuxuenetmail@gmail.com>
PKG_LICENSE:MIT
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

GO_PKG:=github.com/brocaar/lora-gateway-bridge
GO_PKG_BUILD_PKG:=github.com/brocaar/lora-gateway-bridge/cmd/lora-gateway-bridge

include $(INCLUDE_DIR)/package.mk
# golang-package.mk should be relocate regarding the env
include $(INCLUDE_DIR)/../feeds/packages/lang/golang/golang-package.mk

define Package/lora-gateway-bridge
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=LoRaWAN
  TITLE:=LoRa Gateway Bridge
  DEPENDS:=$(GO_ARCH_DEPENDS) +mosquitto-ssl
  PKGARCH:=all
endef

define Package/lora-gateway-bridge/description
  LoRa Gateway Bridge is a service which converts LoRa packet-forwarder 
  protocols into a LoRa Server common protocol (JSON and Protobuf).
  This project is part of the LoRa Server project.
endef

GO_PKG_LDFLAGS:=-s -w
GO_PKG_LDFLAGS_X:=main.version=$(PKG_VERSION)

define Package/lora-gateway-bridge/install
	$(call GoPackage/Package/Install/Bin,$(1))

	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/lora-gateway-bridge.init $(1)/etc/init.d/lora-gateway-bridge

	$(INSTALL_DIR) $(1)/etc/lora-gateway-bridge
	$(INSTALL_DATA) ./files/lora-gateway-bridge.toml $(1)/etc/lora-gateway-bridge/
endef

$(eval $(call GoBinPackage,lora-gateway-bridge))
$(eval $(call BuildPackage,lora-gateway-bridge))
