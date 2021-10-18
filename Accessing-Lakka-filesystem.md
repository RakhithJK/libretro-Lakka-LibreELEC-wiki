It is necessary to access the Lakka filesystem in order to accomplish tasks such as adding [ROMs](ROMs) or [BIOSes](BIOSes). Access to the filesystem also makes it possible to content like screenshots or savefiles from Lakka. **There are two overall approaches to gaining access to the Lakka filesystem:**

 * Network access
 * Attaching the Lakka drive to another system

Lakka can also be configured to use [ROMs that are served from a NAS](Serving-ROMs-from-a-NAS) for users who are comfortable working in a Linux shell environment.

## Filesystem layout

The editable portions of the Lakka system can be found in the following folders. Note that these the only folders which are made accessible via SAMBA -- accessing other areas of the filesystem requires a different approach.

 * **Assets** - fonts, icons, background images, themes
 * **Cheats** - loadable cheat files
 * **Configfiles** - configuration files for RetroArch and other parts of the system
 * **Cores** - libretro emulator cores and info files
 * **Database** - files used for content matching during automatic scanning of ROMs
 * **Joypads** - joypad autoconfiguration profiles
 * **Logs** - log files
 * **Overlays** - custom themed overlays
 * **Playlists** - custom playlists and playlists created by the scanner
 * **Remappings** - custom controller mappings per game / core
 * **Roms** - ROMs, films, music, and other content, including **downloads** subfolder with files downloaded by the `Online Updater` &rarr; `Content Downloader`
 * **Savefiles** - save files created by the games
 * **Savestates** - 'quicksave' states, as opposed to savefiles
 * **Screenshots** - screenshots made during gameplay
 * **Services** - configuration files for system services
 * **Shaders** - shaders for rendering various visual postprocessing effects
 * **System** - to store BIOSes and other files needed by the emulators
 * **Thumbnails** - the place where game thumbnails are stored
 * **Update** - copy update files here to update Lakka

Root file system of Lakka is read only, therefore any changes to assets, cores or other files used by RetroArch are made using overlayfs mount points. These mount points are present in the `/tmp` folder, where folder from root file system is overlayed with custom content. Changes to these special folders are persistent during reboots.

| Mount point | Original content | Overlayed content | Purpose |
+---+---+---+---|
| `/tmp/assets` | `/usr/share/retroarch-assets` | `/storage/assets` | Fonts, icons, background images, themes |
| `/tmp/cheats` | `/usr/share/libretro-cheats` | `/storage/cheats` | Loadable cheat files |
| `/tmp/cores` | `/usr/lib/libretro` | `/storage/cores` | Libretro emulator cores and info files |
| `/tmp/database` | `/usr/share/libretro-database` | `/storage/database` | Databases for content matching |
| `/tmp/joypads` | `/etc/retroarch-joypad-autoconfig` | `/storage/joypads` | Profiles for automatic configuration of game controllers |
| `/tmp/overlays` | `/usr/share/retroarch-overlays` | `/storage/overlays` | Themed overlays |
| `/tmp/shaders` | `/usr/share/common-shaders` | `/storage/shaders` | Shaders for rendering various visual postprocessing effects |
| `/tmp/system` | `/usr/share/retroarch-system` | /storage/system` | BIOS files and other files needed by emulators |

Where applicable, SAMBA shows the merged content, e.g. share **System** shows the content of `/tmp/system`.

## Transferring files via a network connection

### File transfer via Samba

Samba is a service that you can enable in **Settings->Services** which allows other computers on the local network to transfer files to Lakka via the CIFS/SMB protocol.  Only the most important folders are accessible via Samba.

Windows, OS X, and most Linux distributions should be able to navigate directly to Lakka's Samba share by entering `\\lakka\` into their file browser. If you cannot reach the Lakka system by name, it may be possible to reach it by IP. [Once you have determined Lakka's IP](Finding-the-IP-of-your-Lakka-box), enter that address in the file browser as with the Lakka name earlier, such as `\\FULL.IP.ADDRESS.HERE\`.

### File transfer via SCP

This method requires that SSH be enabled in Lakka, but it is faster than SAMBA. It will also require that you have and be familiar with operating SCP-enabled file transfer software or an SSH client capable of managing SCP file transfers.

You may be able to connect to Lakka via the name "lakka" in your SCP client. If not, you will need to [find the IP of your Lakka box](Finding-the-IP-of-your-Lakka-box).
The credentials for SCP are the same as for SSH: username **root** and password **root**.

#### SCP on Linux and Mac OS X hosts

In a terminal, copy the files over network using the scp command:

    scp -r roms/* root@ip-of-your-lakka:/storage/roms/
    scp -r bios/* root@ip-of-your-lakka:/tmp/system/

#### SCP on Windows hosts

Download the free software [FileZilla](https://filezilla-project.org) or [WinSCP](https://winscp.net), and connect to Lakka using the SCP protocol (port 22). They will expose the directories of Lakka, you can transfer files by dragging and dropping.

## Direct drive access

This method consists of mounting the SD card, flash drive, or hard drive where Lakka is installed on a host workstation running Windows, Linux, or OS X. It is not convenient if you have installed Lakka on a device with internal storage, since you would have to connect the drive to another PC. But it works well for ARM boards, where the storage media is an SD card most of the time.

### Direct drive access on a Linux host

If you're on Linux, you can mount the second partition of your SD card/USB pendrive, and access the files on this partition. This way, you don't need network connection, and you can access all files on your drive, including RetroArch configuration files located in `.config/retroarch/`.

### Direct drive access on a Windows host

Accessing `ext4` partitions from windows is not supported natively but you can install a [driver](http://www.howtogeek.com/112888/3-ways-to-access-your-linux-partitions-from-windows/).

### Direct drive access on an OS X host

Mac OS X does not allow users to mount ext4 partitions natively. [Paragon's ExtFS driver](http://www.paragon-software.com/home/extfs-mac/) is paid software. [OSXFuse](http://osxdaily.com/2014/03/20/mount-ext-linux-file-system-mac/) is free software. We have not tested either of these yet.

## Using an external USB drive

Lakka offers the possibility to store your ROMs on an external USB drive. 

Your USB drive must be formatted as FAT, NTFS or ext2/3/4. Store some ROMs on it, and plug it in your Lakka Box. The partition will be mounted automatically in a new folder under `/storage/roms/`, and your ROMs will appear in the menu. Please note that installing Lakka itself to an external USB hard drive is also an option.

Note: If you are using Lakka for PC in live USB mode, you should be able to access the hard drives of the host computer.
