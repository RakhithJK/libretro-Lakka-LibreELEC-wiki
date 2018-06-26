Note: The following guide was tested with a 8Bitdo NES30 Pro Controller.

8Bitdo controllers won't pair automatically. You will have to use the command line interface to pair them the first time.

## Enabling bluetooth

Enable bluetooth in **Settings → Services**.

If you want to check that the service is **active**:

    systemctl status bluetooth

You should see something like this:

    ● bluetooth.service - Bluetooth service
       Loaded: loaded (/usr/lib/systemd/system/bluetooth.service; enabled; vendor preset: enabled)
       Active: active (running) since Tue 2015-04-07 19:37:50 UTC; 1s ago
     Main PID: 489 (bluetoothd)
       Status: "Running"
       CGroup: /system.slice/bluetooth.service
               └─489 /usr/lib/bluetooth/bluetoothd

If you get this message:

    ● bluetooth.service - Bluetooth service
       Loaded: loaded (/usr/lib/systemd/system/bluetooth.service; enabled; vendor preset: enabled)
       Active: inactive (dead)
    Condition: start condition failed at Tue 2015-04-07 19:35:48 UTC; 1min 59s ago
               ConditionPathExists=/storage/.cache/services/bluez.conf was not met

Try to manually enable and start bluetooth service:

    systemctl enable bluetooth
    systemctl start bluetooth

Check again if the service is **active**. (with the commands from above)

If bluetooth is still inactive you have to create the config file, and restart the service:

    touch /storage/.cache/services/bluez.conf
    systemctl start bluetooth

## Pairing the controller

Launch ``bluetoothctl``

    bluetoothctl

A bluetooth prompt will appear. Type the following: 

    agent on
    default-agent
    power on
    discoverable on
    pairable on
    scan on

Power on your 8Bitdo Controller in Mode 1. You will see output in your terminal similar to this:

    Discovery started
    [CHG] Controller B8:27:EB:48:30:22 Discovering: yes
    [NEW] Device E4:17:D8:3E:6A:7D 8Bitdo NES30 Pro

To authorize the 8Bitdo controller copy the device address (e.g. E4:17:D8:3E:6A:7D) and type the following:

    connect <device_addr>

You should see something like this: 

    [bluetooth]# connect E4:17:D8:3E:6A:7D
    Attempting to connect to E4:17:D8:3E:6A:7D
    [CHG] Device E4:17:D8:3E:6A:7D Connected: yes
    [CHG] Device E4:17:D8:3E:6A:7D Modalias: usb:v3820p0009d0100
    [CHG] Device E4:17:D8:3E:6A:7D UUIDs: 00001124-0000-1000-8000-00805f9b34fb
    [CHG] Device E4:17:D8:3E:6A:7D UUIDs: 00001200-0000-1000-8000-00805f9b34fb
    [CHG] Device E4:17:D8:3E:6A:7D Paired: yes
    Connection successful

If the connection fails because the controller already powered-off just power it on and try the `connect` command again.

Now trust the device:

    trust <device_addr>

You're done.

## Common issues

  * Make sure the battery on the controller is decently charged.
  * If the controller had been previously paired with another device, you might need to press the reset button (look in the controller manual).
  * If the controller is not reconnecting after a reboot/shutdown it usually means the pairing didn't stick. Try to manually pair the controller with the following command:

        pair <device_addr>

## Configuring the controller

If the autoconfiguration does not work, you can manually configure your controller via the `Input` menu within Lakka's settings.
