include $(TOPDIR)/rules.mk

PKG_NAME:=captdriver
PKG_VERSION:=0.14
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/mounaiban/captdriver.git
PKG_SOURCE_VERSION:=7906e6d8
PKG_HASH:=('SKIP' '58d3dc5cd1cf6b9e2e44d71885b0f9d5')


TARGET_LDFLAGS+=-Wl,-rpath-link=$(STAGING_DIR)/usr/lib

PKG_MAINTAINER:=Val Kulkov <val.kulkov@gmail.com>
PKG_LICENSE:=FTL GPL-2.0-only MIT ZLIB GPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE.txts
PKG_CPE_ID:=cpe:/a:canon:captdriver
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/captdriver
  CATEGORY:=Network
  SUBMENU:=Printing
  SECTION:=drivers
  TITLE:=A free, high-quality and portable font engine
  URL:=https://github.com/mounaiban/captdriver
  DEPENDS:=+libcups +libstdcpp

endef

define Package/captdriver/description
   Little CMS intends to be an OPEN SOURCE small-footprint color management engine,
   with special focus on accuracy and performance.
   It uses the International Color Consortium standard (ICC),
    which is the modern standard when regarding to color management.
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); \
		aclocal ;\
		autoconf ;\
		automake --add-missing ;\
		./configure --prefix=/usr/ \
	)
endef

define Build/Compile
	($(MAKE) -C $(PKG_BUILD_DIR); \
		cd $(PKG_BUILD_DIR); \
		ppdc -v -d . src/canon-lbp.drv \
	)
endef

define Build/InstallDev
	$(INSTALL_DIR)   $(1)/etc/udev/rules.d 
	$(INSTALL_BIN) ./files/capt.rules   $(1)/etc/udev/rules.d/51-capt.rules
	
	$(INSTALL_DIR)   $(1)/usr/lib/cups/filter
	$(CP) -rf $(PKG_INSTALL_DIR)/usr/bin/rastertocapt  $(1)/usr/lib/cups/filter/rastertocapt

	$(INSTALL_DIR)   $(1)/usr/share/cups/model
	$(CP) -rf $(PKG_BUILD_DIR)/CanonLBP-*.ppd  $(1)/usr/share/cups/model/
endef

define Package/captdriver/install
	$(INSTALL_DIR)   $(1)/etc/udev/rules.d 
	$(INSTALL_BIN) ./files/capt.rules   $(1)/etc/udev/rules.d/51-capt.rules

	$(INSTALL_DIR)   $(1)/usr/lib/cups/filter
	$(CP) -rf $(PKG_INSTALL_DIR)/usr/bin/rastertocapt  $(1)/usr/lib/cups/filter/rastertocapt

	$(INSTALL_DIR)   $(1)/usr/share/cups/model
	$(CP) -rf $(PKG_BUILD_DIR)/CanonLBP-*.ppd  $(1)/usr/share/cups/model/
endef


$(eval $(call BuildPackage,captdriver))

