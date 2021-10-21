To use Lakka properly on a CRT screen, we recommend using a Raspberry Pi.

You will need to add a modeline in the config.txt.

The ideal modeline vary from a game to another, especially for arcade games.

A simple modeline to get started is

    hdmi_timings=1920 1 152 247 280 240 1 3 7 12 0 0 0 60 0 40860000 1

We recommend that you use an adapter like this one: https://www.rgb-pi.com/

The quality will be a lot better than on the composite output.

For this adapter, we add the following lines in the config.txt:

    dtoverlay=pwm-2chan,pin=18,func=2,pin2=19,func2=2
    dtoverlay=rgb-pi
    enable_dpi_lcd=1
    display_default_lcd=1
    dpi_output_format=6
    dpi_group=2
    dpi_mode=87
    hdmi_timings=1920 1 152 247 280 240 1 3 7 12 0 0 0 60 0 40860000 1

You will also need their rgb-pi.dtbo overlay in the overlay folder.

