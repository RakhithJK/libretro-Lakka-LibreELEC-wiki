## General information

On the first partition of your SD card, you will find a file named `config.txt`. This file allows you to tweak a lot of things like framebuffer resolution, overclocking, audio, and is documented [here](https://www.raspberrypi.org/documentation/configuration/config-txt.md)

## Audio not working on some TVs

Some TVs send a wrong EDID saying that HDMI audio is not supported while in fact it is. You may need to force HDMI audio by uncommenting this line in the `config.txt`:

    hdmi_drive=2

## HDMI to DVI adaptor

If your RPi is not booting while using an HDMI to DVI adaptor, please remove this line from your `config.txt`:

    hdmi_drive=2

## HDMI to VGA adaptor

If you are using a HDMI to VGA adaptor on a Raspberry Pi 1 or 2 and you want to use the jack output for the sound you have to write in `config.txt` on the first partition of the SD card:

    hdmi_ignore_edid_audio=1

So the board'll not use the HDMI sound output.

## Composite output

Since Lakka version 3.5.1 it is possible to use CRT output. Here are examples for 240p mode:

### Raspberry Pi 3 
Add `video=Composite-1:720x480@60ie` to `cmdline.txt` right after `quiet` (separate  these statements with a space)

### Raspberry Pi 4
In addition to the modification of `cmdline.txt` above, add `enable_tvout=1` and `dtoverlay=vc4-kms-v3d-pi4,composite=1` to `config.txt`.
