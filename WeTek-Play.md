## Known issues

* Pressing "k" sometimes freezes RetroArch while playing
* Shutdown result in restart
* WeTek logo in background while playing
  * you have a white stripes on both sides (logo itself overlain by game)
  * or if the logo was not in fullscreen last time a it is located at the upper left corner and rest of TV is black

## Enabling SSH

WeTek Play doesn't support bootloader configuration. So you can't add SSH on boot. However, you can create this file

    touch /storage/.cache/services/sshd.conf

And then SSH will start automatically on boot.