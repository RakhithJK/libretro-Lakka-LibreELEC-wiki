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
Add `video=Composite-1:720x480@60e` to `cmdline.txt` right after `quiet` (separate these statements with a space).

Staring from Lakka 4.0 add following line to `config.txt`:

    dtoverlay=vc4-kms-v3d,composite=1


### Raspberry Pi 4
Add `video=Composite-1:720x480@60e` to `cmdline.txt` right after `quiet` (separate these statements with a space).

Add following lines to `config.txt`:

    enable_tvout=1
    dtoverlay=vc4-kms-v3d-pi4,composite=1


## Analog audio output
If you are missing the audio output device for the 3.5 mm jack, following lines have to be added to `config.txt` to enable audio output via the 3.5 mm jack:

    dtoverlay=piaudio
    dtparam=audio=on

These lines must be in this order and no other config lines should be between them.

In RetroArch set the audio output device to `default:CARD=Headphones` to route the audio output to the 3.5 mm jack.