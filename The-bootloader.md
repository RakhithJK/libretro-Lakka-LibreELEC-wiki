The bootloader is the software that will boot the Linux kernel, the core component of Lakka.
Lakka uses the following bootloaders:

  * **syslinux** / **grub** - on the PC
  * **bcm2835-bootloader** - on Raspberry Pi
  * **u-boot** - on other ARM boards

The booloader configuration file is generally present on the first partition of Lakka. It contains some useful settings that will be passed to the kernel. The name of this file differs depending on the platform:

  * **On Raspberry Pi** - file name: `cmdline.txt`
  * **On the Generic PC** - file name: `syslinux.cfg` and `EFI/BOOT/grub.cfg`
  * **On Amlogic devices** - file name: `uEnv.ini`
  * **On iMX6 devices** - file name: `extlinux/extlinux.conf`
  * **On Odroid-XU3/4** - file name: `boot.ini`

The name of the argument passed from the bootloader to the Linux kernel is called the **cmdline**.

## Editing the cmdline

### On Raspberry Pi

Edit `cmdline.txt` in the first partition of your SD card. This first partition is FAT32, so you can just plug the SD card in your PC to find that file.

The cmdline on RPi looks like this:

    boot=/dev/mmcblk0p1 disk=/dev/mmcblk0p2 quiet ssh vt.global_cursor_default=0 loglevel=2

### On Generic PC

You can edit the files directly using a text editor, but also from your Lakka device, if you have access to the [command line interface](Accessing-Lakka-command-line-interface).

Remount the /flash mount r/w:

    mount -o remount,rw /flash

Edit the two config files with nano:

    nano /flash/syslinux.cfg
    nano /flash/EFI/BOOT/syslinux.cfg

There are two files to support both BIOS and EFI boot.

In `syslinux.cfg` cmdline starts with `APPEND`, in `grub.cfg` with `linux`. There are two sections - `Live` and `Installer`, edit the cmdline in the `Live` section.

`syslinux.cfg`:

    LABEL live
      KERNEL /KERNEL
      APPEND boot=UUID=1106-4449 disk=UUID=25c49e90-d6b6-4486-8c2c-12f15a6bef65 tty portable quiet

`grub.cfg`:

    menuentry "Live" {
            search --set -f /KERNEL
            linux /KERNEL boot=UUID=1106-4449 disk=UUID=25c49e90-d6b6-4486-8c2c-12f15a6bef65 tty grub_portable quiet
    }


### On Amlogic

Edit `uEnv.ini` in the first partition of your SD card. The content of this file looks like this:

    dtb_name=/dtb/meson-gxbb-odroidc2.dtb
    bootargs=boot=UUID=1106-3535 disk=UUID=54c47770-0a4c-4295-a86b-f023c8026198 quiet console=ttyAML0,115200n8 console=tty0


### On iMX6

Edit `extlinux.conf` in the `extlinux` folder on the first partition of your SD card. This first partition is FAT32, so you can just plug the SD card in your PC to find that file.

The content of `extlinux.conf` looks like this:

    LABEL Lakka
      LINUX /KERNEL
      FDTDIR /
      APPEND boot=UUID=1106-5028 disk=UUID=1064beb8-b6ec-429c-aa98-c6adf4682c06 quiet video=HDMI-A-1:1920x1080@60


### On Odroid-XU3/4

The file is named `boot.ini` on the first FAT32 partition. The line with cmdline looks like this:

    setenv bootrootfs "boot=UUID=1106-5639 disk=UUID=4302d41d-14ae-4b70-9e4b-eb37825cf67d console=ttySAC2,115200n8 tty noram"


Below sections refer to legacy 2.3.x version, but are kept as reference

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

