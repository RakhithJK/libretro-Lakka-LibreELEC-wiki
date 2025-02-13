When problems arise during the operation of Lakka, it can be helpful for the developers and other volunteers to have certain standard information in order to find a solution. When requesting help with a Lakka issue, please try to include:

1. A description of the problem
2. The hardware that you are using
3. A system log recorded when the problem occurs (if possible) along with any other logs that are relevant
4. The name of the libretro core used
5. The version of Lakka you are using

## Automated collection of relevant logs

Since version 3.2 it is possible to collect all troubleshooting logs using one single script. You only need to [access the Lakka command line interface](Accessing-Lakka-command-line-interface) and run `createlog`. The script will create an archive with logs, which you can then either access on your SD card, via network share or upload.

## Introduction to Lakka logs

The information found in [Accessing the Lakka Command Line Interface](Accessing-Lakka-command-line-interface) can be very helpful during this process as well. The following procedures assume that the user has logged into Lakka via SSH.

On PC (Generic) when booting from USB/SD card you may key in `live ssh` at the boot prompt to enable SSH service. You should be able to access the shell also in case RetroArch does not start and you cannot enable SSH service via the RetroArch GUI.

### Lakka system logs

#### Option A: Copying from the terminal window

1. Restart the `retroarch` service in 'verbose' mode with this command:

       systemctl stop retroarch.service ; retroarch -v

2. Keep the terminal window open. After the service restarts, the system log will begin appearing in the window where it can be copy-pasted to another location.

#### Option B: Creating a log file

1. Restart the `retroarch` service in 'verbose' mode with this command:

       systemctl stop retroarch.service ; LIBGL_DEBUG=verbose retroarch --menu --verbose >> log.txt 2>&1

2. The file `log.txt` is now stored in the home directory. You can now copy the log file off of the Lakka system via an [SCP file transfer](Accessing-Lakka-filesystem#file-transfer-via-scp).

### Graphic card logs
`lspci -nnk | grep -A 3 VGA` will give information about your graphic card.

### Audio device logs
`aplay -L` enumerates audio devices which have been detected by Lakka.

### Input device logs

` lsusb` lists all devices attached via USB

`dmesg` displays all messages from the kernel ring buffer which typically is holding the messages generated by Lakka's Linux kernel from the boot process. The `dmesg` log lists each hardware device that the kernel detected along with information on how the device was configured by the system.

### Saving logs

If you are unable to copy-paste the output, e.g. you have access only to the local terminal and you cannot read ext4  (`/storage`, `LAKKA_DISK`) partition on your system, you can redirect the output of the logs to the FAT32 (`/flash`, `LAKKA`) partition. You only have to remount the partition into read-write mode:

     mount -o remount,rw /flash

Then to save the logs to this partition, just redirect the output to a file on this partition, i.e. replace the redirection from:

     command --parameter > log.txt 2>&1
                           ^^^^^^^

to:

     command --parameter > /flash/log.txt 2>&1
                           ^^^^^^^^^^^^^^

The logs will be saved on the FAT32 partition, so you can easily get to them when you plug in your USB thumb drive / SD card to your computer.

# Troubleshooting "Stuck on Lakka flower logo"

When you stuck after booting on the console with the Lakka flower logo, most certainly RetroArch is not able to start. This requires further steps to acquire the logs or any useful information to find out why. As we will by typing shell commands directly into the shell, it is essential that you either have a keyboard connected to your device, so you can use the shell/terminal directly on your device (recommended) OR connect your device to the network via ethernet cable and your network has DHCP autoconfiguration (devices on the network get and IP assigned automatically and you can determine the IP address assigned to your device on your e.g. router) and you will access your device via SSH .

## Modify kernel cmdline arguments

Depending on your device you must edit kernel cmdline arguments by adding `retroarch=0 textmode ssh` after the last parameter. Where to add these parameters depends on your device. In general, this file is located on the first partition of your SD Card / USB thumb drive.

Note that all arguments must be on the same line - this is very important - no line breaks.

| Device | File name / location | What to modify |
| --- | --- | --- |
| Raspberry Pi | `/cmdline.txt` | must be single line starting with `boot=` |
| Rockchip | `/extlinux/extlinux.conf` | line starting with `APPEND` |
| Amlogic | `/uEnv.ini` | line starting with `bootargs=` |
| Generic - GRUB | `/grub.cfg` | line starting with `linux` in the `menuentry "Live"` section |
| Generic - Syslinux | `/syslinux.cfg` | line starting with `APPEND` in the `LABEL live` section |

Note: For Generic PC it is recommended to modify both `grub.cfg` and `syslinux.cfg`. `grub.cfg` is currently used only for compatibility with EFI32 systems, in all other cases (legacy boot / EFI64) `syslinux.cfg` is used.

## Gathering information

After modifying the boot arguments it is time to boot up your device. If everything was set up correctly, you should end up with a shell prompt `Lakka:~ #` (or similar). As first step you need to mount overlays for retroarch, so type in following command and hit the Enter key:

    systemctl start retroarch.target

If the command executed without any errors, no additional output on screen is expected. Now you can continue with the [Automated log collection](#automated-collection-of-relevant-logs).
