Lakka takes its inspiration from projects like [RetroPie](https://github.com/petrockblog/RetroPie-Setup) and [PiMAME](https://github.com/ssilverm/PiMAME) that demonstrate the potential of combining a dedicated Linux environment with game emulation frontend software running on a small, low-power development board. However, these projects focus on Raspberry Pi hardware.

Lakka's OpenELEC architecture and fast cross-compilation makes it possible to create optimized builds for a variety of hardware. Lakka supports many systems, including development boards, embedded/mobile systems, and tiny PCs. Examples include the Allwinner, iMX6, and Amlogic boards along with builds for 32-bit and 64-bit PC systems. [Learn more in "Hardware Support"](Hardware-support).

## Integration with RetroArch

RetroPie uses [EmulationStation](https://github.com/Aloshi/EmulationStation) as frontend on top of RetroArch and other emulators, while the graphical interface of Lakka is directly coded in RetroArch. This choice offers the following advantages:

 * A single, unified and consistent configuration for all the emulators.
 * No manual joypad configuration, we use RetroArch autoconfig feature and it works for all consoles.
 * Better integration with the frontend: you can pause your game to use savestates, take screenshots, or switch PlayStation CDs and then go back to your game.
 * Less code (so less bugs), and no effort duplication.
 * We encourage developers to port their emulators to RetroArch, with the side effect of making them available on all the platforms supported by RetroArch.
 * The development team of Lakka and RetroArch are composed of the same members, so both projects can benefit from each other.

[Learn more about the systems that Lakka supports](Hardware-support#which-systems-are-supported).

## Built on OpenELEC

Lakka is based on OpenELEC, which provides a number of advantages:

 * A 200mb read-only filesystem you cannot break even with root access.
 * A rock solid update system not based on packages, the whole filesystem and kernel are downloaded and replace the actual system.
 * Cross-compilation: Compiling the whole project including the Linux kernel takes about 2 hours on a good PC.
 * No useless extra packages, we strictly include the dependancy tree of RetroArch.
 * We can version the entire distro under a single git repository, containing all our package recipes, patchsets, kernel configs, etc.
 * The build system will bootstrap itself on a project basis, we compile our specific version of the cross compilers for each project.
 * Lakka is easy to port to new ARM boards.
