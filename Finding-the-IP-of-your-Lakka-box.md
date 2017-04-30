## Lakka interface

You can have access to your IP Address via the menu **Information** > **Network Information**.

## Avahi

Lakka use Avahi, so you should be able to use the hostname **lakka.local** in place of the IP when trying to connect Lakka on your local network. If it doesn't work, use the real IP.

    ping lakka.local

## On Linux

If you're on Linux, you can install the *arp-scan* utility, and run this command in a terminal:

    sudo arp-scan -l

You will get this kind of output

    Interface: wlan0, datalink type: EN10MB (Ethernet)
    Starting arp-scan 1.9 with 256 hosts (http://www.nta-monitor.com/tools/arp-scan/)
    192.168.0.14	f4:ca:e5:67:fe:7e	FREEBOX SA
    192.168.0.1		cc:3a:61:37:e2:95	SAMSUNG ELECTRO MECHANICS CO., LTD.
    192.168.0.1		cc:3a:61:37:e2:95	SAMSUNG ELECTRO MECHANICS CO., LTD. (DUP: 2)
    192.168.0.5		d0:92:9e:a7:6b:24	(Unknown)
    192.168.0.254	f4:ca:e5:49:f6:b5	FREEBOX SA
    
    5 packets received by filter, 0 packets dropped by kernel
    Ending arp-scan 1.9: 256 hosts scanned in 2.673 seconds (95.77 hosts/sec). 5 responded

## On Windows

If you're on Windows, you can install this tool: [LAN Scanner](http://mougino.free.fr/freeware/#LANS). 
Select "SSH" (port 22) as the service to be searched for, and hit Scan. 
One of the active IP addresses listed should be your Lakka box.

## On Mac OS X

    ifconfig | grep broadcast
    arp -a
