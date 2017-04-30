## Overscan

Some TV have overscan. It means that the borders of your display can be cropped. To avoid it, you have to change the settings of your TV, not the settings of Lakka. Use your TV remote and try to disable overscan in the TV menu. Some TVs have display modes called **Computer Mode** or **Game Mode** that will disable overscan.

## Vsync

Vertical synchronization means that RetroArch will try to sync with your TV/monitor refresh rate. This option is useful to reduce/suppress tearing. It is enabled by default on all Lakka images.

However, some TVs send a wrong refresh rate to Lakka, and this can result in slow video. In these special case, you will want to set **video_vsync** to false.

RetroArch lets you set manually the refresh rate of your TV if needed.

## Threaded video driver

Using threaded video can result in a big performance improvement on systems with more than one processor core. For this reason, it is enabled by default on all Lakka images.

However, the vsync is disabled when this setting is enabled.

## Aspect ratio

The setting **Aspect Ratio Index** will let you override the aspect ratio. Some users like the display to be stretched to fit their screen. The default value in Lakka is to let each core provide its own original aspect ratio.

## Monitor index

If you setup Lakka on your laptop, but want the display to be on your TV using a cable, you can use this setting.

## Integer scale

This settings set the scaling to an integer number. It aligns the pixels of the game to the pixels of your screen. It makes the game image smaller in most cases, but each pixel will be neat. This setting is needed for some shaders.

## HW Bilinear Filtering

Disabled by default on Lakka. This setting will make the display smoother. You need to restart RetroArch for it to take effect. It's a matter of taste.
