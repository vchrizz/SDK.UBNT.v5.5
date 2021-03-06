#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# $Id: Makefile 15321 2009-04-21 11:38:28Z nico $

include $(TOPDIR)/rules.mk

PKG_NAME:=bind
PKG_VERSION:=9.5.0-P1
PKG_RELEASE:=1.1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:= \
	ftp://ftp.isc.org/isc/bind9/$(PKG_VERSION) \
	http://www.mirrorservice.org/sites/ftp.isc.org/isc/bind9/$(PKG_VERSION)
PKG_MD5SUM:=a4f9dd6d205d24ec89fa4e44d8188197

include $(INCLUDE_DIR)/package.mk

define Package/bind/Default
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+bind-libs +libopenssl
  TITLE:=bind
  URL:=http://www.isc.org/sw/bind/
  SUBMENU:=DNS
endef

define Package/bind-libs
  SECTION:=net
  CATEGORY:=Network
  TITLE:=bind shared libraries
  URL:=http://www.isc.org/sw/bind/
  SUBMENU:=DNS
endef

define Package/bind-server
  $(call Package/bind/Default)
  TITLE+= DNS server
endef

define Package/bind-client
  $(call Package/bind/Default)
  TITLE+= dynamic DNS client
endef

define Package/bind-tools
  $(call Package/bind/Default)
  TITLE+= administration tools (all)
endef
  
define Package/bind-rndc
  $(call Package/bind/Default)
  TITLE+= administration tools (rndc and rndc-confgen only)
endef

define Package/bind-check
  $(call Package/bind/Default)
  TITLE+= administration tools (named-checkconf and named-checkzone only)
endef

define Package/bind-dnssec
  $(call Package/bind/Default)
  TITLE+= administration tools (dnssec-keygen and dnssec-signzone only)
endef

define Package/bind-host
  $(call Package/bind/Default)
  TITLE+= simple DNS client
endef

define Package/bind-dig
  $(call Package/bind/Default)
  TITLE+= DNS excavation tool
endef

export BUILD_CC="$(TARGET_CC)"

CONFIGURE_ARGS += \
		--enable-shared \
		--enable-static \
		--enable-ipv6 \
		--with-randomdev="/dev/urandom" \
		--disable-threads \
		--with-openssl="$(STAGING_DIR)/usr" \
		--with-libtool \
		--with-libxml2=no \
		, \
		BUILD_CC="$(TARGET_CC)" \

define Build/Compile
	rm -rf $(PKG_INSTALL_DIR)
	mkdir -p $(PKG_INSTALL_DIR)
	$(MAKE) -C $(PKG_BUILD_DIR)/lib/dns \
		BUILD_CC="$(HOSTCC)" \
		CC="$(HOSTCC)" \
		CFLAGS="-O2" \
		LIBS="" \
		gen
	$(MAKE) -C $(PKG_BUILD_DIR) \
	DESTDIR="$(PKG_INSTALL_DIR)" \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

define Package/bind-libs/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib
endef

define Package/bind-server/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/named $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc
	$(CP) ./files/bind $(1)/etc/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/named.init $(1)/etc/init.d/named
	find $(1)/etc/bind/ -name ".svn" | xargs rm -rf
endef

define Package/bind-client/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/nsupdate $(1)/usr/bin/
endef

define Package/bind-tools/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/dig $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/host $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/dnssec-keygen $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/dnssec-signzone $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/named-checkconf $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/named-checkzone $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/rndc $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/rndc-confgen $(1)/usr/sbin/
endef

define Package/bind-rndc/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/rndc $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/rndc-confgen $(1)/usr/sbin/
endef

define Package/bind-check/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/named-checkconf $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/named-checkzone $(1)/usr/sbin/
endef

define Package/bind-dnssec/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/dnssec-keygen $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/dnssec-signzone $(1)/usr/sbin/
endef

define Package/bind-host/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/host $(1)/usr/bin/
endef

define Package/bind-dig/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/dig $(1)/usr/bin/
endef

$(eval $(call BuildPackage,bind-libs))
$(eval $(call BuildPackage,bind-server))
$(eval $(call BuildPackage,bind-client))
$(eval $(call BuildPackage,bind-tools))
$(eval $(call BuildPackage,bind-rndc))
$(eval $(call BuildPackage,bind-check))
$(eval $(call BuildPackage,bind-dnssec))
$(eval $(call BuildPackage,bind-host))
$(eval $(call BuildPackage,bind-dig))
