# 
# Copyright (C) 2007 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# $Id: $

include $(TOPDIR)/rules.mk

PKG_NAME:=coova-chilli
PKG_VERSION:=1.0.12
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://ap.coova.org/chilli/
PKG_MD5SUM:=365f46fe79b3d76432544d6bc5f37939

include $(INCLUDE_DIR)/package.mk

define Package/coova-chilli
  SUBMENU:=Captive Portals
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+kmod-tun
  TITLE:=Wireless LAN HotSpot controller (Coova Chilli Version)
  URL:=http://coova.org/wiki/index.php/CoovaChilli
endef

define Package/coova-chilli/description
	CoovaChilli is an open source access controller for wireless LAN
	access points and is based on ChilliSpot. It is used for authenticating
	users of a wireless (or wired) LAN. It supports web based login (UAM)
	which is today's standard for public HotSpots and it supports Wireless Protected
	Access (WPA) which is the standard of the future. Authentication,
	authorization and accounting (AAA) is handled by your favorite
	radius server.
endef

define Package/coova-chilli/conffiles
/etc/chilli.conf
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

define Package/coova-chilli/install
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/etc/chilli.conf $(1)/etc/
	$(INSTALL_DIR) $(1)/etc/chilli
	$(CP) $(PKG_INSTALL_DIR)/etc/chilli/* $(1)/etc/chilli/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) $(PKG_INSTALL_DIR)/usr/sbin/chilli* $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,coova-chilli))
