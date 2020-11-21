## Foxconn Intel Nettop
This may apply to other small pc's with multiple video outputs as well. This atom powered nettop has both a VGA and an HDMI port. However, it defaults to using the HDMI port. This must be changed if you want to use the VGA port.

Log in via [ssh](Accessing-Lakka-command-line-interface#ssh) or [console](Accessing-Lakka-command-line-interface#direct-access) and run this command to list the available video outputs:

    for p in /sys/class/drm/*/status; do con=${p%/status}; echo -n "${con#*/card?-}: "; cat $p; done

On my system, this outputs the following:

    LVDS-1: connected
    VGA-1: connected

The LVDS-1 output is the HDMI, but it shows connected even though it's unplugged. The solution is to disable the output via a kernel cmdline option.

Remount the /flash mount r/w:

    mount -o remount,rw /flash

Edit the file /flash/syslinux.cfg with nano:

    nano /flash/syslinux.cfg

Find the line that starts with "APPEND" and add "video=LVDS-1:d" to the end. Replace LVDS-1 with whichever video output you want to disable. It should look something like this:

    DEFAULT linux
    PROMPT 0
    
    LABEL linux
     KERNEL /KERNEL
     APPEND boot=LABEL=System disk=LABEL=Storage  ssh vt.global_cursor_default=0 loglevel=2 video=LVDS-1:d

Save the file, then remount /flash r/o:

    mount -o remount,ro /flash

Then reboot.

## Gigabyte Brix

Lakka appears to work quite well on the Gigabyte Brix, however there are a couple of caveats.

* Make sure that the bios is updated to F8, and set in Windows 7 and CSM mode enabled.
* Use the normal bios build, not the EFI build.
* After installation the SYSLinux configuration from pointing to the disk label to the UUID.

Using a Linux installation or live disc (or OSX) you need to have the disk with the install available to get their UUIDs. Use`blkid` .

Your output will look similar to:

    /dev/sdb1: LABEL="SYSTEM" UUID="0a3407de-014b-458b-b5c1-848e92a327a3" TYPE="ext4" PARTLABEL="SYSTEM" PARTUUID="98a81274-10f7-40db-872a-03df048df366"`
    /dev/sdb2: LABEL="STORAGE" UUID="b411dc99-f0a0-4c87-9e05-184977be8539" TYPE="ext4" PARTLABEL="STORAGE" PARTUUID="7280201c-fc5d-40f2-a9b2-466611d3d49e"`

Now you need to mount the SYSTEM partition and in a basic editor (such as notepad, vim, gedit, kate or emacs) open up the extlinux.conf with administrative or superuser privileges. You need to edit the APPEND line and change the boot= and disk= lines from LABEL= to UUID= and replace the identifier with the UUID.

From:

    APPEND boot=LABEL=System disk=LABEL=Storage  quiet vt.global_cursor_default=0 loglevel=2

To:

    APPEND boot=UUID=0a3407de-014b-458b-b5c1-848e92a327a3 disk=UUID=0a3407de-014b-458b-b5c1-848e92a327a3 quiet vt.global_cursor_default=0 loglevel=2