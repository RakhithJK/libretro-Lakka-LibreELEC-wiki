## Joypad auto configuration

When you plug a joypad to your Lakka box, RetroArch will try to match its `vid:pid` pair or its name to one of the config files stored in `/etc/retroarch-joypad-autoconfig`. Those config files are maintained in this [git repository](https://github.com/libretro/retroarch-joypad-autoconfig/tree/master/udev).

When there is an configuration already available from this repository, you should see a yellow message with the name of your joypad appearing on the bottom part of the screen when Lakka starts and at certain other times during operation, depending on your Lakka settings.

If your joypad is already supported, it will work out of the box. Otherwise you will need to "map" or "bind" the buttons on the control to RetroArch and then create your own configuration file. This process takes approximately one minute for most joypads.

## Mapping

When configuring a joypad, keep in mind that RetroArch joypad abstraction is inspired by the SNES pad for the placement of the buttons ABXY:

![RetroPad](https://www.lakka.tv/images/Retropad_360pad.png)

## Binding a joypad

If your joypad is not recognized by Lakka, you will need to bind the buttons.

1. Go to the **Input Settings** using a keyboard and `Bind all` bottons on your joypad for the **User #1**.
2. **Optional**: [Generate an autoconfig file for your joypad](Contributing-your-joypad-config) and contribute it to our repository. Your joypad will then be supported automatically for all RetroArch platforms and users beginning with its next release.

## Wireless joypads

These wireless joypads have been tested with Lakka:

The **XBox360 wireless joypad and its microsoft adapter** works out of the box on Lakka. You will get better results with an official adapter, but we do support some Chinese clones. This adapter does not use bluetooth but a proprietary infrared protocol.

The **DualShock3** requires a bluetooth dongle or a computer with integrated bluetooth. Follow [the Wireless DualShock instructions](Wireless-Dualshock) and be aware that auto-configuration is complicated by bluetooth's pairing system and will not the same as with wired joypads.

## Input remapping

The recent version of RetroArch can remap inputs per core, or maybe even per game.