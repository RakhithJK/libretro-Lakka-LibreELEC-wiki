For the Raspberry Pi, there are two alternative installation methods that allows multiboot. Some users want to dual boot Lakka and OpenELEC. NOOBS is the prefered method.

## NOOBS

Works for RPi1, RPi2, RPi3 and RPi4.

[NOOBS project page](https://projects.raspberrypi.org/en/projects/noobs-install)
[NOOBS GitHub repository](https://github.com/raspberrypi/noobs)

 1. Format your SD card as FAT32
 2. Download [latest NOOBS lite release](https://downloads.raspberrypi.org/NOOBS_lite_latest)
 3. Extract NOOBS to your SD card
 4. Open [Lakka NOOBS download page](https://le-builds.lakka.tv/noobs/)
 5. Enter the folder matching your RPi:

 * For RPi0 / RPi1: [Lakka_RPi](https://le-builds.lakka.tv/noobs/Lakka_RPi/)
 * For RPi2 / RPi3: [Lakka_RPi2](https://le-builds.lakka.tv/noobs/Lakka_RPi2/)
 * For RPi3 (64 bits): [Lakka_RPi4_64](https://le-builds.lakka.tv/noobs/Lakka_RPi3_64/)
 * For RPi4: [Lakka_RPi4](https://le-builds.lakka.tv/noobs/Lakka_RPi4/)
 * For RPi4 (64 bits): [Lakka_RPi4_64](https://le-builds.lakka.tv/noobs/Lakka_RPi4_64/)

 6. Download all the available files into a local folder named as the last part of the URL (e.g. *Lakka_RPi3_64*)
 7. Copy the folder with all the files to the __os__ folder in your SD card
 8. Boot your RPi with your SD card, Lakka should appear in the OS list

## BerryBoot

Works for RPi1 and RPi2.

[BerryBoot homepage](https://www.berryterminal.com/doku.php/berryboot)

 1. Flash Berryboot on your SD card.
 2. Update Berryboot to latest version.
 3. Download the .system file for [RPi](https://le.builds.lakka.tv/RPi.arm/) or [RPi2](https://le.builds.lakka.tv/RPi2.arm/)
 4. Rename the file to lakka.img
 5. Use the Berryboot "Add OS" Menu

## Ignition

Works for SolidRun hardware, the imx6 hummingboard and cubox-i. They support Lakka officially.

[Ignition installer](https://www.solid-run.com/ignition/)

## PlopKexec Boot Manager

If you want to install Lakka on a PC that does not support USB booting, but has a CD drive.

[PlopKexec](https://www.plop.at/en/plopkexec/index.html)

> PlopKexec is a Linux Kernel based boot manager for autodetecting and chainloading Linux distributions from USB and CD/DVD. It works even if no Bios USB support is available. 
