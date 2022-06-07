include $(TOPDIR)/rules.mk

PKG_NAME:=cndrvcups-capt
PKG_VERSION:=2.71
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/xfront/openwrt-print-drivers/raw/master/canon/
PKG_HASH:=skip


TARGET_LDFLAGS+=-Wl,-rpath-link=$(STAGING_DIR)/usr/lib

PKG_MAINTAINER:=Val Kulkov <val.kulkov@gmail.com>
PKG_LICENSE:=FTL GPL-2.0-only MIT ZLIB GPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE.txts
PKG_CPE_ID:=cpe:/a:canon:cndrvcups-capt
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/cndrvcups-capt
  CATEGORY:=Network
  SUBMENU:=Printing
  SECTION:=drivers
  TITLE:=A free, high-quality and portable font engine
  URL:=https://www.canon.com.cn/
  DEPENDS:=+libcups +libstdcpp

endef

define Package/cndrvcups-capt/description
   Little CMS intends to be an OPEN SOURCE small-footprint color management engine,
   with special focus on accuracy and performance.
   It uses the International Color Consortium standard (ICC),
    which is the modern standard when regarding to color management.
endef

define Build/Configure
    (cd $(PKG_BUILD_DIR); \
		./allgen.sh \
	)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) all
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/share
	$(CP)  -rf $(PKG_INSTALL_DIR)/usr/share/* $(1)/usr/share/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) -rf $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
endef

define Package/cndrvcups-capt/install
	$(INSTALL_DIR) $(1)/usr/share
	$(CP)  -rf $(PKG_INSTALL_DIR)/usr/share/* $(1)/usr/share/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) -rf $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,cndrvcups-capt))

