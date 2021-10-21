Lakka can display three types of thumbnails for games in playlists:

 * In-game snapshots
 * Title screen snapshots
 * Boxart

Below: An in-game snapshot displayed with a Sega - 32X playlist.
![XMB Thumbnails](images/thumbnails.png)

Lakka provides packs of [thumbnails](https://thumbnailpacks.libretro.com) suitable for use with many emulated systems. These thumbnail packs are recommended for most users and can be installed in two ways:

* **Option A**: Download those packs to a host PC and then [copy the contents of the pack into your Lakka system's Thumbnails directory](Accessing-Lakka-filesystem). 
* **Option B**: [Connect the Lakka system to the internet](Network-settings) and use the built-in thumbnails updater, available from the online update menu within the Lakka settings interface

Once your Thumbnail files are in place, go to `Menu Settings`, and change the `Thumbnails` option to reflect the type of thumbnail you prefer to display.

Users who wish to create their own thumbnails for use with Lakka can do so by naming and locating the image files according to the RetroArch naming convention. Images must use the PNG format and must placed in the Thumbnails directory: `/storage/thumbnails`. Thumbnails should follow this naming convention: `/storage/thumbnails/<Playlist_Name>/<Thumbnail_type>/<Game_Name>.png`

Note: The Thumbnails directory is configurable. If you prefer to store the thumbnails in another location, you can change the `Thumbnails Dir` setting in the `Directory Settings`.
