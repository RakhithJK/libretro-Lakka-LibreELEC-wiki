Warning: THIS GUIDE IS STILL UNDER DEVELOPMENT

This Wii Remote guide is based on the [Wireless DualShock guide](Wireless-Dualshock) which may also be useful until the Wii Remote guide is complete.

## Enabling bluetooth

You can enable bluetooth in **Settings → Services**. If it doesn't work, you can use the command line interface:

Enable and start bluetooth service

    touch /storage/.cache/services/bluez.conf
    systemctl enable bluetooth
    systemctl start bluetooth

Check that the service is **active**

    systemctl status bluetooth

    ● bluetooth.service - Bluetooth service
       Loaded: loaded (/usr/lib/systemd/system/bluetooth.service; enabled; vendor preset: enabled)
       Active: active (running) since Tue 2015-04-07 19:37:50 UTC; 1s ago
     Main PID: 489 (bluetoothd)
       Status: "Running"
       CGroup: /system.slice/bluetooth.service
               └─489 /usr/lib/bluetooth/bluetoothd

## Pairing the controller

Launch ``bluetoothctl``

    bluetoothctl

A bluetooth prompt will appear. Type the following: 

    agent on
    default-agent
    power on
    discoverable on
    pairable on

Press the red button inside the wiimote. Then type:

    scan on

After a while, type

    devices

You should see something like this:

    [CHG] Device A4:C0:E1:29:D7:E8 Name: Nintendo RVL-CNT-01
    [CHG] Device A4:C0:E1:29:D7:E8 Alias: Nintendo RVL-CNT-01
    [CHG] Device A4:C0:E1:29:D7:E8 LegacyPairing: yes

Copy the MAC address (here A4:C0:E1:29:D7:E8) and type:

    pair A4:C0:E1:29:D7:E8

You should see:

    Attempting to pair with A4:C0:E1:29:D7:E8
    [CHG] Device A4:C0:E1:29:D7:E8 Connected: yes
    [CHG] Device A4:C0:E1:29:D7:E8 Modalias: usb:v057Ep0306d8600
    [CHG] Device A4:C0:E1:29:D7:E8 UUIDs: 00001000-0000-1000-8000-00805f9b34fb
    [CHG] Device A4:C0:E1:29:D7:E8 UUIDs: 00001124-0000-1000-8000-00805f9b34fb
    [CHG] Device A4:C0:E1:29:D7:E8 UUIDs: 00001200-0000-1000-8000-00805f9b34fb
    [CHG] Device A4:C0:E1:29:D7:E8 Paired: yes
    Pairing successful

Then type

    trust A4:C0:E1:29:D7:E8

You should see:

    [CHG] Device A4:C0:E1:29:D7:E8 Trusted: yes
    Changing A4:C0:E1:29:D7:E8 trust succeeded
    [CHG] Device A4:C0:E1:29:D7:E8 Connected: no

Then type:

    connect A4:C0:E1:29:D7:E8

And you should see:

    Attempting to connect to A4:C0:E1:29:D7:E8
    [CHG] Device A4:C0:E1:29:D7:E8 Connected: yes
    Connection successful

If one of the last step fails, try again until it works.

## Common issues

  * Make sure the battery on the controller is charged.

## Configuring the controller

If the autoconfiguration does not work, you can manually configure your Wii controller. 
