## No video output on some TVs

You may need to disable EDID detection in the boot.ini on the first partition:

    #------------------------------------------------------------------------------------------------------
    #
    # Video output
    #
    # Setup the video output
    #   Unset variable = automatic
    #
    #   setenv video_output "video=HDMI-A-1:1920x1080M@60" : 1080p (Use connected display's EDID)
    #   setenv video_output "video=HDMI-A-1:1280x720@60"   :  720p (Use connected display's EDID)
    # 
    #   setenv video_output "drm_kms_helper.edid_firmware=edid/1920x1080.bin" : 1080p (Use system EDID)
    #   setenv video_output "drm_kms_helper.edid_firmware=edid/1280x720.bin"  :  720p (Use system EDID)
    #------------------------------------------------------------------------------------------------------
    # setenv video_output "video=HDMI-A-1:1920x1080M@60"

## Audio Output Rate

Setting the audio output rate to 44100 instead of 48000 fixes the 55FPS bug.

## Using eMMC and SD at the same time

One of our users installed Lakka on his SD card, and wanted to keep its eMMC plugged. He had to change the dev names in the boot.ini. /dev/mmcblk1p1 instead of /dev/mmcblk0p1, and /dev/mmcblk1p2 instead of /dev/mmcblk0p2

## A less noisy fan (XU3-Lite/XU4)

The fan is loud and constantly switches ON/OFF. You can improve it using this [this fan control script](https://github.com/fluffymadness/odroid-xu3-fan-control).(Not well tested, use it at your own risk).

XU4 Fan-Mod

To take it one step further, you can replace the stock fan with a [3rd party one](http://forum.odroid.com/viewtopic.php?f=65&t=15310).

This [mod](http://forum.odroid.com/viewtopic.php?f=97&t=18211) combines the noctua and the stock-fan in a way that the original case can be used without any modifications.