This page is for developers who want to customize their build and/or contribute
to Lakka.

You will need Linux (we usually build on Debian, Arch or Crux) and the base 
development packages (base-devel on Arch, build-essential on Debian).

You may also need a local HTTP server to host Lakka packages if you plan to do
packaging.

## Building Lakka the first time

First, clone Lakka:

    $ git clone https://github.com/libretro/Lakka-LibreELEC

Lakka is organized by projects, the *Generic* project targets PCs, while other
projects like *RPi* targets very specific hardware like the Raspberry Pi.  
The full list of projects can be listed like this:

    $ ls -l Lakka-LibreELEC/projects

You can now launch *make*, set the PROJECT/DEVICE and ARCH variables to fit your needs:

    $ cd Lakka-LibreELEC
    $ DISTRO=Lakka PROJECT=RPi DEVICE=RPi ARCH=arm make image   # for the Raspberry Pi
    $ DISTRO=Lakka PROJECT=RPi DEVICE=RPi2 ARCH=arm make image  # for the Raspberry Pi2/ Pi3
    $ DISTRO=Lakka PROJECT=Generic ARCH=x86_64 make image       # for 64 bits PCs
    $ DISTRO=Lakka PROJECT=Generic ARCH=i386 make image         # for 32 bits PCs

Building Lakka the first time takes a lot of time, you can go grab a coffee or two :)  
If the build fails, make sure you have at least 10 GB of free space and try to figure out which package is missing, install it, and *make* again.

You will find the result in Lakka-LibreELEC/target:

    $ ls -l target

The `.kernel` and `.system` files can be used to upgrade an existing Lakka system.  
The `.img.gz` file is the final result, it contains the image that can be flashed to an SD card or a USB pen drive.

Please follow this [tutorial](https://www.lakka.tv/get/) to know how to flash Lakka on a drive.

## Upgrading your Lakka build

If some time passed and you want to rebuild from newer sources:

    $ cd Lakka-LibreELEC
    $ git pull
    $ rm -rf target
    $ DISTRO=Lakka PROJECT=RPi DEVICE=RPi2 ARCH=arm make image

But if you just want to rebuild a particular package, for example a package you are trying to port to Lakka, you can just remove it like this and rebuild.

    $ DISTRO=Lakka PROJECT=RPi DEVICE=RPi ARCH=arm scripts/clean yourpackage
    $ DISTRO=Lakka PROJECT=RPi DEVICE=RPi ARCH=arm scripts/build yourpackage

If you want to rebuild all from scratch, remove the `build.*` folders
