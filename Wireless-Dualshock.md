Under most circumstances, the only steps required are:

1. Enable bluetooth in **Lakka → Services**
2. Plug your controller
3. Let the LEDs blink for a while
4. Unplug your controller
3. Lakka should now pair the controller automatically.

If automatic pairing does not succeed, please follow the following guide. All the following commands have to be executed on your Lakka box using the [Command Line Interface](Accessing-Lakka-command-line-interface)

## Enabling bluetooth

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
    scan on

### Dualshock 4

The Dualshock 4 is a bit different from the Dualshock 3 in that you should press the "Share" and "PS Home" button at the same time to get it into detection mode. You do not need to have controller connected via USB. Now press the two buttons and the led should start blinking rapidly. You will see output in your terminal similar to this:

    [bluetooth]# scan on
    Discovery started
    [CHG] Controller 00:15:83:0C:BF:EB Discovering: yes
    [NEW] Device 90:FB:A6:D6:D0:45 90-FB-A6-D6-D0-45
    [CHG] Device 90:FB:A6:D6:D0:45 LegacyPairing: no
    [CHG] Device 90:FB:A6:D6:D0:45 RSSI: 127
    [CHG] Device 90:FB:A6:D6:D0:45 Name: Wireless Controller
    [CHG] Device 90:FB:A6:D6:D0:45 Alias: Wireless Controller
    [CHG] Device 90:FB:A6:D6:D0:45 LegacyPairing: yes
    [CHG] Device 90:FB:A6:D6:D0:45 RSSI is nil

Now follow the steps under [Authorize the Dualshock Controller](#authorize-the-dualshock-controller). 

_If the controller led stops blinking (meaning you took too long), just press the "Share" and "PS Home" buttons again._

### Dualshock 3

Connect the DualShock 3 to the system using a USB cable and press the button round Playstation button. Watch for connection and disconnection messages and copy the device address (something like 38:C0:96:56:4D:AA). You will see a prompt that asks you to authorize the device:

    Authorize service ''service_uuid'' (yes/no):

### Authorize the Dualshock controller

Authorize it by typing 'yes'. Disconnect the USB cable from the DualShock 3. Hit the Playstation button again and while it blinks type the following:

    connect <device_addr>

Keep trying this command if you see device not available (it will loop between connected and disconnected) until you see something like the following

I usually keep pressing up + enter (repeating the last command)

    [CHG] Device <device_addr> Modalias: usb:v054Cp0268d0100
    [CHG] Device <device_addr> UUIDs:
           00001124-0000-1000-8000-00805f9b34fb
           00001200-0000-1000-8000-00805f9b34fb

Now trust the device

    trust <device_addr>

You're done.

Next time you hit the Playstation button it will connect without asking anything else. 

## Common issues

  * Make sure the battery on the controller is decently charged.

  * If the controller had been previously paired with another device, you might need to press the [reset button](images/wireless-dualshock-reset-button.png) with a paper clip.

  * Make sure you're using a working (and data-carrying) USB cable. You can assess that by following these steps:
      - Plug in the cable and connect the controller
      - Type in ``dmesg``
      - See the following (or similar) output at the bottom of the result:
````
[121113.389793] input: Sony PLAYSTATION(R)3 Controller as /devices/pci0000:00/0000:00:14.0/usb3/3-2/3-2:1.0/0003:054C:0268.0048/input/input61
[121113.390269] sony 0003:054C:0268.0048: input,hiddev0,hidraw2: USB HID v1.11 Joystick [Sony PLAYSTATION(R)3 Controller] on usb-0000:00:14.0-2/input0
````
  - If after following these steps you don't get the controller to connect, or the connection is unreliable (ex. only connected once). Make sure you are using a genuing controller. The market is flooded with high quality fakes. It's difficult to tell a fake apart from the original one without having them side by side. Some giveaways are:
      - Rattling inside
      - Relatively loud clicks when pressing the nubs
      - Rough edges
      - Spelling mistake on the [back label](images/fake-ds-back-label.jpg) (However, having a different label design isn't a telltale sign of a counterfeit pad)

## Configuring the controller

If the autoconfiguration does not work, you can manually configure your controller via the `Input` menu within Lakka's settings.
