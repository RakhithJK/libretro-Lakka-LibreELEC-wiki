### What is the origin of the project's name ?

When we started the project, it was working only on RPi and we were looking for a berry name.
The word Lakka means cloudberry in Finnish. The logo of the project is not a flower but a Lakka berry.

### Can I sell Lakka boxes?

No. Lakka is shipped with emulators protected by a Non Commercial license. Also, the name and the logo are a registered trademark.

### Do you support installation through CD or DVD?

Not yet. For now we only provide USB images. However, some users managed to set up Lakka on PC without USB boot support using [Plop](https://www.plop.at/en/bootmanagers.html).

### Do you support Virtualisation?

Not yet. Supporting virtualisation means having an X server with some special video drivers, and it is not yet the case. You can still set up RetroArch as a software on your current OS.

### Which hardware is the best for Lakka?

A small PC with an Intel graphics card will emulate most systems at full speed. The Odroid-XU4 is also very capable for a smaller price. The Raspberry Pi 3 is a decent choice, too. It depends on how you want to use Lakka. See other [supported hardware](Hardware-support).

### How do you navigate with a keyboard?

Use the directional arrows, and Enter and Backspace keys.

### My controller is not working. How come?

Read the documentation about [inputs](Input-settings), then, if you still do not get how to configure your controller, join our IRC channel or our forum. Someone will help you.

### I use wired PS3 controller, but pressing buttons does nothing.

You have to push the central button once and it should start working.

### Do you support wireless PS3 controllers?

Yes, if your DS3 is an official Sony controller. Just plug it once, and it should be paired. [Wireless Dualshock](Wireless-Dualshock)

### Do you support wireless PS4 controllers?

Yes, it will work out of the box in wired mode. In wireless mode, you will have to pair it using command line. [Wireless Dualshock](Wireless-Dualshock)

### Do you support XBOX 360 wireless controllers?

Wireless XBOX 360 controllers are supported, but they require a proprietary dongle. You cannot use the USB wire with your wireless controller. If you plan to buy a dongle, choose an official one. We do support some Chinese clones, but not all of them, yet.

### None of my GBA/NES/PS1 games work. Why?

You need to put the [BIOS](BIOSes) in the system directory.

### I have the 3 PS1 bios, but my PS1 games are still not launching (on PC). Why?

You need to use bin+cue, check that the content of the cue file matches the bin name.

### How do I upgrade Lakka?

Please read the documentation about [Upgrading Lakka](Upgrading-Lakka).

### What are all the menu items for?

There is an explanation in the RGUI [documentation](https://github.com/libretro/RetroArch/wiki/RGUI). 
You can also press *select* over an item to get a description of what it does.

### How do I use the jack audio output on RPi?

Jack audio output should work out of the box as long as you use an HDMI2DVI converter. If you are using a real HDMI wire and TV, you can plug your headphones in the TV. However, there might be a way to configure the RPi to force jack audio output in the config.txt file on the System partition.

### How do I use the jack audio output on Cubieboard, Banana Pi, Cuboxi, Hummingboard...?

These devices have more than one alsa cards. The distribution sets the HDMI card as default. You can override this setting in RetroArch configuration file :

    audio_device = "hw:0,0"

### How do I configure network and Wifi?

Please read the [documentation](Network-settings#wifi).

### Is it possible to access the OS with SSH?

Yes, find the [IP of your box](Finding-the-IP-of-your-Lakka-box) in the Network Information. SSH is enabled by default on most images, if not, you can enable it in the Service Settings. Credentials are `root:root`.

### How good (or bad) is the support for known joypads, keyboards?

All keyboards should work fine but if yours is not working, please tell us which model it is and we will try to investigate. However, the issue will have a low priority as our team is small and we support joypads first.

A [list](https://github.com/libretro/retroarch-joypad-autoconfig/tree/master/udev) of supported joypads is available. Joypads with no input_menu_toggle_btn lack an important button and can not be used as primary joypads. For now, the only primary joypads supported are wired XBOX360 and PS3. Most other pads have 15 buttons only, and the RETROPAD abstraction needs 16.

### How do I debug RetroArch?

Please see the documentation for [Troubleshooting Lakka](Troubleshooting-Lakka).

### How do I overclock Raspberry Pi CPU?

Plug your SD card into your computer, in the System partition (FAT32) you will find a config.txt file where you can uncomment some lines to enable overclocking. 

**Please note**: While overclocking _may_ give you better performance, it is done at your own risk and Lakka is not responsible for any damage you do to your RPi/boards. 

### I use Raspberry Pi on a TV connected by HDMI, and get no audio.

This can happen on some TVs. 
Mount your SD card and check that *hdmi_drive=2* is in config.txt and uncommented. This will force the sound to be sent over HDMI no matter what the TV says.

### I use Raspberry Pi with an HDMI to DVI adapter, why does it not boot?

Mount your SD card and remove or comment *hdmi_drive=2* in config.txt.

### When I Use Raspberry Pi on some particular TV, everything is slow, why?

In Settings -> Video Settings, disable VSync.

Or manually set *vsync = "false"* in /storage/.config/retroarch/retroarch.cfg

### How do I develop games for Lakka?

Take a look at [libretro-lutro](https://github.com/libretro/libretro-lutro), [lutro game of life](https://github.com/libretro/lutro-game-of-life) and [lutro platformer](https://github.com/libretro/lutro-platformer).

### I get no inputs on my Cubietruck.

Do not use the USB OTG to power your Cubietruck, use the barrel instead.

### FBA or another core's sound is laggy on my BananaPi/Cubieboard2/Cubietruck.

Remove `EDID:` from your uEnv.txt and set your exact resolution to force 60 FPS. You can alternatively disable vsync.

### Do you support dual booting?

Some boards like the RPi provide some tools to dual boot Lakka with other distros. We try to support NOOBS and Berryboot, but dual booting is not the priority right now. Lakka is meant to be installed on a dedicated machine.

### Trying to setup Lakka for PC, my hard drive is not listed by the installer.

Your hard drive must have an MBR partition table, and at least one partition (it will be erased).

### When booting Lakka on my PC, I get stuck at the flower screen.

Probably a graphics card [issue](https://github.com/libretro/Lakka/issues). Register on github and report the bug. Please provide some [debug information](Troubleshooting-Lakka).

### Menu XMB is too slow
You can change default setting for the ribbon via the Setting Tab > Menu > Menu Shader Pipeline to Ribbon (Simplified) or  Off which corresponds to the entry `menu_shader_pipeline = "1"` and `menu_shader_pipeline = "O"` for the configuration file. At last, you can switch to menu RGUI via Setting Tab > Driver > Menu Driver > rgui.

### Lakka doesn't expose RetroArch Online Updater (buildbot). Why?

 * Some cores from the buildbot are crashing or have glitches when used in Lakka
 * Lakka's toolchain cross compile each core with different flags and optimizations for each board, resulting in a speed boost
 * Lakka is delivered batteries included, and doesn't require internet connection to play games
 * Having monolithic upgrades ensures integration between cores, core info files, and database files
 * If one day the buildbot is down or unmaintained, a Lakka image would remain usable
 * It allows OEM to pack only the cores they care about
 * We can make sure that the cores in the system are all in their stable and tested version, VS the bleeding edge version
 * When a user reports a bug, we can determine the exact version of every core the user had on his system just by knowing his version of the system, which simplifies support a lot
 * Upgrading the system, the assets, the database, the cores, the shaders, is achieved with a single user action