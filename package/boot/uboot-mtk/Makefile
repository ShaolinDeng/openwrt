include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=uboot-mtk
PKG_RELEASE:=1
PR_NAME=LEDEMT7620N

include $(INCLUDE_DIR)/local-development.mk
PKG_VERSION:=4.3.0.0

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

UBOOT_MAKE_OPTS:= \
    LZMA=$(STAGING_DIR_HOST)/bin/lzma \
    ARCH=mips \
    CPU=mips \
    CROSS_COMPILE=$(TARGET_CROSS)

define Package/uboot-mtk
	CATEGORY:=Boot Loaders
	TITLE:=MTK uboot
	DEPENDS:=@TARGET_ramips
endef

define Package/uboot-mtk/description
	MTK uboot
endef

define Build/Configure
	cp -rf configs/$(PR_NAME)/* $(PKG_BUILD_DIR)
	cp $(PKG_BUILD_DIR)/$(PR_NAME)_defconfig $(PKG_BUILD_DIR)/.config
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CROSS_COMPILE=$(TARGET_CROSS)
endef

define Package/uboot-mtk/install
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/uboot.bin $(BUILD_DIR)/../../bin/targets/$(BOARD)/$(SUBTARGET)/
endef

$(eval $(call BuildPackage,uboot-mtk))
