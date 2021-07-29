include $(TOPDIR)/rules.mk

PKG_NAME:=localcustom
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/localcustom-$(PKG_VERSION)
PKG_SOURCE:=$(TOPDIR)/local/feeds/$(PKG_NAME)/src

include $(INCLUDE_DIR)/package.mk

define Package/localcustom/Default
	SECTION:=utils
	CATEGORY:=Base system
	DEPENDS:=$(PKG_DEFAULT_DEPENDS) +libc
	URL:=http://www.demo.com/
endef

define Package/localcustom
	$(call Package/apps/Default)
	TITLE:=Custom package demo of local feeds
endef

define Package/localcustom/description
	localcustom description
endef

define Build/Prepare
	$(CP) $(PKG_SOURCE)/* $(PKG_BUILD_DIR)
endef

define Package/localcustom/extra_provides
	echo libc.so.6
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS) -Wall" \
		LDFLAGS="$(TARGET_LDFLAGS)"
endef

define Package/localcustom/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) $(PKG_BUILD_DIR)/localcustom $(1)/usr/sbin/localcustom

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DIR) $(1)/etc/init.d

	$(CP) ./files/etc/config/localcustom.config $(1)/etc/config/localcustom
	$(CP) ./files/etc/init.d/localcustom.init $(1)/etc/init.d/localcustom
endef

$(eval $(call BuildPackage,localcustom))
