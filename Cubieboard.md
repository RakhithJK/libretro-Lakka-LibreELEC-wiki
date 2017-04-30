## Forcing audio through Jack

These devices have more than one alsa cards. The distribution sets the HDMI card as default. You can override this setting in retroarch config:

    audio_device = "hw:0,0"