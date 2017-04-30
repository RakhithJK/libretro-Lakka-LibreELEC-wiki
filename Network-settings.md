## Wired

Lakka uses DHCP, so if you attach your Lakka system to a wired switch or router it should automatically connect to the network and become available at the address "lakka".

## Wi-Fi

RetroArch does not have a graphical interface to change the network settings, requiring the [command line interface](Accessing-Lakka-command-line-interface).

Connecting to the network requires the *conmannctl* command.

    connmanctl

This will open a new prompt.

First enable the wifi interface:

    enable wifi

Start the agent (required by some wifi cards)

    connmanctl agent on

To scan the area for wifi networks run:

    connmanctl scan wifi

To list the wifi networks from the above scan run:

    connmanctl services
    android-device-tether wifi_de65fr56325_524632863278
    FBIDrone wifi_je86fe48321_532486348931

To connect to one of the wifi networks use the section starting with `wifi_`. You can use tab to autocomplete the name.

    connmanctl connect wifi_de65fr56325_524632863278
    exit

You can now be on the network. Check it out by using `ip addr` or `connmanctl state`.

Once done, your Lakka Box should automatically connect on startup. If not, you way have to mark the service as **prefered**.
