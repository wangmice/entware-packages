#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Upgraded from devel-20151125 rev. e2065bf0fc22ba33001ad503c01bba01648024a8

include $(TOPDIR)/rules.mk

PKG_NAME:=xl2tpd
PKG_VERSION:=1.3.8
PKG_RELEASE:=1
PKG_MAINTAINER:=Yousong Zhou <yszhou4tech@gmail.com>
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=LICENSE

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/xelerance/xl2tpd.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=cec1ebe1523bf248f134647dd6030a333d93e19b
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/xl2tpd
  SECTION:=net
  CATEGORY:=Network
  TITLE:=An L2TP (Layer 2 Tunneling Protocol) daemon
  URL:=http://www.xelerance.com/software/xl2tpd/
  SUBMENU:=VPN
  DEPENDS:=+ppp
endef

define Package/xl2tpd/description
l2tpd is the open source implementation of the L2TP tunneling protocol (RFC2661).
It does implement both LAC and LNS role in a L2TP networking architecture. The
main goal of this protocol is to tunnel PPP frame trough an IP network.
endef

# Use optimization options from OpenWrt build system
MAKE_FLAGS += OFLAGS=""

ifneq (0,0)
  # debugging options from Makefile of xl2tpd package
  EXTRA_CFLAGS += \
	-DDEBUG_ZLB \
	-DDEBUG_HELLO \
	-DDEBUG_CLOSE \
	-DDEBUG_FLOW \
	-DDEBUG_FILE \
	-DDEBUG_AAA \
	-DDEBUG_PAYLOAD \
	-DDEBUG_CONTROL \
	-DDEBUG_PPPD \
	-DDEBUG_HIDDEN \
	-DDEBUG_ENTROPY \
	-DDEBUG_CONTROL_XMIT \
	-DDEBUG_MAGIC \
	-DDEBUG_FLOW_MORE \
	-DDEBUG_AUTH
endif

define Package/xl2tpd/conffiles
/opt/etc/xl2tpd/xl2tpd.conf
/opt/etc/xl2tpd/xl2tp-secrets
/opt/etc/ppp/options.xl2tpd
/opt/etc/ppp/chap-secrets
/opt/etc/ppp/ip-up.sh
/opt/etc/ppp/ip-down.sh
endef

define Package/xl2tpd/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/local/sbin/xl2tpd $(1)/opt/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/local/sbin/xl2tpd-control $(1)/opt/sbin/

	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S20xl2tpd $(1)/opt/etc/init.d/

	$(INSTALL_DIR) $(1)/opt/etc/xl2tpd
	$(INSTALL_DATA) ./files/xl2tpd.conf $(1)/opt/etc/xl2tpd/
	$(INSTALL_CONF) ./files/xl2tp-secrets $(1)/opt/etc/xl2tpd/

	$(INSTALL_DIR) $(1)/opt/etc/ppp
	$(INSTALL_CONF) ./files/chap-secrets $(1)/opt/etc/ppp/chap-secrets
	$(INSTALL_DATA) ./files/options.xl2tpd $(1)/opt/etc/ppp/options.xl2tpd
	$(INSTALL_BIN) ./files/ip-up.sh $(1)/opt/etc/ppp/
	$(INSTALL_BIN) ./files/ip-down.sh $(1)/opt/etc/ppp/
	$(INSTALL_DIR) $(1)/opt/var/run
endef

$(eval $(call BuildPackage,xl2tpd))
