The bootloader is the software that will boot the Linux kernel, the core component of Lakka.
Lakka uses the following bootloaders:

  * **syslinux** - on the PC
  * **bcm2835-bootloader** - on Raspberry Pi
  * **u-boot** - on other ARM boards

The booloader configuration file is generally present on the first partition of Lakka. It contains some useful settings that will be passed to the kernel. The name of this file differs depending on the platform:

  * **On Raspberry Pi** - file name: cmdline.txt
  * **On a10** - file name: uEnv.txt
  * **On a20 Cubieboard2** - file name: uEnv.cb2
  * **On a20 Cubietruck** - file name: uEnv.ct 
  * **On Bananapi** - file name: uEnv.txt
  * **On imx6** - file name: uEnv.txt
  * **On Odroid-C1** - file name: boot.ini
  * **On Odroid-C2** - file name: boot.ini
  * **On Odroid-XU4** - file name: boot.ini
  * **On the Generic PC** - file name: extlinux.conf
  * **On WeTek Play** - not accessible
  * **On WeTek Hub** - not accessible
  * **On Orange Pi** - not yet supported

The name of the argument passed from the bootloader to the Linux kernel is called the **cmdline**.

## Editing the cmdline

### On Raspberry Pi

Edit **cmdline.txt** in the first partition of your SD card. This first partition is FAT32, so you can just plug the SD card in your PC to find that file.

The cmdline on RPi looks like this:

    boot=/dev/mmcblk0p1 disk=/dev/mmcblk0p2 quiet ssh vt.global_cursor_default=0 loglevel=2

### On Generic PC

Access the [command line interface](Accessing-Lakka-command-line-interface).

Remount the /flash mount r/w:

    mount -o remount,rw /flash

Edit the two config files with nano:

    nano /flash/syslinux.cfg
    nano /flash/EFI/BOOT/syslinux.cfg

There are two files to support both BIOS and EFI boot.

### On imx6

Edit **uEnv.txt** in the first partition of your SD card. This first partition is FAT32, so you can just plug the SD card in your PC to find that file.

The content of uEnv.txt looks like this:

    zImage=/KERNEL
    bootfile=/KERNEL
    mmcargs=setenv bootargs 'boot=/dev/mmcblk0p1 disk=/dev/mmcblk0p2 quiet video=mxcfb0:dev=hdmi,1920x1080M@60,if=RGB24,bpp=32 dmfc=3 consoleblank=0 loglevel=2 vt.global_cursor_default=0 ssh'

### On Allwinner 20

The default **uEnv.cb2** for Cubieboard2:

    script=cubieboard2.bin
    kernel=KERNEL
    extraargs='console=ttyS0,115200 console=tty0 boot=/dev/mmcblk0p1 disk=/dev/mmcblk0p2 rootwait quiet ssh loglevel=2 hdmi.audio=EDID:0 disp.screen0_output_mode=EDID:1280x1024p60 consoleblank=0'
    boot_mmc=fatload mmc 0 0x43000000 ${script}; fatload mmc 0 0x48000000 ${kernel}; bootm 0x48000000

The default **uEnv.ct** for Cubietruck:

    script=cubietruck.bin
    kernel=KERNEL
    extraargs='console=ttyS0,115200 console=tty0 boot=/dev/mmcblk0p1 disk=/dev/mmcblk0p2 rootwait quiet ssh loglevel=2 hdmi.audio=EDID:0 disp.screen0_output_mode=EDID:1280x1024p60 consoleblank=0'
    boot_mmc=fatload mmc 0 0x43000000 ${script}; fatload mmc 0 0x48000000 ${kernel}; bootm 0x48000000

### On Odroid-C1

The file is named **boot.ini** on the first FAT32 partition:

    ODROIDC-UBOOT-CONFIG
    
    setenv bootargs "console=ttyS0,115200n8 boot=/dev/mmcblk0p1 disk=/dev/mmcblk0p2 ro no_console_suspend vdaccfg=0xa000 logo=osd1,loaded,0x7900000,720p,full dmfc=3 cvbsmode=576cvbs hdmimode=1080p m_bpp=16 vout=hdmi ssh consoleblank=0"
    fatload mmc 0:1 0x21000000 KERNEL
    fatload mmc 0:1 0x21800000 meson8b_odroidc.dtb
    fdt addr 21800000
    bootm 0x21000000 - 0x21800000

### On Odroid-XU3/4

The file is named **boot.ini** on the first FAT32 partition.