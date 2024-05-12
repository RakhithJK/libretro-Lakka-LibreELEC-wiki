## Prerequisites

We assume that git remote `upstream` is the Lakka upstream (libretro/Lakka-LibreELEC) repository. These notes are written for the v4.3 release, adjust your steps/typing accordingly for other releases/versions. It is also assumed that you have write privilege to the [Lakka's GitHub repository](https://github.com/libretro/Lakka-LibreELEC). You should also have an user account and root access on the Lakka download server (le.builds.lakka.tv).

In case of doubt ask vudiq ;-)

## Prepare local repository

First of all update the repository to the latest commit or to the commit the release should be based on:

```
$ git pull
```

Then tag the commit that the release should be build from, for example tagging commit 656c5f0506d1a44b696916f4d27915b5cd8004f7 for v4.3:

```
$ git tag v4.3 656c5f0506d1a44b696916f4d27915b5cd8004f7
```

Push the tag to the repository:

```
$ git push upstream v4.3
```

Now checkout the tagged commit:

```
$ git checkout v4.3
```

## Build the release files

Edit `distributions/Lakka/version` and adjust `LIBREELEC_VERSION` - replace `devel` with proper version (e.g. `4.3`). It should be same version as quoted in `OS_VERSION`.

Start the build of the images/release files by running the `build_all.sh` script:

```
$ ./build_all.sh
```

The build process will take some time, on 8-core / 16-threads Ryzen 7 3700X CPU it takes approximately 1.5 hours per image. The progress will be displayed during the building/compilation, if any package fails to build, it will finish building current packages and then move to the next image. Wait until all builds are finished.

Move finished release files from `target/` folder somewhere else for safekeeping, e.g.:

```
$ mkdir release
$ mv target/* release/
```

If some builds failed, investigate the reason for it. Maybe a simple manual rebuild of the package will be enough. You can use the `status` file of the project to retrieve the job id, for example:

```
$ cat build.Lakka-Generic.i386/.threads/status
```

Job ID is the number after slash (e.g. `[03/042]` means build slot #3 and job ID 42). To see the logfile, for example:

```
$ vim build.Lakka-Generic.i386/.threads/logs/42.log
```

To manually rebuild the package, use for example:

```
$ PROJECT=Generic ARCH=i386 ./scripts/build ffmpeg
```

In case you had to edit some files and commit new changes to fix the build errors, the old tag has to be removed and new tag created:

```
$ git tag --delete v4.3
$ git push upstream --delete v4.3
$ git tag v4.3 <commit_hash>
$ git push upstream v4.3
```

If no changes to the repository files were needed, we need to build only the remaining images, edit `build_all.sh` script and remove projects/devices from `targets`. Otherwise all projects/devices have to be rebuild, but now it will be faster, as the build cache is ready. Then run the build script again for the remaining projects/devices:

```
$ ./build_all.sh
```

Move finished release files from `target/` folder to the `release/` folder:

```
$ mv target/* release/
```

Again, if some builds failed, repeat steps above, until you have release files for all projects/devices in folder `release/`.

## Prepare GitHub release

After all release files are ready, create a release draft on GitHub. Go to [Lakka's GitHub releases page](https://github.com/libretro/Lakka-LibreELEC/releases) and click on the <kbd>Draft a new release</kbd> button. Then you select the tag, as title use the same as tag name (e.g. `v4.3`). For now leave the description empty. And finaly click on the <kbd>Publish release</kbd> button.

You can also create a release using command line:

```
$ gh release create v4.3
```

It will be created interactively by answering questions. For title leave the default value (same as tag - just press <kbd>Enter</kbd>. For release note select `Leave blank` (we will take of this later). For prerelease just confirm default value 'N', but if you are releasing a "release candite" version, type `y` and press <kbd>Enter</kbd>. And final step - select `Publish release`.

## Push release files to GitHub

These files are used by the Raspberry Pi Imaging Utility to flash images to SD cards / USB thumb drives or also to install directly to the RPi hardware. And as the files are stored on the GitHub servers, they also provide some kind of a backup to the download server.

First make sure that `gh` is set up to push to the correct remote, in our example the `upstream` remote (libretro/Lakka-LibreELEC):

```
$ gh repo set-default
```

Assuming the release files are stored in `release/` subfolder, each project/device in separate subfolder, following command will upload all `.img.gz`, `.tar` and relevant checksums to the release page:

```
$ gh release upload v4.3 release/*/Lakka-*.img.gz* release/*/Lakka-*.tar*
```

This will also upload tarballs for noobs (and their checksums), so after the upload is finished, remove them - navigate to the release draft page and click on the cross button next to these files.

## Copy files to the download server

Use `scp` or other tools to copy release files to the Lakka download server (le.builds.lakka.tv):

```
$ scp -r release user@le.builds.lakka.tv:~/
```

## Update Raspberry Pi Imaging Utility json file

Login to the Lakka download server (le.builds.lakka.tv) via SSH. In the `release/` subfolder you should have a script called `lakka_rpi_imager.sh`. If not, grab it from vudiqs home folder, `lakka-scripts` subfolder (use your root privilege). The script takes 3 parameters in following order:
- version, e.g.: `4.3` (note: no `v`)
- release date, e.g.: `2023-01-18` (year-month-day)
- path to release files, e.g.: `./` for current folder (either relative path to the current working directory, or absolute path)

```
$ cd ~/release/
$ ./lakka_rpi_imager.sh 4.3 2023-01-18 ./
```

After the script is finished running, you should have json file ready in your current (`~/release/`) folder, e.g. `rpi-imager-4.3_2023-01-18.json`. Copy this file to the web files, remove json file in in the `~/release/` folder and update the symlink to point to the latest json file.

```
$ sudo cp ~/release/rpi-imager-4.3_2023-01-18.json /var/www/le-builds.lakka.tv/.rpi-imager/
$ rm ~/release/rpi-imager-4.3_2023-01-18.json
$ sudo ln -sf rpi-imager-4.3_2023-01-18.json /var/www/le-builds.lakka.tv/.rpi-imager/rpi-imager.json
```

From this moment users can download/flash the images using the utility.

## Deploy release files to the download server

Login to the Lakka download server (le.builds.lakka.tv) via SSH. In the `release/` subfolder you should have a script called `lakka_web_deploy.sh`. If not, grab it from vudiqs home folder, `lakka-scripts` subfolder (use your root privilege). The script takes no parameters, it looks for release files in current working directory and moves them to the correct location in the web root (therefore needs root privileges):

```
$ cd ~/release/
$ sudo ./lakka_web_deploy.sh
```

From this moment users can update their Lakka devices using the `Online Updater` in RetroArch.

## Clean-up

You can now remove the `release/` subfolder in the build repository (not in your home on the Lakka download server - keep this folder with the scripts for future). Also revert all temporary changes to the repository files (e.g. changes to `distributions/Lakka/version` or `build_all.sh`) and exit the detached HEAD branch:

```
$ rm -r release/
$ git checkout -- ./
$ git switch -
```

## Release article for Lakka web site

You need to have fork of [Lakka web site repository](https://github.com/lakkatv/lakka-website). You can create the fork and clone the repository also via command line in your home folder. Lakka website uses the GitHub wiki to generate content under `lakka.tv/doc/` and it is set up as a subrepo/submodule of the website repository.

```
$ cd ~
$ gh repo fork https://github.com/lakkatv/lakka-website --clone
$ cd lakka-website
$ git submodule update --init --recursive
```

As first order of business create new branch (give the branch a descriptive name) and update the `doc/` section (pull changes from Lakka GitHub Wiki):

```
$ git checkout -b lakka-release-v4.3
$ git -C content/doc/ pull origin master
```

Edit `nanoc.yaml` file and update the URLs for the download links (search for line starting with `release:` and the URLs should be below this line), i.e. replace old version with new version. Also in case there are new images for certain project, add them with new unique key, e.g. to add Orange Pi 4 LTS (which is RK3399 device) add following line somewhere where other RK3399 URLs are located:

```
  rockchip.rk3399_orangepi4lts: https://le-builds.lakka.tv/RK3399.aarch64/Lakka-RK3399.aarch64-4.3-orangepi-4-lts.img.gz
```

In case new device/download link was added, you need to adapt also the individual download page by adding a download button. For example to add download button for the Orange Pi 4 LTS to RK3399 download page you have to edit the file `content/get/linux/rockchip.html`. Find the section with download buttons, copy one section and change as necessary. The result should look like this:

```

<p class="dl">
  <a href="<%= @config[:release][:'rockchip.rk3399_orange_pi4lts'] %>">Download Lakka
  <span class="details">for Orange Pi 4 LTS</span></a>
</p>

```

If a device is removed, there are two options - either keep the URL in `nanoc.yaml` pointing to the latest release (older than current) for this device, or remove the download button for this device in `content/get/linux/xxx.html` file. By the way - there are also `mac` and `windows` paths, but you can ignore them for the release - they use the same files thanks to symlinks.

Now is the time to write the release notes/article. Create a new folder/path (change the year/month/day and article short name in the example accordingly) and copy previous release article as our base for the current release article:

```
$ mkdir -p content/articles/2023/01/18/lakka-4.3/media
$ cp content/articles/2022/04/27/lakka-4.2.md content/articles/2023/01/18/lakka-4.3.md
```

Edit `content/articles/2023/01/18/lakka-4.3.md`. In the `Release summary` section describe the most important changes, bugfixes, feature and stability enhancements since the previous release. Mention any new cores that were added or discontinued. Remaining sections may stay unchanged.

Regarding the thumbnail for the release article - either create your own or ask for help in the community. The image size should be 720px x 500px, PNG is preferred. When you have your thumibnail ready, upload it to your home (use WinSCP, scp from shell or other tools) and copy it to the `media` folder.

```
$ cp ~/verynicethumbnail.png content/articles/2023/01/18/lakka-4.3/media/thumb.png
```

The file name should be `thumb.png`, as this file name is already used in the article `.md` file. If you use different file name for the thumbnail, you must correct the file name for the thumbnail in the `.md` file. You can also copy other images to the `media` folder and add them to the release article `.md` file using the markdown syntax, for example `![Alternate text if media file is missing](media/screenshot-game-psx.png "Image title")`.

So your article is ready, links have been updated, devices added/removed. Show the article to some other maintainers for their input and update it based on the feedback. Now you can commit the changes:

```
$ git add ./
$ git commit --message="Lakka 4.3 release article, links updates, doc updates"
$ git push origin
```

You should see that the branch was pushed to your fork and also a notice with a URL for a pull request. Copy this URL, paste it into your browser and proceed with the pull request in the browser. Request a merge from somebody with write privileges to the `lakkatv/lakka-website` repository. After your pull request is merged, it can take up to an hour until the web page (https://www.lakka.tv) is updated with the new content.

## Update the release on GitHub

After the Lakka web page is updated, open the release article and copy the URL (make sure to use `https://`). Open the [releases page](https://github.com/libretro/Lakka-LibreELEC/releases) and click on the pen icon to edit the release. Paste the URL into the description field, scroll down and click <kbd>Update release</kbd>.

### The end
