Most of the existing libretro cores are listed [here](https://github.com/libretro/libretro-super/tree/master/dist/info).  
The libretro cores we already packaged are listed [here](https://github.com/lakkatv/Lakka/tree/lakka/packages/libretro).

You have to read this before packaging cores for Lakka : [Compiling Lakka](Compiling-Lakka)

This [commit](https://github.com/lakkatv/Lakka/commit/a260552d472c81e81990d55d00e25cd17c43a06f) is a showcase. It adds the gsSP libretro core to Lakka.

## Hosting your local packages

The build scripts expect tar.xz packages to be served by HTTP. However, most libretro cores are not distributed as tar.xz, and we prefer to use git versions. For this, some scripts are here to clone the repos, update it and create the tar.xz.

Examples scripts are located in tools/mkpkg/, they are pretty straight forward and almost all the same (but not always) so you can just copy it and adapt it to your needs.

    $ tools/mkpkg/mkpkg_gpsp
    $ mv gpsp-*.tar.xz /path/to/your/www/

## Writing the package.mk

Reading the other packages located in packages/lakka should give you enough knowledge to start packaging new cores.

Here is an example package:

    ################################################################################
    #      This file is part of OpenELEC - http://www.openelec.tv
    #      Copyright (C) 2009-2012 Stephan Raue (stephan@openelec.tv)
    #
    #  This Program is free software; you can redistribute it and/or modify
    #  it under the terms of the GNU General Public License as published by
    #  the Free Software Foundation; either version 2, or (at your option)
    #  any later version.
    #
    #  This Program is distributed in the hope that it will be useful,
    #  but WITHOUT ANY WARRANTY; without even the implied warranty of
    #  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
    #  GNU General Public License for more details.
    #
    #  You should have received a copy of the GNU General Public License
    #  along with OpenELEC.tv; see the file COPYING.  If not, write to
    #  the Free Software Foundation, 51 Franklin Street, Suite 500, Boston, MA 02110, USA.
    #  http://www.gnu.org/copyleft/gpl.html
    ################################################################################

    PKG_NAME="fba"
    PKG_VERSION="e9581fe"
    PKG_REV="1"
    PKG_ARCH="any"
    PKG_LICENSE="Non-commercial"
    PKG_SITE="https://github.com/libretro/fba-libretro"
    PKG_URL="$LAKKA_MIRROR/$PKG_NAME-$PKG_VERSION.tar.xz"
    PKG_DEPENDS=""
    PKG_BUILD_DEPENDS_TARGET="toolchain"
    PKG_PRIORITY="optional"
    PKG_SECTION="RetroArch"
    PKG_SHORTDESC="Port of Final Burn Alpha to Libretro."
    PKG_LONGDESC="Port of Final Burn Alpha to Libretro."

    PKG_IS_ADDON="no"
    PKG_AUTORECONF="no"

    make_target() {
      make -C svn-current/trunk/ -f makefile.libretro
    }

    makeinstall_target() {
      mkdir -p $INSTALL/usr/lib/libretro
      cp svn-current/trunk/fb_alpha_libretro.so $INSTALL/usr/lib/libretro/
    }

Once written, you need to add your package as dependancy of the metapackage of your project. For example, if your package is for the RPi project, add it to the list in packages/lakka/RPi/package.mk.

## Forcing rebuild of a package

If you need to force the rebuild a certain package, you can use the following scripts

    DISTRO=Lakka PROJECT=RPi DEVICE=RPi ARCH=arm scripts/clean snes9x
    DISTRO=Lakka PROJECT=RPi DEVICE=RPi ARCH=arm scripts/build snes9x
    DISTRO=Lakka PROJECT=RPi DEVICE=RPi ARCH=arm scripts/install snes9x

Adapt the values to your case.