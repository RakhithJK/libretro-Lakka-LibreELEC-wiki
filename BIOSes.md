Some libretro cores require a [BIOS](https://en.wikipedia.org/wiki/BIOS) to work.

BIOSes must be placed in the [system folder](http://www.lakka.tv/doc/Accessing-Lakka-filesystem/) although there are certain exceptions described in the table below.

## BIOS requirements table

This table shows the required BIOS for each system. You'll find up-to-date information [here](https://github.com/libretro/libretro-super/tree/master/dist/info) and [here](https://github.com/libretro/libretro-database/blob/master/dat/BIOS.dat).

Warning: Linux is a case sensitive system. Please name BIOS files exactly according to this table.

| System | BIOS | MD5 | Comment |
|---|---|---|---|
| 3DO - 3DO | panafz10.bin | `51f2f43ae2f3508a14d9f56597e2d3ce` |
| Atari - 7800 | 7800 BIOS (U).rom | `0763f1ffb006ddbe32e52d497ee848ae` |
| Atari - Lynx | lynxboot.img | `FCD403DB69F54290B51035D82F835E7B` |
| Final Burn Alpha | | | BIOS goes next to the ROMs |
| DOOM | prboom.wad | | BIOS goes next to the ROMs |
| Magnavox - Odyssey2 | o2rom.bin | `562d5ebf9e030a40d6fabfc2f33139fd` ||
| MAME 2003 | | | BIOS goes next to the ROMs |
| Mattel - Intellivision | exec.bin | 62e761035cb657903761800f4437b8af ||
| Mattel - Intellivision | grom.bin | 0cd5946c6473e42e8e4c2137785e427f ||
| NEC - PC Engine - TurboGrafx 16 | syscard3.pce | `0754f903b52e3b3342202bdafb13efa5` | |
| NEC - PC-FX | pcfx.rom | `08e36edbea28a017f79f8d4f7ff9b6d7` | |
| Nintendo - Famicom Disk System | disksys.rom | `ca30b50f880eb660a320674ed365ef7a` | |
| Nintendo - Game Boy Advance | gba_bios.bin | `a860e8c0b6d573d191e4ec7db1b1e4f6`| |
| Phillips - Videopac+ | o2rom.bin? | | Same as Magnavox Oddessy2? |
| Sega - Dreamcast (reicast) | dc_boot.bin | `e10c53c2f8b90bab96ead2d368858623` | Goes under `system/dc/` |
| Sega - Dreamcast (reicast) | dc_flash.bin | `0a93f7940c455905bea6e392dfde92a4` | Goes under `system/dc/` |
| Sega - Dreamcast (redream) | boot.bin | `e10c53c2f8b90bab96ead2d368858623` | Goes under `system/dc/` |
| Sega - Dreamcast (redream) | flash.bin | `0a93f7940c455905bea6e392dfde92a4` | Goes under `system/dc/` |
| Sega - Mega Drive - Genesis | bios_CD_J.bin | `278a9397d192149e84e820ac621a8edd` | Japan |
| Sega - Mega Drive - Genesis | bios_CD_U.bin | `2efd74e3232ff260e371b99f84024f7f` | USA |
| Sega - Mega Drive - Genesis | bios_CD_E.bin | `e66fa1dc5820d254611fdcdba0662372` | Europe |
| Sega - Saturn (Yabause) | saturn_bios.bin | `f273555d7d91e8a5a6bfd9bcf066331c` | |
| Sega - Saturn (beetle-saturn) | sega_101.bin | `85ec9ca47d8f6807718151cbcca8b964` | Japan |
| Sega - Saturn (beetle-saturn) | mpr-17933.bin | `3240872c70984b6cbfda1586cab68dbe` | USA/Europe |
| Sega - Saturn (beetle-saturn) | mpr-18811-mx.ic1 | `255113ba943c92a54facd25a10fd780c` | ROM for King of Fighters '95 |
| Sega - Saturn (beetle-saturn) | mpr-19367-mx.ic1 | `1cd19988d1d72a3e7caa0b73234c96b4` | ROM for Ultraman: Hikari no Kyojin Densetsu |
| Sharp - X68000 | cgrom.dat | `cb0a5cfcf7247a7eab74bb2716260269` | Goes under `system/keropi/` |
| Sharp - X68000 | iplrom.dat | `7fd4caabac1d9169e289f0f7bbf71d8e` | Goes under `system/keropi/`|
| Sony - PlayStation | scph5500.bin | `8dd7d5296a650fac7319bce665a6a53c` | Japan |
| Sony - PlayStation | scph5501.bin | `490f666e1afb15b7362b406ed1cea246` | USA (Can be renamed from scph7003.bin) |
| Sony - PlayStation | scph5502.bin | `32736f17079d0b2b7024407c39bd3050` | Europe |
