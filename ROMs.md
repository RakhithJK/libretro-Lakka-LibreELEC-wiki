## ROM storage and organization

Game ROMs must be placed within the `roms` folder. It is recommanded to keep ROMs zipped, except for CD images.

Many users sort their ROMs into subfolders named after the system which the ROMs belong to. This results in hierarchy such as:

    roms/
         Atari - 2600/
              Game 1.zip
              Game 2.zip
              Game 3.zip
         Sega - 32X/
              Game 1.zip
              Game 2.zip
         etc.
         etc.

You are free to organize your ROMs as you prefer.

Lakka supports loading ROMs from an external USB drive.

It also supports [loading ROMs from remote storage](Serving-ROMs-from-a-NAS) using network filesystems like NFS.

## ROM scanning and playlist generation

Lakka uses a ROM scanning system to generate the playlists in its horizontal menu. It is a convenient way to sort your ROMs on a per-system basis.

Each ROM stored in a folder being scanned by RetroArch is checked against a [database](https://github.com/libretro/libretro-database/tree/master/dat).

This database is based on [No-Intro](https://no-intro.org/) and will recognize only the good dumps. See it as a sort of ROM validator.

If you would like to generate playlists manually, or generate playlists for systems that do not have scanning support yet, [the playlist file format has been documented](Playlists).

## Special ROMs

Cartdige ROMs from the famous consoles are well known and all follow the same rules:

 * A ROM is composed of a single file
 * It can be zipped or not (Prefer zipped for Lakka)

But some systems are more complex.

## CD images

The preferred format for CD images is **BIN+CUE**. The .cue is a text file like this:

    FILE "NameOfTheBin.bin" BINARY
      TRACK 01 MODE2/2352
        INDEX 01 00:00:00

For PSP games, the preferred format is ISO.

## Arcade games

The specificity of Arcade games is explained [here](Arcade)
