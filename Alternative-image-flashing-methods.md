It is recommended to use [Etcher](https://etcher.io/) to flash the Lakka images. If it is not possible to use Etcher, follow the methods below based on your operating system.

# Windows
On Windows you will need two additional tools, that can:
- decompress .gz files (in this example we will use [7-Zip](https://www.7-zip.org/))
- write image files to USB thumb drives / SD cards (in this example we will use [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/))

## Install required tools
Install 7-Zip and Win32DiskImager. You can download them using the links above.
## Decompress the downloaded Lakka image file
Using Windows File Explorer navigate to folder where you have save the downloaded Lakka image file (`Lakka-*.img.gz`). Right click on it and select 7-Zip -> Extract here. You will get decompressed file (`Lakka-*.img`).

## Determine your SD/USB drive
Plug in your SD card / USB thumb drive. Windows should give you the drive letter. Please note this for next step.

# Flash the image
Run the Win32DiskImager utility. Click on the folder icon below "Image File" and select the decompressed image file (`Lakka-*.img`). Under "Device" select the drive letter of your SD card / USB thumb drive. **Selecting incorrect letter can lead to erasing either your hard drive or any other device!** Click on the "Write" button. Wait until the writing process is finished and disconnect your SD card / USB thumb drive.

# Linux

## Decompress the downloaded Lakka image file
The downloaded image file is compressed using `gzip`, so it must be decompressed. We assume that you downloaded the file to your `~/Downloads` folder:

     $ cd ~/Downloads
     $ gunzip Lakka-*.img.gz

## Determining the SD/USB drive
Now list your current drives and partitions before you plug in your SD card / USB thumb drive:

     $ ls -l /dev/sd*

You will see a list of disks/partitions similar to following:

     brw-rw----. 1 root disk 8,  0 Sep 16 18:09 /dev/sda
     brw-rw----. 1 root disk 8,  1 Sep 16 18:09 /dev/sda1
     brw-rw----. 1 root disk 8,  2 Sep 16 18:09 /dev/sda2
     brw-rw----. 1 root disk 8,  3 Sep 16 18:09 /dev/sda3
     brw-rw----. 1 root disk 8,  4 Sep 16 18:09 /dev/sda4

In this case there is one disk _/dev/sda_ with 4 partitions _/dev/sda1_ to _/dev/sda4_. Your output might be different depending on number of drives and partitions.
Now plug in your SD card / USB thumb drive and type again:

     ls -l /dev/sd*

Once again the same disks/partitions will be shown, but there will be new disk with its partitions:

     brw-rw----. 1 root disk 8,  0 Sep 16 18:09 /dev/sda
     brw-rw----. 1 root disk 8,  1 Sep 16 18:09 /dev/sda1
     brw-rw----. 1 root disk 8,  2 Sep 16 18:09 /dev/sda2
     brw-rw----. 1 root disk 8,  3 Sep 16 18:09 /dev/sda3
     brw-rw----. 1 root disk 8,  4 Sep 16 18:09 /dev/sda4
     brw-rw----. 1 root disk 8, 16 Sep 18 23:12 /dev/sdb
     brw-rw----. 1 root disk 8, 17 Sep 18 23:12 /dev/sdb1
     brw-rw----. 1 root disk 8, 18 Sep 18 23:12 /dev/sdb2

In this case it is the disk _/dev/sdb_ with 2 partitions _/dev/sdb1_ to _/dev/sdb2_. This means, that _/dev/sdb_ represents the SD card / USB thumb drive. Please note your identifier.

## Flashing the image
Now that you know your SD card / USB thumb drive identifier, you can flash the image to it.
**Please note that dd is a very dangerous command: if you give it the wrong drive identifier, it could erase your hard drive instead of the SD card / USB thumb drive!**

     $ sudo dd if=Lakka-*.img of=/dev/sdX status=progress

Replace _/dev/sdX_ with your location noted in previous step, e.g. _/dev/sdb_. It should take a few minutes. Once done, type following:

     $ sync

Wait for the prompt and you can unplug your USB thumb drive / eject your SD card.

# MacOS

## Decompressing the downloaded Lakka image
Navigate to the location where you have downloaded the Lakka image. Double click the file to decompress it.

## Determining your SD/USB drive
First, you need to know the location of your your SD/USB drive. Open a Console and list your current drives and partitions before inserting the SD card / USB thumb drive:

     $ diskutil list

It will show output similar to this:

     /dev/disk0
        #:                       TYPE NAME                     SIZE      IDENTIFIER
        0:     GUID_partitions_scheme                        *121.3 GB   disk0
        1:                        EFI                         209.7 MB   disk0s1
        2:                  Apple_HFS                         67.9 GB    disk0s2
        3:                  Apple_HFS Linux Boot Loader fr... 134.2 MB   disk0s3
        4:                  Apple_HFS MacOS                   52.4 GB    disk0s4
        5:                 Apple_Boot Recovery HD             650.0 MB   disk0s5

In this case _disk0_ is the internal hard drive with 5 partitions _disk0s1_ to _disk0s5_. Now plug in your SD card / USB thumb drive and type again:

     $ diskutil list

The output should show one new drive:

     /dev/disk0
        #:                       TYPE NAME                    SIZE       IDENTIFIER
        0:     GUID_partitions_scheme                        *121.3 GB   disk0
        1:                        EFI                         209.7 MB   disk0s1
        2:                  Apple_HFS                         67.9 GB    disk0s2
        3:                  Apple_HFS Linux Boot Loader fr... 134.2 MB   disk0s3
        4:                  Apple_HFS MacOS                   52.4 GB    disk0s4
        5:                 Apple_Boot Recovery HD             650.0 MB   disk0s5
     /dev/disk1
        #:                       TYPE NAME                    SIZE       IDENTIFIER
        0:     FDisk_partition_scheme                        *2.0 GB     disk1
        1:             Windows_FAT_32 System                  131.1 MB   disk1s1
        2:                      Linux                         1.8 GB     disk1s2

So the identifier of the SD card / USB thumb drive is in this case _/dev/disk1_. Please note your identifier.

## Flashing the image
Now that you know your SD card / USB thumb drive location, you can flash the image to it.Go to the folder where you have extracted the downloaded file (`cd /path/to_the/location`).
**Please note that dd is a very dangerous command: if you give it the wrong drive identifier, it could erase your hard drive instead of the SD card!**

     $ sudo dd if=Lakka-*.img of=/dev/diskX

Replace _/dev/diskX_ with your identifier noted in previous step, e.g. _/dev/disk1_. It should take a few minutes until similar message is shown:

     327680+0 records in
     327680+0 records out
     167772160 bytes transferred in 179.500632 secs (934661 bytes/sec)

Once done, you can unplug your USB thumb drive / eject your SD card.
If you get this error:

     dd: /dev/diskXsN: Resource busy

You have to unmount every partition of your SD card / USB thumb drive. This can be done with:

     $ diskutil unmountDisk /dev/diskX

And then you can retry.