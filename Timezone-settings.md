## Regular way

    echo "TIMEZONE=Europe/Rome" > /storage/.cache/timezone

## Alternative way

Using the [command line interface](Accessing-Lakka-filesystem):

    nano .config/autostart.sh

And export your timezone like this:

    #!/bin/sh
    export TZ="Europe/Helsinki"

This is the [List of tz database time zones available on Wikipedia](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)

You may need to reboot.