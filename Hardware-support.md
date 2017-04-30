This page is a compilation of remarks that will help you choose the best hardware for your intended use case. Please remember that Lakka has been made to transform a dedicated machine into a game console.

The first section is composed of a table showing the level of support for each system. Below the table are more detailed comments about the pros and cons of each system type in terms of Lakka and emulator core support.

## Which systems are supported?

This table shows which systems can be emulated on each of our supported hardware.

|                 |RPi Zero |RPi  |RPi2 |RPi3 |a10 |a20 |imx6 |C1 |XU3 |PC |
|-----------------|---------|-----|-----|-----|----|----|-----|---|----|---|
|2048             |A        |A    |A    |A    |A   |A   |A    |A  |A   |A  |
|3DO              |-        |-    |-    |-    |-   |-   |-    |-  |-   |A  |
|Atari 2600       |?        |A    |A    |A    |A   |A   |A    |A  |A   |A  |
|Atari 7800       |?        |-    |-    |A    |-   |-   |-    |-  |-   |A  |
|Atari Jaguar     |?        |?    |?    |?    |?   |?   |?    |?  |?   |A  |
|Atari Lynx       |?        |A    |A    |A    |A   |A   |A    |A  |A   |A  |
|Cave Story       |?        |B    |A    |A    |?   |A   |A    |A  |A   |A  |
|Dinothawr        |?        |A    |A    |A    |A   |A   |A    |A  |A   |A  |
|Doom             |?        |A    |A    |A    |A   |A   |A    |A  |A   |A  |
|FB Alpha         |-        |C    |B    |A    |?   |B   |A    |A  |A   |A  |
|FFmpeg           |-        |D    |?    |?    |?   |?   |C    |C  |B   |B  |
|Game Boy         |A        |A    |A    |A    |A   |A   |A    |A  |A   |A  |
|Game Boy Advance |C        |B    |A    |A    |?   |B   |A    |A  |A   |A  |
|Game Boy Color   |A        |A    |A    |A    |A   |A   |A    |A  |A   |A  |
|Game Gear        |A        |A    |A    |A    |A   |A   |A    |A  |A   |A  |
|Lutro            |-        |?    |?    |A    |?   |?   |?    |?  |A   |A  |
|Master System    |A        |A    |A    |A    |A   |A   |A    |A  |A   |A  |
|Mega Drive       |A        |A    |A    |A    |A   |A   |A    |A  |A   |A  |
|NES              |A        |B    |A    |A    |A   |A   |A    |A  |A   |A  |
|Neo Geo Pocket   |-        |-    |A    |A    |?   |A   |A    |A  |A   |A  |
|Nintendo 64      |-        |-    |C    |B    |?   |C   |C    |B  |A   |A  |
|Nintendo DS      |-        |-    |-    |-    |-   |-   |-    |-  |-   |A  |
|PCEngine         |A        |A    |A    |A    |?   |A   |A    |A  |A   |A  |
|PCEngine CD      |B        |B    |A    |A    |?   |A   |A    |A  |A   |A  |
|PC-FX            |-        |-    |-    |-    |-   |-   |-    |-  |-   |A  |
|PlayStation      |-        |-    |B    |A    |?   |A   |A    |A  |A   |A  |
|PSP              |-        |-    |C    |B    |-   |-   |C    |B  |B   |A  |
|Quake            |?        |?    |?    |?    |?   |?   |?    |?  |?   |?  |
|Sega 32X         |?        |?    |A    |A    |?   |?   |A    |A  |A   |A  |
|Sega CD          |?        |?    |?    |?    |?   |?   |?    |?  |A   |?  |
|SuperNES         |C        |C    |B    |B    |B   |B   |A    |A  |A   |A  |
|Vectrex          |A        |A    |A    |A    |A   |A   |A    |A  |A   |A  |
|Virtual Boy      |-        |-    |-    |-    |?   |?   |?    |?  |?   |A  |
|WonderSwan Color |-        |-    |?    |A    |?   |?   |?    |?  |?   |A  |

Note: The hardware of a PC can vary significantly, this impacts performance accordingly. Also note that Nintendo 64 currently fails on 32 bit PC.

Meaning of grades:
    
    A = Most games are playable at full speed
    B = Sometimes lag, or may need overclocking, or need a little frameskipping
    C = Slow, but some games are playable, could be improved in the future
    D = Very slow, but at least one game is playable
    - = Not packaged, or will never be playable, or has a huge bug preventing playing

### Raspberry Pi

**CPU:** BCM2835  
**GPU:** VideoCore IV

**Pros:** Silent with no fan. Cheap like $35. Very good compatibility with TVs. Open source video API. Well documented and a large community of users. Uses the normal HDMI cable. Powered with micro USB. Uses SD or microSD cards. Easy to dual boot.

**Cons:** Weak, can't even run snes9x_next at full speed. Obsolete since the RPi2 is out. No SATA. No eMMC. No NAND. No WiFI. No Bluetooth.

**Conclusion:** Buy a RPi 2

### Raspberry Pi 2

**CPU:** BCM2836  
**GPU:** VideoCore IV

**Pros:** Powerful enough to run most SNES games with snes9x_next at full speed. Silent with no fan. Cheap like $35. Very good compatibility with TVs. Open source video api. Well documented with a large community of users. Uses the normal HDMI cable. Powered with micro USB. Uses SD or microSD cards. 4 USB ports. Easy to dual boot. Officially supported by OpenELEC.

**Cons:** Still weak, can't run N64 and PSP games at full speed. Some CPS3 arcade games are slow. No SATA. No eMMC. No NAND. No WiFI. No Bluetooth.

**Conclusion:** A good choice for beginners who want a cheap hardware and a lot of documentation. But it's still better to use a RPi3.

### Raspberry Pi 3

**CPU:** BCM2837  
**GPU:** VideoCore IV

**Pros:** Powerful enough to run most SNES games with snes9x_next at full speed. Silent with no fan. Cheap like $35. Very good compatibility with TVs. Open source video api. Well documented with a large community of users. Uses the normal HDMI cable. Powered with micro USB. Uses SD or microSD cards. 4 USB ports. Easy to dual boot. Officially supported by OpenELEC/LibreELEC. Intagrated Wi-Fi and bluetooth.

**Cons:** Can't run stuff like PSP games at full speed.

**Conclusion:** A good choice for beginners who want a cheap hardware and a lot of documentation.

### Generic PC

**CPU:** i386, x86_64  
**GPU:** Intel/Nvidia/Radeon

PCs can work very well. In fact, performance depends on its hardware.

Nvidia and Intel graphic cards should work. If you have to choose, choose Intel HD graphics for now.

On PC, you will have to flash a USB drive. This drive can be used as a live environment, allowing you to try Lakka on your hardware without installing it. The drive can also be used to install Lakka on your PC, but still does not support dual booting so it would be better to use a dedicated machine like a NUC.

**Pros:** Can virtually run any core. The live USB mode is convenient. The shaders can work well. Modular. Officially supported by OpenELEC.

**Cons:** Can be noisy. IO can be slow if not using an SSD. Very expensive. You will see a lot of messages on boot, like the BIOS and the syslinux bootloader. Not easy to dual boot. Not easy to unplug the hard drive to mount it on your laptop.

**Conclusion:** If you want to build the ultimate emulation console with no care for money, choose PC.

### Cubieboard

**CPU:** A10  
**GPU:** Mali-400

**Pros:** Can run some SNES games with snes9x_next, some arcade games. Cheap. Silent.

**Cons:** Obsolete, use the Cubietruck or the Banana Pi instead. Powered by a barel. 

**Conclusion:** More powerful than a RPi1, but still weak.

### Cubieboard2, Cubietruck and Banana Pi

**CPU:** A20  
**GPU:** Mali-400

RetroArch works on the Cubieboard2, Cubietruck and Banana Pi. However, the bad quality of MALI GLES userspace drivers provided by sunxi make it a bad choice for gaming. The kernel is also stuck at 3.4 which version is not supported by systemd. Lakka is being ported to these boards anyway and games are playable.

**Pros:** Some of these devices have Wifi, Bluetooth, SATA, and NAND. Powered by microUSB. Uses the normal HDMI port. Silent.

**Cons:** Old kernel, difficult to maintain. Wifi and bluetooth will not work. The Mali blobs are leaked. Only 2 USB ports.

**Conclusion:** An inferior product to the RPi2. Not recommended.

### Hummingboard and Cubox-i

**CPU:** i.MX6 i2ex to i4  
**GPU:** Vivante GC2000

Very good ARM boards. Their price is higher than RPi2 and Odroid-C1 but Lakka runs very well on them. Runs full speed PSX games, and some PSP games are playable. No vsync bugs. However, only two USB ports.

**Pros:** Good quality. Powerfull. Silent. Pretty good support of TVs. Powered by microUSB. Uses the normal HDMI port. The SolidRun team have been friendly enough to send us free samples. Officially supported by OpenELEC. Silent. The microSOM makes it modular.

**Cons:** Expensive. Hot CPU. mupen64plus bugs on it. The menu is not always 60fps, sometimes 55fps. Only 2 USB ports.

### Odroid-C1 and Odroid-C1+

**CPU:** Amlogic S805  
**GPU:** Mali-450

**Pros:** Powerfull CPU able to run some PSP games. Cheap like $35. The C1+ Model uses the big HDMI port, and can be powered by microUSB. Supports eMMC and microSD. The Hardkernel team is friendly, they sent us 2 free samples, and they love emulation. 4 USB ports.

**Cons:** Doesn't try to detect the resolution of TVs. No integrated Wi-Fi and Bluetooth.

**Conclusion:** More powerful than a RPi3 for the same price. Too bad it is lacking integrated Wi-Fi and Bluetooth.

### Odroid-XU3 and Odroid-XU4

**CPU:** Exynos
**GPU:** Mali-T628

**Pros:** $74 for an octa core is cheap. Very powerful CPU able to run most PSP games. No vsync issue, no tearing. The board supports eMMC. 4 USB ports. Friendly team, they provided two C1, one XU3 and one XU4 for free.

**Cons:** The fan is noisy on the XU3. Uses his own barel power supply. Uses micro HDMI. Only 2 USB ports on the XU4. No integrated Wi-Fi and Bluetooth.

**Conclusion:** A good and cheap alternative to PC. Too bad it is lacking integrated Wi-Fi and Bluetooth.

### WeTek_Play

**CPU:** Amlogic
**GPU:** Mali

**Pros:** Box provided. Powerful CPU. Good quality for the GPU BLOBs able to run mupen64plus at full speed. The WeTek team have been very helpful, they sent us a free sample. Officially supported by OpenELEC.

**Cons:** No access to the bootloader. Resolution fixed to 720p. No way to disable their white bootsplash that stays behind the game viewport.

**Conclusion:** If you are a N64 fan, and you have a 720p TV, and are not annoyed playing with a white background, it can be OK.

## Joypads

All USB joypads can be configured with some efforts. The most common USB joypads are pre-configured. When plugged they will work automatically. Here is [the list of auto-configured joypads](https://github.com/libretro/retroarch-joypad-autoconfig/tree/master/udev) so far. Joypads with no central button can use a L3+R3 combo to trigger the menu.

The best joypads to use with Lakka are:

- XBox 360 wired controller
- XBox 360 wireless controller + Microsoft adapter
- Dualshock 3 controller

We also support:

 - 8bitdo NES30Pro
 - Dualshock 4 controller
 - XBOX ONE controller