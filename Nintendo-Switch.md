# Installation instruction for Nintendo Switch

1. Extract the 7z archive to first (FAT32) partition of the SD card
2. Extract [hekate](https://github.com/CTCaer/hekate/releases/download/v5.5.6/hekate_ctcaer_5.5.6_Nyx_1.0.3.zip) files if not already on the SD card
3. Boot hekate with TegraRCMGui, fusee-launcher, RCM Loader (Android app) or any other injection method
4. Under Nyx Options dump joyons after they have been paired in HOS (official Switch OS; only required once, or after you have to pair the joycons with Switch again, e.g. you paired them with different device)
5. Under More Configs press `lakka` to boot Lakka

It is advised to use Hekate UMS to do any SD card changes. This is due to bad design of the SD card reader in the console, which has tendency to break pins in the connector for the SD card reader on the motherboard.