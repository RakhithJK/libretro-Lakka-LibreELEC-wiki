Lakka uses [Avahi](https://en.wikipedia.org/wiki/Avahi_(software)) to publish its hostname on its local network. By default, a system running Lakka is accessible as _lakka.local_ within your local network without explicitly knowing its IP address. (It is also accessible as simply _lakka_ via Samba.)

    ssh root@lakka.local

However, if you have multiple machines running Lakka, setting a unique hostname for each will avoid name collisions.

## Regular way
Using the [command line interface](Accessing-Lakka-filesystem):

    echo "picard" > /storage/.cache/hostname

Upon rebooting, the system will be accessible as _picard.local_ within your local network. (The Samba name will be simply _picard_.) 

    ssh root@picard.local
