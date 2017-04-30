For the Raspberry Pi, there are two alternative installation methods that allows multiboot. Some users want to dual boot Lakka and OpenELEC. NOOBS is the prefered method.

## NOOBS

Works for RPi1 and RPi2.

<http://www.raspberrypi.org/help/noobs-setup/>

 1. Format your SD card as FAT32
 2. Download NOOBS lite from here <http://www.raspberrypi.org/downloads/>
 3. Extract NOOBS lite to your SD card
 4. Get the latest __Lakka-RPi.*-noobs.tar__ from here <http://sources.lakka.tv/nightly/RPi.arm/>
 5. Extract __Lakka-RPi.*-noobs.tar__ to the __os__ folder in your SD card
 6. Boot your RPi with your SD card, Lakka should appear in the OS list

## Berryboot

Works for RPi1 and RPi2.

<http://www.berryterminal.com/doku.php/berryboot/adding_custom_distributions>

 1. Flash Berryboot on your SD card.
 2. Update Berryboot to latest version.
 3. Download the .system file from [here](http://sources.lakka.tv/nightly/RPi.arm/?C=N;O=D)
 4. Rename the file to lakka.img
 5. Use the Berryboot "Add OS" Menu

## Ignition

Works for SolidRun hardware, the imx6 hummingboard and cubox-i. They support Lakka officially.

<http://www.solid-run.com/support/downloads/>

## PlopKexec Boot Manager

If you want to install Lakka on a PC that does not support USB booting, but has a CD drive.

<https://www.plop.at/en/bootmanagers.html>

> PlopKexec is a Linux Kernel based boot manager for autodetecting and chainloading Linux distributions from USB and CD/DVD. It works even if no Bios USB support is available. 