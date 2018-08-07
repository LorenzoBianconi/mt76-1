================================================================================
Jeff Lancaster
Komodo Systems, LLC
2018-08-07
================================================================================
Introduction:
This code is based on the openwrt/mt76 package. Using mt76x2e driver we created
the new mt76x0e driver which is a device used on the wr92ac v3 hardware and of
which is our motivation to do so. We lifted the entire pacakge and simply added
the mt76x0e driver to it.
================================================================================

Build instructions for the wr902ac v3 with mt7610e driver
---------------------------------------------------------
cd <your-workdir>
git clone https://git.lede-project.org/source.git
git clone https://github.com/Komodowifi/mt76.git
cd source
patch -p1 --dry-run < ../../mt76/docs/patches/openwrt-package-kernel-mt76-mt7610e.patch
patch -p1 < ../../mt76/docs/patches/openwrt-package-kernel-mt76-mt7610e.patch

make menuconfig
Target System (MediaTek Ralink MIPS)  --->
	Subtarget (MT76x8 based boards)  --->
	Target Profile (TP-Link TL-WR902AC v3)  --->

In 
Kernel modules ---> Wireless Drivers --->
	<*> kmod-mt76........... MediaTek MT76x2/MT7603 wireless driver (metapackage) (NEW)
	-*- kmod-mt76-core........................... MediaTek MT76xx wireless driver
	< > kmod-mt7601u................... MT7601U-based USB dongles Wireless Driver (NEW)
	-*- kmod-mt7603.............................. MediaTek MT7603 wireless driver
	<M> kmod-mt76x0.............................. MediaTek MT76x0 wireless driver
	-*- kmod-mt76x2.............................. MediaTek MT76x2 wireless driver
Exit
Save
make

To upgrade or update a board use:
./bin/targets/ramips/mt76x8/openwrt-ramips-mt76x8-tplink_tl-wr902ac-v3-squashfs-sysupgrade.bin

To upgrade or recover to the new image using tftp:
./bin/targets/ramips/mt76x8/openwrt-ramips-mt76x8-tplink_tl-wr902ac-v3-squashfs-tftp-recovery.bin


================================================================================
