We are using two cores to emulate N64:

 * Parallel-N64 (previously named Mupen64plus) an optimized/rewritten Nintendo 64 emulator made specifically for libretro
 * Mupen64plus (previously named Glupen64) a straight port of Mupen64plus to libretro

Mupen64plus is faster, and Parellel-N64 is more accurate. Depending on the platform, we set one or the other as default.

## GFX plugins

Parellel-N64 have many GFX plugins. It will default to glide64

 - glide64: hardware rendered, medium accuracy, medium speed
 - rice: hardware rendered, low accuracy, fast (use this on RPi)
 - gln64: hardware rendered, low accuracy, fast (broken on GLES2)
 - angrylion: software rendered, high accuracy, slow

Switching the gfx plugin requires a content restart.

## HD

You can increase the internal and external resolution of the games in the core options. This also requires a content restart.