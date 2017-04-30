Arcade games are a special case and arcade emulation is complex.

## Arcade emulators

Lakka ships two emulators able to launch arcade ROMs: MAME2003 and FBA.

### FBA

FBA is set as the default emulator for Arcade in Lakka. We ship the version 0.2.97.38. It is faster than MAME and emulates the following platforms:

* Capcom CPS-1
* Capcom CPS-2
* Capcom CPS-3
* Cave
* Data East DEC-0, DEC-8 and DECO IC16 based games
* Galaxian based hardware
* Irem M62, M63, M72, M90, M92 and M107 hardware
* Kaneko 16
* Konami
* Neo-Geo
* NMK16
* Pacman based hardware
* PGM
* Psikyo 68EC020 and SH-2 based hardware
* Sega System 1, System 16 (and similar), System 18, X-Board and Y-Board
* Super Kaneko Nova System
* Toaplan 1
* Toaplan 2
* Taito F2, X, Z and others
* Miscellaneous drivers for lots of other hardware

### MAME

MAME supports more games than FBA. We ship the version from 2003 also called 0.78. It is an old version, but it was the easiest to package in Lakka and it is faster than newer versions of MAME.

## Arcade ROMs

Arcade ROMs are special and follow these rules:

 * Arcade ROMs have to stay zipped, they contain many files.
 * Arcade emulators are running the .zip games directly, they take care of uncompressing, while other emulators let RetroArch uncompress the ROM for them.
 * Never rename an arcade ROM, the file name is an identifier that helps the emulator to know how to emulate it.
 * Arcade ROMs have versions. Each arcade emulator comes with its own ROM set. A ROM that works under MAME2003 can be incompatible with MAME2014 or FBA.
 * Arcade ROMs can have parents/clone relationships.
 * Arcade ROMs can be of 3 types:
   * **Non-merged:** Games are standalone, each zip contain all the files needed to run the game, including the parent ROM.
   * **Split:** Games require the parent ROM to run.
   * **Merged:** Clones are merged in the parent. You end up with more than one game in a single zip.

In Lakka, we recommend you to use FBA with an **FBA v0.2.97.38 split ROM set**. RetroArch doesn't support merged sets anyway.

But if you really need to run more games, choose MAME2003 with a **MAME0.78 splitted ROM set**.