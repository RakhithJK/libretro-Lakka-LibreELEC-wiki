There are 3 ways to edit Lakka configuration:

## Using the graphical interface

You can configure Lakka using the graphical interface. Please note that some settings (such as menu driver switching) requires to restart Retroarch to take effect. To restart RetroArch, you can just use the *Quit RetroArch* entry in the menu. There is a service in Lakka that will restart RetroArch automatically.

## Using the command line interface

You can also edit the configuration file manually using the [command line interface](Accessing-Lakka-command-line-interface). To edit the configuration file, you need to stop the service first:

    systemctl stop retroarch

Then edit the config file:

    nano /storage/.config/retroarch/retroarch.cfg

Then start retroarch using the service:

    systemctl start retroarch

Or launch it manually (useful to get a log):

    retroarch

## Using the filesystem

You can also configure Lakka by mounting your SD card or USB key on your PC, and edit the configuration file with a text editor. This way is not convenient when you've installed Lakka on a PC's internal hard drive. It can be difficult if you are using Windows or OSX too. But it will be easy with Linux and an SD Card or a Live USB. See [this](Accessing-Lakka-filesystem).
