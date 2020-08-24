# Extended CnCNet Client Updater #

This document attempts to explain the usage and features of the extended CnCnet Client updater that is included with the client files in this repository. Some of the details may overlap with the regular CnCNet Client updater, however many features presented here are absent in it.


Updater-Related Files
-------------------

**WARNING: None of the included example configuration files are suitable for as-is usage and require to be edited to suit the mod structure and redistribution methods!**

### Developer Files
**These files are needed only by the mod developer and aren't meant to be redistributed to others!** 
- **Version File Writer**: Software that writes a version file based on info in `VersionConfig.ini` and copies all the files a mod developer needs to put on the server to a `VersionWriter_CopiedFiles` subdirectory in the current working directory.
- **Update Server Scripts** (`preupdateexec` and `updateexec`): Script files that can be used to rename, move or delete files & directories. They are downloaded and executed by updater before and after the update, respectively. They can be put on the server in the same folder specified in download mirrors. Note that changes made by `preupdateexec` **will not** be reverted even if the update process itself fails afterwards. Additionally both of the scripts are executed regardless of current local or server version state & info.

### Distributable Files
- **Updater Configuration File** (`Resources/UpdaterConfig.ini`): Client [updater configuration](#updater-configuration) file which sets the download mirrors for the updater and available custom component info. Requires [a client with extended updater support](#client-support). If no such file is found, client falls back to using `updateconfig.ini` that is used by the original XNA CnCNet Client which uses a different syntax and does not allow setting custom component info.
- **Second-Stage Updater** (`clientupdt.dat`): A second-stage updater executable that copies the files to their correct places after they've all been downloaded and then launches the client again after it is done. Normally it has a hardcoded list of launcher executable names it looks for, and if it doesn't find any it won't launch the client again. The executable included here will attempt to read the launcher executable name from `LauncherExe` key in `Resources/ClientDefinitions.ini` if none from the hardcoded list are present.

Basic Usage
-----------

## Quick Guide
1. Have a web server set up and create a publicly accessible directory from which to download your updates from.
2.  On your client configuration with support for extended updater, add URL of the aforementioned directory to list of available download mirrors in `Resources/UpdaterConfig.ini`. 
3. Make changes to files and `VersionConfig.ini`.
4. Run `VersionWriter.exe`.
5. Upload the contents of the `VersionWriter_CopiedFiles` and [update server scripts](../Tools&#32;&&#32;Misc/Update&#32;Server&#32;Scripts) to the aforementioned directory on the web server.

## Detailed Instructions
To have automatic updates via XNA CnCNet client, an update server needs to be set up. The update server needs to be a web server with the files accessible through HTTP (**not HTTPS**, unless you want to ditch Windows XP support), which would then allow them to be downloaded by client during the update process. The URL path to the file (sans update location part) has to replicate the local path to the file relative to mod folder in order to be succesfully downloaded (for example, with update location `http://your.test/location/of/updates/` the file `Resources/clientdx.exe` would need to be accessible at `http://your.test/location/of/updates/Resources/clientdx.exe` URL). Besides the update server scripts, the updater does not explicitly require any other files or specific software to exist or run on the update web server.

To set up an update information needed to produce the files to upload on a server edit `VersionConfig.ini` file to include all of the redistributed files (or updated files only if you're saving on bandwidth and don't want to allow full downloads). Each time you need to push an update to your players (also if you change something in `VersionConfig.ini`) you have to change the version key under `[Version]` section in aforementioned configuration file so the CnCNet client prompts for an update. In case you need to force users to download an update manually you can change a key under `[UpdaterVersion]` section. After that run `VersionWriter.exe` and upload the contents of the `VersionWriter_CopiedFiles` to your update server along with updater scripts.

Refer below for a more comprehensive explanation of both version writer's and updater's features & configuration files.


Features
-------

### Version File Writer
The example `VersionConfig.ini` included with the version writer contains comments explaining most of the functionality and features.

`VersionWriter.exe` accepts a single command-line argument that can be used to set its working directory - this allows running VersionWriter from outside the mod directory itself.

#### Options
These are set under `[Options]` in `VersionConfig.ini`.
- `EnableExtendedUpdaterFeatures`: If set, enables the extended updater features such as compressed archives, updater version and manual download URL.
- `RecursiveDirectorySearch`: If set, will go through every subdirectory recursively for directories given in `[Include]`.
; If set, will always create two version files - one with everything included (version_base) and the proper, actual version file with only changed files (version). 
; version_base should be kept around as it is used to compare which files have been changed next time VersionWriter is ran.
- `IncludeOnlyChangedFiles`: If set, version file writer will always create two version files - one with everything included (`version_base`) and the proper, actual version file with only changed files (`version`). Note that `version_base` should be kept around as it is used to compare which files have been changed next time version file writer is ran.
- `CopyArchivedOriginalFiles`: If set, original versions of archived files will also be copied to copied files directory.
- `UseLegacyArchiveFormat`: If set, will use legacy archived file info format. Only enable in case of compatibility problems when migrating from older client / updater versions that had compressed archive and not wishing to resort to multi-stage updates through client. **New users should not use this option.**

#### Updater Version & Manual Download URL
Setting `[UpdaterVersion]` in `VersionConfig.ini` writes this information to the `version` file and allows developers to control which versions are allowed to download files from the version info through the client. Mismatching updater versions between local and server version files will suggest users to download update manually through updater status message. Absent or malformed updater version (both local & server) is equivalent to `N/A` and updater will bypass the mismatch check entirely if server  updater version is set to this or absent.

Additionally setting `[ManualDownloadURL]` will, in addition to displaying the updater status message, also bring up a notification dialog with the provided URL as a download link in case a updater version mismatch occurs.

#### Compressed Archives
The extended updater supports downloading and uncompressing LZMA-compressed data archives. Files that are to be compressed should be included under `[ArchiveFiles]` in `VersionConfig.ini`. Note that they still need to be included through `[Include]` in the first place. As a result there would be information in the `version` file which allows the client, assuming the modified updater is in use, to figure out it is supposed to download the archive instead, and instead of the original files the compressed files with `.lzma` extension are placed to the `VersionWriter_CopiedFiles` folder.

#### Custom Components
Custom components are available even with the original XNA CnCnet Client, but since the IDs and filenames are hardcoded in the updater, their usage is limited. Custom component info for the updater can be set in `Resources/UpdaterConfig.ini`, see below for more info. For version file writer, any custom components should be included under `[AddOns]`, using syntax `ID=filename` as shown in the example `VersionConfig.ini`. Custom component filenames **should not** be listed under `[Include]`. The filenames can be listed under `[ArchiveFiles]` to enable use of compressed archives.

- Custom component download file path (in `Resources/UpdaterConfig.ini`) accepts absolute URLs and uses them properly, so it's possible to define custom components which have to be downloaded from elsewhere.

### Updater Configuration
The example `Resources/UpdaterConfig.ini` included with client files contains comments explaining most of the functionality and features.

Only currently supported global updater setting under `[Settings]` is `IgnoreMasks` that allows customizing the list filenames that are exempted from file integrity checks even if they are included in `version` file.

#### Download Mirrors

List of available download mirrors from which to download version info and files from. Listed as comma-separated values under `[DownloadMirrors]`, containing URL, UI display name and location. Location is optional and can be omitted.

Omitting the download mirrors list will default to the hardcoded list for currently set mod / game if available. Updater and Updater & Component options in client options will be unavailable if no download mirrors are found.

#### Custom Components
List of custom components available for the updater. Listed as comma-separated values under `[CustomComponents]`, containing custom component ID used in the `version` file, download path / URL, local filename, flag that disables archive file extensions for download path / URL.

Download path / URL supports absolute URLs, allowing custom components to be downloaded from location outside the current update server but also restricts it to one download location instead of one per each download mirror.

Download path archive file extension disable flag is a boolean value (yes/no, true/false), is optional and defaults to false.

Omitting the custom components list will default to the hardcoded list for currently set mod / game if available. Custom components and the Components tab in client options will be unavailable if no custom component info is found.


Client Support
--------------

It's recommended to use one of the following client forks which include the extended updater features:
- Client included in this repository - source code available [here](https://github.com/Starkku/xna-cncnet-client/tree/mod-base)
- [Kerbiter's modified client](https://github.com/Metadorius/xna-cncnet-client)

The extended updater library (`DTAUpdater.dll`) should theoretically be backwards compatible with all modern XNA CnCNet client variants, though not all of the extended updater features will be available. Not using it with a corresponding client version is generally speaking advised against and not really supported in any real capacity.
