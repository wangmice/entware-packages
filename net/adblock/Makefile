#
# Copyright (c) 2015-2017 Dirk Brenken (dev@brenken.org)
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=adblock
PKG_VERSION:=3.0.2
PKG_RELEASE:=1
PKG_LICENSE:=GPL-3.0+
PKG_MAINTAINER:=Dirk Brenken <dev@brenken.org>

include $(INCLUDE_DIR)/package.mk

define Package/adblock
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Powerful adblock script to block ad/abuse domains
	PKGARCH:=all
endef

define Package/adblock/description
Powerful adblock script to block ad/abuse domains via dnsmasq, unbound or bind dns backend.
The script supports many domain blacklist sites plus manual black- and whitelist overrides.
Please see https://github.com/openwrt/packages/blob/master/net/adblock/files/README.md for further information.

endef

define Package/adblock/conffiles
/opt/etc/config/adblock
/opt/etc/adblock/adblock.whitelist
/opt/etc/adblock/adblock.blacklist
endef

define Build/Prepare
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/adblock/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) ./files/adblock.sh $(1)/opt/usr/bin/

	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/adblock.init $(1)/opt/etc/init.d/adblock

	$(INSTALL_DIR) $(1)/opt/etc/config
	$(INSTALL_CONF) ./files/adblock.conf $(1)/opt/etc/config/adblock

	$(INSTALL_DIR) $(1)/opt/etc/adblock
	$(INSTALL_CONF) ./files/adblock.conf $(1)/opt/etc/adblock/adblock.conf.default
	$(INSTALL_CONF) ./files/adblock.blacklist $(1)/opt/etc/adblock/
	$(INSTALL_CONF) ./files/adblock.whitelist $(1)/opt/etc/adblock/
endef

$(eval $(call BuildPackage,adblock))
