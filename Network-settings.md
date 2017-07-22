## Wired

Lakka uses DHCP, so if you attach your Lakka system to a wired switch or router it should automatically connect to the network and become available at the address "lakka".

## Wi-Fi

RetroArch has now a [graphical interface](https://youtu.be/4Wr0jXKM3EY?t=4) to change the network settings. Just go to [Settings Tab > Wifi](http://www.lakka.tv/articles/2016/10/06/major-release-brings-wifi-and-simplified-interface/#wi-fi-configuration-interface).

You can still use  *conmannctl* command to connect to the network.

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
