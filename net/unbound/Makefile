#
# Copyright (C) 2010-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=unbound
PKG_VERSION:=1.6.5
PKG_RELEASE:=1

PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Eric Luehrsen <ericluehrsen@hotmail.com>

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.unbound.net/downloads
PKG_HASH:=e297aa1229015f25bf24e4923cb1dadf1f29b84f82a353205006421f82cc104e

PKG_BUILD_DEPENDS:=libexpat
PKG_BUILD_PARALLEL:=1
PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/unbound/Default
  TITLE:=Validating Recursive DNS Server
  URL:=http://www.unbound.net/
  DEPENDS:=+libopenssl
endef

define Package/unbound
  $(call Package/unbound/Default)
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=IP Addresses and Names
  USERID:=unbound=553:unbound=553
  TITLE+= (daemon)
  DEPENDS+= +libunbound
endef

define Package/unbound/description
  This package contains the Unbound daemon.
endef

define Package/unbound-anchor
  $(call Package/unbound/Default)
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=IP Addresses and Names
  TITLE+= (DSKEY utility)
  DEPENDS+= +unbound +libexpat
endef

define Package/unbound-anchor/description
  This package contains the Unbound anchor utility.
endef

define Package/unbound-control
  $(call Package/unbound/Default)
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=IP Addresses and Names
  TITLE+= (control utility)
  DEPENDS+= +unbound
endef

define Package/unbound-control/description
  This package contains the Unbound control utility.
endef

define Package/unbound-control-setup
  $(call Package/unbound/Default)
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=IP Addresses and Names
  TITLE+= (control setup)
  DEPENDS+= +unbound-control +openssl-util
endef

define Package/unbound-control-setup/description
  This package contains the Unbound control setup utility.
endef

define Package/unbound-host
  $(call Package/unbound/Default)
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=IP Addresses and Names
  TITLE+= (lookup utility)
  DEPENDS+= +libunbound
endef

define Package/unbound-host/description
  This package contains the Unbound DNS lookup utility.
endef

define Package/libunbound
  $(call Package/unbound/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE+= (library)
  DEPENDS+= +libpthread
endef

define Package/libunbound/description
  This package contains the Unbound shared library.
endef

CONFIGURE_VARS += ac_cv_func_getentropy=no

CONFIGURE_ARGS += \
	--disable-dsa \
	--disable-gost \
	--enable-allsymbols \
	--with-libexpat="$(STAGING_DIR)/opt" \
	--with-ssl="$(STAGING_DIR)/opt" \
	--with-pidfile=/opt/var/run/unbound.pid \

define Package/unbound/conffiles
/opt/etc/unbound/unbound.conf
/opt/etc/unbound/unbound_ext.conf
/opt/etc/unbound/unbound_srv.conf
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/include/unbound.h $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/lib/libunbound.{so*,a,la} $(1)/opt/lib/
endef

define Package/unbound/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/sbin/unbound \
		$(PKG_INSTALL_DIR)/opt/sbin/unbound-checkconf \
		$(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/etc/unbound
	$(INSTALL_CONF) \
		$(PKG_INSTALL_DIR)/opt/etc/unbound/unbound.conf \
		$(1)/opt/etc/unbound/
	$(INSTALL_CONF) ./files/root.key $(1)/opt/etc/unbound/
	$(INSTALL_DATA) ./files/unbound_ext.conf $(1)/opt/etc/unbound/unbound_ext.conf
	$(INSTALL_DATA) ./files/unbound_srv.conf $(1)/opt/etc/unbound/unbound_srv.conf
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S61unbound $(1)/opt/etc/init.d/
endef

define Package/unbound-anchor/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/unbound-anchor $(1)/opt/sbin/
endef

define Package/unbound-control/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/unbound-control $(1)/opt/sbin/
endef

define Package/unbound-control-setup/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/unbound-control-setup $(1)/opt/sbin/
endef

define Package/unbound-host/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/unbound-host $(1)/opt/sbin/
endef

define Package/libunbound/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/lib/libunbound.so.* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,unbound))
$(eval $(call BuildPackage,unbound-anchor))
$(eval $(call BuildPackage,unbound-control))
$(eval $(call BuildPackage,unbound-control-setup))
$(eval $(call BuildPackage,unbound-host))
$(eval $(call BuildPackage,libunbound))

