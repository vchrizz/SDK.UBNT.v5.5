#
# Copyright (C) 2006-2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# $Id: Makefile 11647 2008-07-05 12:33:14Z florian $

include $(TOPDIR)/rules.mk

PKG_NAME:=hdparm
PKG_VERSION:=8.9
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/$(PKG_NAME)
PKG_MD5SUM:=19fa013956612581af7d00907990ac84

include $(INCLUDE_DIR)/package.mk

define Package/hdparm
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Hard disk drive configuration utilitity
  URL:=http://sourceforge.net/projects/hdparm/
endef

define Package/hdparm/description
	Tune hard disk parameters for high performance.
	Get/set hard disk parameters for Linux IDE drives.
	Primary use is for enabling irq-unmasking and IDE multiplemode.
endef

MAKE_FLAGS += \
	CFLAGS="$(EXTRA_CFLAGS)" \
	LDFLAGS="$(EXTRA_LDFLAGS)" \

define Package/hdparm/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/sbin
endef

$(eval $(call BuildPackage,hdparm))
