## Playlist support

To allow launching ScummVM games from the menu, you'll need to do the following:

1. Find the Game ID of the game you're looking to add. The game IDs can be found in [ScummVM's compatibility list](https://scummvm.org/compatibility).
    > `monkey` for Monkey Island

2. Create a `.scummvm` file *inside the game directory* named by the Game ID
    > `monkey.scummvm` for Monkey Island

3. Open up the file in a text editor, and add the Game ID.
    > `echo monkey >> monkey.scummvm`

4. (Optional) Alternatively, you could download a prepared `.scummvm` file from [libretro-database-scummvm](https://github.com/RobLoach/libretro-database-scummvm).

5. Scan each game directory

This is an example of what the playlist would look like:

    /storage/roms/scummvm/monkey/monkey.scummvm
    The Secret of Monkey Island
    /tmp/cores/scummvm_libretro.so
    ScummVM
    b0e2af30|crc
    ScummVM.lpl
