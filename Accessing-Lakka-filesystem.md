It is necessary to access the Lakka filesystem in order to accomplish tasks such as adding [ROMs](ROMs) or [BIOSes](BIOSes). Access to the filesystem also makes it possible to content like screenshots or savefiles from Lakka. **There are two overall approaches to gaining access to the Lakka filesystem:**

 * Network access
 * Attaching the Lakka drive to another system

Lakka can also be configured to use [ROMs that are served from a NAS](Serving-ROMs-from-a-NAS) for users who are comfortable working in a Linux shell environment.

## Filesystem layout

The editable portions of the Lakka system can be found in the following folders. Note that these the only folders which are made accessible via SAMBA -- accessing other areas of the filesystem requires a different approach.

 * **roms** - ROMs, films, music, and other content
 * **savefiles**
 * **savestates** - 'quicksave' states, as opposed to savefiles
 * **screenshots**
 * **shaders** - to override shaders
 * **system** - to store BIOSes
 * **update** - copy update files here to update Lakka
 * **playlists** - to access the playlists
 * **joypad** - joypad autoconfiguration profiles which are specific to your Lakka system
 * **thumbnails** - the place where game thumbnails are stored

## Transferring files via a network connection

### File transfer via Samba

Samba is a service running on Lakka which allows other systems on the local network to add and remove files from Lakka via the CIFS/SMB protocol.  Only some folders are accessible via Samba.

Windows, OS X, and most Linux distributions should be able to navigate directly to Lakka's Samba share by entering `\\lakka\` into their file browser. If you cannot reach the Lakka system by name, it may be possible to reach it by IP. [Once you have determined Lakka's IP](Finding-the-IP-of-your-Lakka-box), enter that address in the file browser as with the Lakka name earlier, such as `\\FULL.IP.ADDRESS.HERE\`.

### File transfer via SCP

This method requires that SSH be enabled in Lakka, but it is faster than SAMBA. It will also require that you have and be familiar with operating SCP-enabled file transfer software or an SSH client capable of managing SCP file transfers.

You may be able to connect to Lakka via the name "lakka" in your SCP client. If not, you will need to [find the IP of your Lakka box](Finding-the-IP-of-your-Lakka-box).
The credentials for SCP are the same as for SSH: username **root** and password **root**.

#### SCP on Linux and Mac OS X hosts

In a terminal, copy the files over network using the scp command:

    scp -r roms/* root@ip-of-your-lakka:roms/
    scp -r bios/* root@ip-of-your-lakka:system/

#### SCP on Windows hosts

Download the free software [FileZilla](https://filezilla-project.org) or [WinSCP](https://winscp.net), and connect to Lakka using the SCP protocol (port 22). They will expose the directories of Lakka, you can transfer files by dragging and dropping.

## Direct drive access

This method consists of mounting the SD card, flash drive, or hard drive where Lakka is installed on a host workstation running Windows, Linux, or OS X. It is not convenient if you have installed Lakka on a device with internal storage, since you would have to connect the drive to another PC. But it works well for ARM boards, where the storage media is an SD card most of the time.

### Direct drive access on a Linux host

If you're on Linux, you can mount the second partition of your SD card/USB pendrive, and access the files on this partition. This way, you don't need network connection, and you can access all files on your drive, including RetroArch configuration files located in `.config/retroarch/`.

### Direct drive access on a Windows host

Accessing `ext4` partitions from windows is not supported natively but there are some workarounds available:

1. Use a 3rd party software/driver to access the partitions (This [web article](http://www.howtogeek.com/112888/3-ways-to-access-your-linux-partitions-from-windows/) has some more information on this topic).
2. Use a complicated Linux Virtual Machine setup.
3. Use Linux.

The easiest option would be to use a 3rd party software/driver but they don't support all the features/requirements which `ext4` file system require. Its not recommended as they can corrupt the file systems.

The safest option would be to use Linux itself... Although, it does not qualify its place in this section, its the most safe/secure way to access your lakka data partition. Here are 2 ways of using Linux:

### Direct drive access on an OS X host

Mac OS X does not allow users to mount ext4 partitions natively. [Paragon's ExtFS driver](http://www.paragon-software.com/home/extfs-mac/) is paid software. [OSXFuse](http://osxdaily.com/2014/03/20/mount-ext-linux-file-system-mac/) is free software. We have not tested either of these yet.

## Using an external USB drive

Lakka offers the possibility to store your ROMs on an external USB drive. 

Your USB drive must be formatted as FAT, NTFS or ext2/3/4. Store some ROMs on it, and plug it in your Lakka Box. The partition will be mounted automatically in a new folder under `/storage/roms/`, and your ROMs will appear in the menu. Please note that installing Lakka itself to an external USB hard drive is also an option.

Note: If you are using Lakka for PC in live USB mode, you should be able to access the hard drives of the host computer.
