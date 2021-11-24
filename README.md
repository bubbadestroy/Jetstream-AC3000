More reason  than ever to wipe that firmware and install fresh openwrt.

# 2021-NOV SAFETY AND PRIVACY NOTICE  RCE – CVE-2020-10971 and CVE-2020-10972****

https://james-clee.com/2020/04/18/multiple-wavlink-vulnerabilities/

No suprise, the apps for said devices should be assumed to be a tool for backdoor as well

## Walmart-exclusive routers can control devices via hidden backdoors (Wavlink, Jetstream, Ematic)

https://youtu.be/K-o0U8sQh-c


# DIRTY FLASH OPENWRT on the following and shut the stock firmware backdoor for good.


https://git.openwrt.org/?p=openwrt/openwrt.git;a=commit;h=51b653de94e7e5006b5480df33d5dfd9de824cc7

## *Note* As of now 5ghz module on radio2 seems to not cleanly flash with the below method. It would require building openwrt from 'make menu' command with that module selected in the build options.


Model Difference Statement: "We would like to confirm the models:
https://www.youtube.com/watch?v=K-o0U8sQh-c&t=13s
    • WS-WN536A8, WS-WN533A8, ARK T6, Quantum Max, Quantum T10, Quantum T12,
    • Quantum D4C, Quantum D4, Quantum D6Q, Quantum D6, Quantum T8, Quantum T6
    are same in all respects. Only the model name and appearance is different.
    The model WS-WN536A8 is the tested sample."

https://fccid.io/NZ3-WN536A8/Letter/Model-Difference-Statement-3975614

  ## Bubba finally destroy stock firmware and destroy the flash, but fix it easy with luci intact!
 ## Thanks everyone mentioned below and those who I don't know yet to credit.. .. So glad this got done! 
## Jetstream-AC3000 
## EMATIC ERAC3000 
## WAVLINK 
## WINSTAR 
## WINSTARS 



 instructions to work for the above router Openwrt for Wavlink WL-WN531A6 ( or whatever your similiar model is )
 (they are all the same)

  https://openwrt.org/toh/wavlink/wavlink_wl-wn531a6

https://git.openwrt.org/?p=openwrt/openwrt.git;a=commit;h=51b653de94e7e5006b5480df33d5dfd9de824cc7

# Suggested that you backup your config and then factory reset first.
# Format a FAT32 USB and place it in the WS-WN536A8 usb
# go to the following address

  192.168.10.1/webcmd.shtml

# copy and paste this

  dd if=/dev/mtd4ro of=/media/sda1/firmware.bin

Backup the OEM Firmware:
-----------------------

There isn't any firmware released for the WS-WN536A8 on
the Wavlink/Winstar/Ematic web site. Reverting back to the OEM firmware is
not possible unless we have a backup of the original OEM
firmware.

The OEM firmware is stored on /dev/mtd4 ("Kernel").

  1) Plug a FAT32 formatted USB flash drive into the USB port.
  2) Navigate to "Setup->USB Storage". Under the "Available
     Network folder" you can see part of the mount point of
     the newly mounted flash drive filesystem - e.g "sda1".
     The full mount point is prefixed with "/media", so in
     this case the mount point becomes "/media/sda1".
  3) Go to http://192.168.10.1/webcmd.shtml .
  4) Type the following line in the "Command" input box:

     dd if=/dev/mtd4ro of=/media/sda1/firmware.bin

  5) Click "Apply"
  6) After few seconds, in the text area should appear this
     output:

        30080+0 records in
      30080+0 records out

  7) Type "sync" in the "Command" input box and click "Apply".
  8) At this point the OEM firmware is stored on the flash
     drive as "firmware.bin". The size of the file is 15040 KB.

# Last chance to look around the old shit interface 
# ls -la or whatever you want from
http://192.168.10.1/webcmd.shtml

	-rwxr-xr-x    1 0        0           62384 nas.cgi
-rwxr-xr-x    1 0        0           66847 login.cgi
-rwxr-xr-x    1 0        0           18963 upload.cgi
-rwxr-xr-x    1 0        0          105596 adm.cgi
-rwxr-xr-x    1 0        0           61945 mesh.cgi
-rwxr-xr-x    1 0        0           17469 upload_settings.cgi
-rwxr-xr-x    1 0        0            1057 ExportLogs.sh
-rwxr-xr-x    1 0        0           96964 wireless.cgi
-rwxr-xr-x    1 0        0           97216 firewall.cgi
-rwxr-xr-x    1 0        0           80013 internet.cgi
-rwxr-xr-x    1 0        0           61923 touchlist_sync.cgi
-rwxr-xr-x    1 0        0            9015 live_api.cgi
-rwxr-xr-x    1 0        0           62841 upload_uboot.cgi
-rwxr-xr-x    1 0        0             551 ExportAllSettings.sh
-rwxr-xr-x    1 0        0           57950 applogin.cgi
-rwxr-xr-x    1 0        0           93639 makeRequest.cgi
-rwxr-xr-x    1 0        0           57482 ddns.cgi


## WARNING ( I had no LUCI at first, but found the work around just fine and now have luci )



Installation:
------------

* Flashing instructions (OEM web interface):
The OEM web interface accepts only files with names containing
"WN536A8". It's also impossible to flash the *-sysupgrade.bin
image, so we have to flash the *-initramfs-kernel.bin first and
use the OpenWrt's upgrade interface to write the sysupgrade
image.

  1) Rename openwrt-ramips-mt7621-wavlink_wl-wn531a6-initramfs-kernel.bin
     to WS-WN536A8.bin.
  2) Connect your computer to the one of the LAN ports of the
     router with an Ethernet cable and open http://192.168.10.1
  3) Browse to Setup -> Firmware Upgrade interface.
  4) Upload the (renamed) OpenWrt image - WN536A8.bin.
  5) Proceed with the firmware installation and give the device
     a few minutes to finish and reboot.
# I didnt have LUCI at first so..
# WARNING The next few steps are due to the original guide comming from another model (same hardware, but be warned, likely bugs) make sure to be in /tmp directory


Go to a powershell or use putty 

ping 192.168.1.1
ctrl-c
ssh root@192.168.1.1
cd /temp
wget http://downloads.openwrt.org/snapshots/targets/ramips/mt7621/openwrt-ramips-mt7621-wavlink_wl-wn531a6-squashfs-sysupgrade.bin
sysupgrade openwrt-ramips-mt7621-wavlink_wl-wn531a6-squashfs-sysupgrade.bin


# and wait for some time to let it get an ip or

sync
ping 192.168.1.1
ctrl-c
ssh root@192.168.1.1
cd /temp

opkg install  uhttpd uhttpd-mod-ubus libiwinfo-lua luci-base luci-app-firewall luci-mod-admin-full luci-theme-bootstrap

sync


root@OpenWrt:/# dmesg
[    0.000000] Linux version 5.4.61 (builder@buildhost) (gcc version 8.4.0 (OpenWrt GCC 8.4.0 r14391-7f676b5ed6)) #0 SMP Sat Sep 5 13:43:16 2020
[    0.000000] SoC Type: MediaTek MT7621 ver:1 eco:3
[    0.000000] printk: bootconsole [early0] enabled
[    0.000000] CPU0 revision is: 0001992f (MIPS 1004Kc)
[    0.000000] MIPS: machine is Wavlink WL-WN531A6
[    0.000000] Initrd not found or empty - disabling initrd
[    0.000000] VPE topology {2} total 2
[    0.000000] Primary instruction cache 32kB, VIPT, 4-way, linesize 32 bytes.
[    0.000000] Primary data cache 32kB, 4-way, PIPT, no aliases, linesize 32 bytes
[    0.000000] MIPS secondary cache 256kB, 8-way, linesize 32 bytes.
[    0.000000] Zone ranges:
[    0.000000]   Normal   [mem 0x0000000000000000-0x0000000007ffffff]
[    0.000000]   HighMem  empty
[    0.000000] Movable zone start for each node
[    0.000000] Early memory node ranges
[    0.000000]   node   0: [mem 0x0000000000000000-0x0000000007ffffff]
[    0.000000] Initmem setup node 0 [mem 0x0000000000000000-0x0000000007ffffff]
[    0.000000] On node 0 totalpages: 32768
[    0.000000]   Normal zone: 288 pages used for memmap
[    0.000000]   Normal zone: 0 pages reserved
[    0.000000]   Normal zone: 32768 pages, LIFO batch:7
[    0.000000] percpu: Embedded 14 pages/cpu s26768 r8192 d22384 u57344
[    0.000000] pcpu-alloc: s26768 r8192 d22384 u57344 alloc=14*4096
[    0.000000] pcpu-alloc: [0] 0 [0] 1
[    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 32480
[    0.000000] Kernel command line: console=ttyS0,57600 rootfstype=squashfs,jffs2
[    0.000000] Dentry cache hash table entries: 16384 (order: 4, 65536 bytes, linear)
[    0.000000] Inode-cache hash table entries: 8192 (order: 3, 32768 bytes, linear)
[    0.000000] Writing ErrCtl register=00011cd0
[    0.000000] Readback ErrCtl register=00011cd0
[    0.000000] mem auto-init: stack:off, heap alloc:off, heap free:off
[    0.000000] Memory: 120696K/131072K available (5929K kernel code, 207K rwdata, 1272K rodata, 1284K init, 238K bss, 10376K reserved, 0K cma-reserved, 0K highmem)
[    0.000000] SLUB: HWalign=32, Order=0-3, MinObjects=0, CPUs=2, Nodes=1
[    0.000000] rcu: Hierarchical RCU implementation.
[    0.000000] rcu:     RCU restricting CPUs from NR_CPUS=4 to nr_cpu_ids=2.
[    0.000000] rcu: RCU calculated value of scheduler-enlistment delay is 25 jiffies.
[    0.000000] rcu: Adjusting geometry for rcu_fanout_leaf=16, nr_cpu_ids=2
[    0.000000] NR_IRQS: 256
[    0.000000] random: get_random_bytes called from start_kernel+0x340/0x558 with crng_init=0
[    0.000000] CPU Clock: 880MHz
[    0.000000] clocksource: GIC: mask: 0xffffffffffffffff max_cycles: 0xcaf478abb4, max_idle_ns: 440795247997 ns
[    0.000000] clocksource: MIPS: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 4343773742 ns
[    0.000009] sched_clock: 32 bits at 440MHz, resolution 2ns, wraps every 4880645118ns
[    0.015482] Calibrating delay loop... 583.68 BogoMIPS (lpj=1167360)
[    0.055787] pid_max: default: 32768 minimum: 301
[    0.065106] Mount-cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.079503] Mountpoint-cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.097215] rcu: Hierarchical SRCU implementation.
[    0.107126] smp: Bringing up secondary CPUs ...
[    0.117248] Primary instruction cache 32kB, VIPT, 4-way, linesize 32 bytes.
[    0.117259] Primary data cache 32kB, 4-way, PIPT, no aliases, linesize 32 bytes
[    0.117270] MIPS secondary cache 256kB, 8-way, linesize 32 bytes.
[    0.117365] CPU1 revision is: 0001992f (MIPS 1004Kc)
[    0.144184] Synchronize counters for CPU 1: done.
[    0.203825] smp: Brought up 1 node, 2 CPUs
[    0.216044] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 7645041785100000 ns
[    0.235327] futex hash table entries: 512 (order: 2, 16384 bytes, linear)
[    0.248980] pinctrl core: initialized pinctrl subsystem
[    0.261031] NET: Registered protocol family 16
[    0.283216] FPU Affinity set after 4688 emulations
[    0.303527] workqueue: max_active 576 requested for napi_workq is out of range, clamping between 1 and 512
[    0.324931] clocksource: Switched to clocksource GIC
[    0.336599] NET: Registered protocol family 2
[    0.346336] tcp_listen_portaddr_hash hash table entries: 512 (order: 0, 6144 bytes, linear)
[    0.362978] TCP established hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.378104] TCP bind hash table entries: 1024 (order: 1, 8192 bytes, linear)
[    0.392093] TCP: Hash tables configured (established 1024 bind 1024)
[    0.404839] UDP hash table entries: 256 (order: 1, 8192 bytes, linear)
[    0.417738] UDP-Lite hash table entries: 256 (order: 1, 8192 bytes, linear)
[    0.431793] NET: Registered protocol family 1
[    0.440366] PCI: CLS 0 bytes, default 32
[    0.536915] 4 CPUs re-calibrate udelay(lpj = 1163264)
[    0.548462] workingset: timestamp_bits=14 max_order=15 bucket_order=1
[    0.574652] squashfs: version 4.0 (2009/01/31) Phillip Lougher
[    0.586160] jffs2: version 2.2 (NAND) (SUMMARY) (LZMA) (RTIME) (CMODE_PRIORITY) (c) 2001-2006 Red Hat, Inc.
[    0.609177] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 251)
[    0.625917] mt7621_gpio 1e000600.gpio: registering 32 gpios
[    0.637258] mt7621_gpio 1e000600.gpio: registering 32 gpios
[    0.648545] mt7621_gpio 1e000600.gpio: registering 32 gpios
[    0.660391] Serial: 8250/16550 driver, 16 ports, IRQ sharing enabled
[    0.677078] printk: console [ttyS0] disabled
[    0.685539] 1e000c00.uartlite: ttyS0 at MMIO 0x1e000c00 (irq = 15, base_baud = 3125000) is a 16550A
[    0.703462] printk: console [ttyS0] enabled
[    0.720015] printk: bootconsole [early0] disabled
[    0.739571] 1e000d00.uartlite2: ttyS1 at MMIO 0x1e000d00 (irq = 16, base_baud = 3125000) is a 16550A
[    0.761527] spi-mt7621 1e000b00.spi: sys_freq: 220000000
[    0.773937] random: fast init done
[    0.775041] spi-nor spi0.0: gd25q128 (16384 Kbytes)
[    0.790539] 5 fixed-partitions partitions found on MTD device spi0.0
[    0.803199] Creating 5 MTD partitions on "spi0.0":
[    0.812766] 0x000000000000-0x000000030000 : "u-boot"
[    0.824218] 0x000000030000-0x000000040000 : "config"
[    0.835591] 0x000000040000-0x000000050000 : "factory"
[    0.847149] 0x000000050000-0x000000f00000 : "firmware"
[    0.859038] 2 uimage-fw partitions found on MTD device firmware
[    0.870992] Creating 2 MTD partitions on "firmware":
[    0.880917] 0x000000000000-0x00000025c990 : "kernel"
[    0.892283] 0x00000025c990-0x000000eb0000 : "rootfs"
[    0.903620] mtd: device 5 (rootfs) set to be root filesystem
[    0.915025] 1 squashfs-split partitions found on MTD device rootfs
[    0.927359] 0x0000005a0000-0x000000eb0000 : "rootfs_data"
[    0.939574] 0x000000f00000-0x000001000000 : "vendor"
[    0.951976] libphy: Fixed MDIO Bus: probed
[    0.987417] libphy: mdio: probed
[    0.994109] mt7530 mdio-bus:1f: MT7530 adapts as multi-chip module
[    1.007456] mtk_soc_eth 1e100000.ethernet eth0: mediatek frame engine at 0xbe100000, irq 18
[    1.025334] i2c-mt7621 1e000900.i2c: clock 100 kHz
[    1.036495] mt7621-pci 1e140000.pcie: Parsing DT failed
[    1.050030] NET: Registered protocol family 10
[    1.060572] Segment Routing with IPv6
[    1.068024] NET: Registered protocol family 17
[    1.076989] bridge: filtering via arp/ip/ip6tables is no longer available by default. Update your scripts to load br_netfilter if you need this.
[    1.103097] 8021q: 802.1Q VLAN Support v1.8
[    1.114032] mt7530 mdio-bus:1f: MT7530 adapts as multi-chip module
[    1.137212] libphy: dsa slave smi: probed
[    1.145660] mt7530 mdio-bus:1f lan1 (uninitialized): PHY [dsa-0.0:00] driver [Generic PHY]
[    1.163734] mt7530 mdio-bus:1f lan2 (uninitialized): PHY [dsa-0.0:01] driver [Generic PHY]
[    1.181771] mt7530 mdio-bus:1f lan3 (uninitialized): PHY [dsa-0.0:02] driver [Generic PHY]
[    1.199792] mt7530 mdio-bus:1f lan4 (uninitialized): PHY [dsa-0.0:03] driver [Generic PHY]
[    1.217970] mt7530 mdio-bus:1f wan (uninitialized): PHY [dsa-0.0:04] driver [Generic PHY]
[    1.235909] mt7530 mdio-bus:1f: configuring for fixed/rgmii link mode
[    1.253556] DSA: tree 0 setup
[    1.259829] rt2880-pinmux pinctrl: pcie is already enabled
[    1.270787] mt7621-pci 1e140000.pcie: Error applying setting, reverse things back
[    1.285860] mt7621-pci-phy 1e149000.pcie-phy: PHY for 0xbe149000 (dual port = 1)
[    1.300783] mt7621-pci-phy 1e14a000.pcie-phy: PHY for 0xbe14a000 (dual port = 0)
[    1.415396] mt7621-pci-phy 1e149000.pcie-phy: Xtal is 40MHz
[    1.426518] mt7621-pci-phy 1e14a000.pcie-phy: Xtal is 40MHz
[    1.537423] mt7621-pci 1e140000.pcie: pcie2 no card, disable it (RST & CLK)
[    1.551298] mt7621-pci 1e140000.pcie: PCIE0 enabled
[    1.561021] mt7621-pci 1e140000.pcie: PCIE1 enabled
[    1.570747] mt7621-pci 1e140000.pcie: PCI coherence region base: 0x60000000, mask/settings: 0xf0000002
[    1.589489] mt7621-pci 1e140000.pcie: PCI host bridge to bus 0000:00
[    1.602175] pci_bus 0000:00: root bus resource [io  0x1e160000-0x1e16ffff]
[    1.615880] pci_bus 0000:00: root bus resource [mem 0x60000000-0x6fffffff]
[    1.629587] pci_bus 0000:00: root bus resource [bus 00-ff]
[    1.640557] pci 0000:00:00.0: [0e8d:0801] type 01 class 0x060400
[    1.652562] pci 0000:00:00.0: reg 0x10: [mem 0x00000000-0x7fffffff]
[    1.665064] pci 0000:00:00.0: reg 0x14: [mem 0x60400000-0x6040ffff]
[    1.677624] pci 0000:00:00.0: supports D1
[    1.685617] pci 0000:00:00.0: PME# supported from D0 D1 D3hot
[    1.697483] pci 0000:00:01.0: [0e8d:0801] type 01 class 0x060400
[    1.709499] pci 0000:00:01.0: reg 0x10: [mem 0x00000000-0x7fffffff]
[    1.721996] pci 0000:00:01.0: reg 0x14: [mem 0x60410000-0x6041ffff]
[    1.734543] pci 0000:00:01.0: supports D1
[    1.742535] pci 0000:00:01.0: PME# supported from D0 D1 D3hot
[    1.755506] pci 0000:01:00.0: [14c3:7615] type 00 class 0x000280
[    1.767545] pci 0000:01:00.0: reg 0x10: [mem 0x00000000-0x000fffff 64bit]
[    1.781241] pci 0000:01:00.0: 2.000 Gb/s available PCIe bandwidth, limited by 2.5 GT/s x1 link at 0000:00:00.0 (capable of 4.000 Gb/s with 5 GT/s x1 link)
[    1.810129] pci 0000:00:00.0: PCI bridge to [bus 01-ff]
[    1.820559] pci 0000:00:00.0:   bridge window [io  0x0000-0x0fff]
[    1.832707] pci 0000:00:00.0:   bridge window [mem 0x60000000-0x600fffff]
[    1.846241] pci 0000:00:00.0:   bridge window [mem 0x60100000-0x601fffff pref]
[    1.860639] pci_bus 0000:01: busn_res: [bus 01-ff] end is updated to 01
[    1.874051] pci 0000:02:00.0: [14c3:7615] type 00 class 0x000280
[    1.886079] pci 0000:02:00.0: reg 0x10: [mem 0x00000000-0x000fffff 64bit]
[    1.899783] pci 0000:02:00.0: 2.000 Gb/s available PCIe bandwidth, limited by 2.5 GT/s x1 link at 0000:00:01.0 (capable of 4.000 Gb/s with 5 GT/s x1 link)
[    1.928629] pci 0000:00:01.0: PCI bridge to [bus 02-ff]
[    1.939061] pci 0000:00:01.0:   bridge window [io  0x0000-0x0fff]
[    1.951208] pci 0000:00:01.0:   bridge window [mem 0x60200000-0x602fffff]
[    1.964739] pci 0000:00:01.0:   bridge window [mem 0x60300000-0x603fffff pref]
[    1.979145] pci_bus 0000:02: busn_res: [bus 02-ff] end is updated to 02
[    1.992375] pci 0000:00:00.0: BAR 0: no space for [mem size 0x80000000]
[    2.005562] pci 0000:00:00.0: BAR 0: failed to assign [mem size 0x80000000]
[    2.019439] pci 0000:00:01.0: BAR 0: no space for [mem size 0x80000000]
[    2.032630] pci 0000:00:01.0: BAR 0: failed to assign [mem size 0x80000000]
[    2.046512] pci 0000:00:00.0: BAR 8: assigned [mem 0x60000000-0x600fffff]
[    2.060045] pci 0000:00:00.0: BAR 9: assigned [mem 0x60100000-0x601fffff pref]
[    2.074446] pci 0000:00:01.0: BAR 8: assigned [mem 0x60200000-0x602fffff]
[    2.087979] pci 0000:00:01.0: BAR 9: assigned [mem 0x60300000-0x603fffff pref]
[    2.102378] pci 0000:00:00.0: BAR 1: assigned [mem 0x60400000-0x6040ffff]
[    2.115916] pci 0000:00:01.0: BAR 1: assigned [mem 0x60410000-0x6041ffff]
[    2.129461] pci 0000:00:00.0: BAR 7: assigned [io  0x1e160000-0x1e160fff]
[    2.142993] pci 0000:00:01.0: BAR 7: assigned [io  0x1e161000-0x1e161fff]
[    2.156534] pci 0000:01:00.0: BAR 0: assigned [mem 0x60000000-0x600fffff 64bit]
[    2.171116] pci 0000:00:00.0: PCI bridge to [bus 01]
[    2.181016] pci 0000:00:00.0:   bridge window [io  0x1e160000-0x1e160fff]
[    2.194547] pci 0000:00:00.0:   bridge window [mem 0x60000000-0x600fffff]
[    2.208078] pci 0000:00:00.0:   bridge window [mem 0x60100000-0x601fffff pref]
[    2.222485] pci 0000:02:00.0: BAR 0: assigned [mem 0x60200000-0x602fffff 64bit]
[    2.237073] pci 0000:00:01.0: PCI bridge to [bus 02]
[    2.246968] pci 0000:00:01.0:   bridge window [io  0x1e161000-0x1e161fff]
[    2.260498] pci 0000:00:01.0:   bridge window [mem 0x60200000-0x602fffff]
[    2.274032] pci 0000:00:01.0:   bridge window [mem 0x60300000-0x603fffff pref]
[    2.289227] hctosys: unable to open rtc device (rtc0)
[    2.299966] mt7530 mdio-bus:1f: Link is Up - 1Gbps/Full - flow control off
[    2.317846] VFS: Mounted root (squashfs filesystem) readonly on device 31:5.
[    2.336249] Freeing unused kernel memory: 1284K
[    2.345300] This architecture does not have kernel memory protection.
[    2.358123] Run /sbin/init as init process
[    2.934235] init: Console is alive
[    2.941260] init: - watchdog -
[    3.691015] kmodloader: loading kernel modules from /etc/modules-boot.d/*
[    3.795457] usbcore: registered new interface driver usbfs
[    3.806556] usbcore: registered new interface driver hub
[    3.817293] usbcore: registered new device driver usb
[    3.837970] xhci-mtk 1e1c0000.xhci: 1e1c0000.xhci supply vbus not found, using dummy regulator
[    3.855378] xhci-mtk 1e1c0000.xhci: 1e1c0000.xhci supply vusb33 not found, using dummy regulator
[    3.873126] xhci-mtk 1e1c0000.xhci: xHCI Host Controller
[    3.883742] xhci-mtk 1e1c0000.xhci: new USB bus registered, assigned bus number 1
[    3.905075] xhci-mtk 1e1c0000.xhci: hcc params 0x01401198 hci version 0x96 quirks 0x0000000000210010
[    3.923361] xhci-mtk 1e1c0000.xhci: irq 17, io mem 0x1e1c0000
[    3.936085] hub 1-0:1.0: USB hub found
[    3.943711] hub 1-0:1.0: 2 ports detected
[    3.952415] xhci-mtk 1e1c0000.xhci: xHCI Host Controller
[    3.963107] xhci-mtk 1e1c0000.xhci: new USB bus registered, assigned bus number 2
[    3.978038] xhci-mtk 1e1c0000.xhci: Host supports USB 3.0 SuperSpeed
[    3.990895] usb usb2: We don't know the algorithms for LPM for this host, disabling LPM.
[    4.007994] hub 2-0:1.0: USB hub found
[    4.015589] hub 2-0:1.0: 1 port detected
[    4.029235] kmodloader: done loading kernel modules from /etc/modules-boot.d/*
[    4.057281] init: - preinit -
[    4.797915] mtk_soc_eth 1e100000.ethernet eth0: configuring for fixed/rgmii link mode
[    4.814022] mtk_soc_eth 1e100000.ethernet eth0: Link is Up - 1Gbps/Full - flow control rx/tx
[    4.830903] IPv6: ADDRCONF(NETDEV_CHANGE): eth0: link becomes ready
[    4.978504] random: jshn: uninitialized urandom read (4 bytes read)
[    5.045835] random: jshn: uninitialized urandom read (4 bytes read)
[    5.117851] random: jshn: uninitialized urandom read (4 bytes read)
[    5.334563] mt7530 mdio-bus:1f lan1: configuring for phy/gmii link mode
[    5.348189] 8021q: adding VLAN 0 to HW filter on device lan1
[    9.537340] mount_root: jffs2 not ready yet, using temporary tmpfs overlay
[    9.567242] urandom-seed: Seed file not found (/etc/urandom.seed)
[    9.656614] procd: - early -
[    9.662505] procd: - watchdog -
[   10.285095] procd: - watchdog -
[   10.291682] procd: - ubus -
[   10.502265] procd: - init -
[   11.059147] kmodloader: loading kernel modules from /etc/modules.d/*
[   11.090205] Loading modules backported from Linux version v5.8-0-gbcf876870b95
[   11.104688] Backport generated by backports.git v5.8-1-0-g79400d9e
[   11.143165] xt_time: kernel timezone is -0000
[   11.220696] mt7621-pci 1e140000.pcie: bus=1 slot=0 irq=20
[   11.231608] pci 0000:00:00.0: enabling device (0004 -> 0007)
[   11.242917] mt7615e 0000:01:00.0: enabling device (0000 -> 0002)
[   11.243758] urngd: v1.0.2 started.
[   11.276530] ieee80211 phy0: Selected rate control algorithm 'minstrel_ht'
[   11.289884] mt7621-pci 1e140000.pcie: bus=2 slot=1 irq=21
[   11.300733] pci 0000:00:01.0: enabling device (0004 -> 0007)
[   11.312082] mt7615e 0000:02:00.0: enabling device (0000 -> 0002)
[   11.352282] ieee80211 phy1: Selected rate control algorithm 'minstrel_ht'
[   11.422459] PPP generic driver version 2.4.2
[   11.434650] NET: Registered protocol family 24
[   11.464358] kmodloader: done loading kernel modules from /etc/modules.d/*
[   11.478846] mt7615e 0000:01:00.0: HW/SW Version: 0x8a108a10, Build Time: 20180518100604a
[   11.478846]
[   11.498087] mt7615e 0000:02:00.0: HW/SW Version: 0x8a108a10, Build Time: 20180518100604a
[   11.498087]
[   11.805806] random: crng init done
[   11.812625] random: 7 urandom warning(s) missed due to ratelimiting
[   11.910535] mt7615e 0000:02:00.0: N9 Firmware Version: _reserved_, Build Time: 20200814163649
[   11.910584] mt7615e 0000:01:00.0: N9 Firmware Version: _reserved_, Build Time: 20200814163649
[   11.998511] mt7615e 0000:02:00.0: CR4 Firmware Version: _reserved_, Build Time: 20190121161307
[   11.998519] mt7615e 0000:01:00.0: CR4 Firmware Version: _reserved_, Build Time: 20190121161307
[   19.612561] ieee80211 phy2: Selected rate control algorithm 'minstrel_ht'
[   19.612590] ------------[ cut here ]------------
[   19.622052] WARNING: CPU: 0 PID: 19 at backports-5.8-1/net/wireless/core.c:872 wiphy_register+0xd80/0xd88 [cfg80211]
[   19.643068] Modules linked in: pppoe ppp_async iptable_nat xt_state xt_nat xt_conntrack xt_REDIRECT xt_MASQUERADE xt_FLOWOFFLOAD xt_CT pppox ppp_generic nf_nat nf_flow_table_hw nf_flow_table nf_conntrack_rtcache nf_conntrack mt7615e mt7615_common mt7603e mt76 mac80211 ipt_REJECT cfg80211 xt_time xt_tcpudp xt_multiport xt_mark xt_mac xt_limit xt_comment xt_TCPMSS xt_LOG slhc nf_reject_ipv4 nf_log_ipv4 nf_defrag_ipv6 nf_defrag_ipv4 iptable_mangle iptable_filter ip_tables crc_ccitt compat nf_log_ipv6 nf_log_common ip6table_mangle ip6table_filter ip6_tables ip6t_REJECT x_tables nf_reject_ipv6 leds_gpio xhci_plat_hcd xhci_pci xhci_mtk xhci_hcd gpio_button_hotplug usbcore nls_base usb_common
[   19.764451] CPU: 0 PID: 19 Comm: kworker/u4:1 Not tainted 5.4.61 #0
[   19.776945] Workqueue: phy0 0x873f42e0
[   19.784398] Stack : 806576d8 87cbdc7c 806d0000 80720000 87cb4080 80668ee4 8738123c 00000009
[   19.801029]         86c75908 00000001 00000004 8007d624 00000000 00000001 87cbdc38 d999a5ca
[   19.817657]         00000000 00000000 00000000 00000000 00000030 00000101 6870203a 30203079
[   19.834282]         00000000 00000000 00000000 000bdaf1 00000000 80740000 00000000 8738123c
[   19.850909]         00000009 86c75908 00000001 00000004 00000001 8034f8e0 01808117 01808157
[   19.867535]         ...
[   19.872394] Call Trace:
[   19.877279] [<8000b72c>] show_stack+0x30/0x100
[   19.886149] [<805a96e8>] dump_stack+0xa4/0xdc
[   19.894830] [<8002bea0>] __warn+0xc0/0x10c
[   19.902978] [<8002bf48>] warn_slowpath_fmt+0x5c/0xac
[   19.912915] [<8738123c>] wiphy_register+0xd80/0xd88 [cfg80211]
[   19.924700] [<86c014ac>] ieee80211_register_hw+0x9bc/0xd8c [mac80211]
[   19.937584] [<873121dc>] mt76_register_phy+0x18/0x38 [mt76]
[   19.948700] [<873e31e4>] mt7615_register_ext_phy+0x274/0x2ac [mt7615_common]
[   19.962743] [<800458f0>] process_one_work+0x244/0x498
[   19.972790] [<80045cac>] worker_thread+0x168/0x5ec
[   19.982319] [<8004b4dc>] kthread+0x140/0x148
[   19.990812] [<800068d8>] ret_from_kernel_thread+0x14/0x1c
[   20.002178] ---[ end trace a5f82ab23c5525ea ]---
[   22.879487] jffs2_scan_eraseblock(): End of filesystem marker found at 0x0
[   22.905118] jffs2_build_filesystem(): unlocking the mtd device...
[   22.905208] done.
[   22.921475] jffs2_build_filesystem(): erasing all blocks after the end marker...
[   24.669402] mtk_soc_eth 1e100000.ethernet eth0: Link is Down
[   24.720136] mtk_soc_eth 1e100000.ethernet eth0: configuring for fixed/rgmii link mode
[   24.737804] mtk_soc_eth 1e100000.ethernet eth0: Link is Up - 1Gbps/Full - flow control rx/tx
[   24.766820] IPv6: ADDRCONF(NETDEV_CHANGE): eth0: link becomes ready
[   24.780800] mt7530 mdio-bus:1f lan1: configuring for phy/gmii link mode
[   24.820428] 8021q: adding VLAN 0 to HW filter on device lan1
[   24.854622] br-lan: port 1(lan1) entered blocking state
[   24.865132] br-lan: port 1(lan1) entered disabled state
[   24.878823] device lan1 entered promiscuous mode
[   24.888169] device eth0 entered promiscuous mode
[   24.935843] mt7530 mdio-bus:1f lan2: configuring for phy/gmii link mode
[   24.960458] 8021q: adding VLAN 0 to HW filter on device lan2
[   24.992889] br-lan: port 2(lan2) entered blocking state
[   25.003449] br-lan: port 2(lan2) entered disabled state
[   25.043911] device lan2 entered promiscuous mode
[   25.080783] mt7530 mdio-bus:1f lan3: configuring for phy/gmii link mode
[   25.124745] 8021q: adding VLAN 0 to HW filter on device lan3
[   25.157653] br-lan: port 3(lan3) entered blocking state
[   25.168132] br-lan: port 3(lan3) entered disabled state
[   25.205570] device lan3 entered promiscuous mode
[   25.243280] mt7530 mdio-bus:1f lan4: configuring for phy/gmii link mode
[   25.285919] 8021q: adding VLAN 0 to HW filter on device lan4
[   25.320230] br-lan: port 4(lan4) entered blocking state
[   25.330783] br-lan: port 4(lan4) entered disabled state
[   25.367052] device lan4 entered promiscuous mode
[   25.420809] mt7530 mdio-bus:1f wan: configuring for phy/gmii link mode
[   25.440614] 8021q: adding VLAN 0 to HW filter on device wan
[   29.389475] mt7530 mdio-bus:1f lan4: Link is Up - 1Gbps/Full - flow control rx/tx
[   29.404508] br-lan: port 4(lan4) entered blocking state
[   29.414970] br-lan: port 4(lan4) entered forwarding state
[   29.429366] IPv6: ADDRCONF(NETDEV_CHANGE): br-lan: link becomes ready
[   29.549460] mt7530 mdio-bus:1f wan: Link is Up - 1Gbps/Full - flow control off
[   29.563930] IPv6: ADDRCONF(NETDEV_CHANGE): wan: link becomes ready
[   43.193493] done.
[   43.197377] jffs2: notice: (1437) jffs2_build_xattr_subsystem: complete building xattr subsystem, 0 of xdatum (0 unchecked, 0 orphan) and 0 of xref (0 dead, 0 orphan) found.
[   43.350534] overlayfs: upper fs does not support tmpfile.
[ 1247.703714] kmodloader: loading kernel modules from /etc/modules.d/*
[ 1247.722922] kmodloader: done loading kernel modules from /etc/modules.d/*
[ 1247.800040] kmodloader: loading kernel modules from /etc/modules.d/*
[ 1247.814896] kmodloader: done loading kernel modules from /etc/modules.d/*
[ 1247.892238] kmodloader: loading kernel modules from /etc/modules.d/*
[ 1247.907265] kmodloader: done loading kernel modules from /etc/modules.d/*
[ 1247.984304] kmodloader: loading kernel modules from /etc/modules.d/*
[ 1247.999302] kmodloader: done loading kernel modules from /etc/modules.d/*



# padavan, etc, and other

# FIRMWARE
https://www.mediafire.com/file/80a80u2155vt0ta/WN533A8-WAVLINK-20181109/file

# Thank you source here:
https://forum.openwrt.org/t/mt7621-bricked/24802



# Thank you guy who backed up the entire deviwiki keeping it alive with updates here:
http://en.techinfodepot.shoutwiki.com/wiki/Winstars_WS-WN536A8


# Connor; Thank you reverse engineer here:
https://mcmillan.website/openwrt-for-wl-wn575a3/

https://mcmillan.website/rewriting-mt7628an-bootloader/

https://mcmillan.website/openwrt-ws-wn529b3/


# The Resellers with amazing stock firmware

https://play.google.com/store/apps/developer?id=WiLink.APP&hl=en_US

https://ematic.zendesk.com/hc/en-us/articles/360021348313-ERAC3000

https://forum.dd-wrt.com/phpBB2/viewtopic.php?p=1183408&sid=5005cba771e7a8a312f7352275e0ad18
