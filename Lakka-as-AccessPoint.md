If your Wi-Fi card allows it, you can configure your Lakka box to behave as a local Wi-Fi access point.

In the cmdline, add `localap` to enable the service.

You can also enable it from SSH with:

    systemctl enable localap
    systemctl start localap

But before this, you will need to create a `/storage/.cache/services/localap.conf` containing the SSID and the password (8 characters min):

    APNAME=LAKKA
    PASSWORD=BLAHBLAH