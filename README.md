# CnCNet Client Yuri's Revenge Mod Base #

This repository contains a collection of files that can be used as a base to adapt [Rampastring's](https://github.com/Rampastring) [CnCNet Client](https://github.com/CnCNet/xna-cncnet-client) for use with Command & Conquer: Yuri's Revenge mods, particularly those also using [Ares DLL](https://ares.strategy-x.com/) _(not included in this repository or any of the releases)_.

The contents of this repository can be broken down into the following categories (also separated into folders):

- **[Client Files](ClientFiles)**: Contains compiled client binaries, an example client configuration & assets as well as all Command & Conquer: Yuri's Revenge maps (including the official map pack maps) and preview images generated for them. Source code for the client binaries included in this repository can be found [here](https://github.com/CnCNet/xna-cncnet-client).
- **[Tools](Tools)**: Contains tool software that may be helpful for or required by the mod developers using the client. Currently this includes version file writer tool (source code for which can be found [here](https://github.com/Starkku/VersionWriter)) which is used for the client's updater feature.
- **[Miscellaneous](Miscellaneous)**: Contains assorted files that are not additional software or part of the client configuration. Currently this includes update server script files used with the client's updater feature.
- **[Documentation](Documentation)**: Contains documentation and guides for client features & configuration.

Latest version can be downloaded [here](https://github.com/Starkku/cncnet-client-mod-base/releases/tag/latest).

Other releases can be browsed at https://github.com/Starkku/cncnet-client-mod-base/releases.

## Documentation Index

- [Quick Start Guide](Documentation/QuickStartGuide.md)

More documentation can be found in repository for the client itself [here](https://github.com/CnCNet/xna-cncnet-client/tree/develop/Docs).

Credits
-------

- [Rampastring](https://github.com/Rampastring) - Original CnCNet Client & updater, example DTA update server scripts
- [Starkku](https://github.com/Starkku) - Client contributions, extended client updater, [VersionWriter](https://github.com/Starkku/VersionWriter), some client graphical assets, client configuration, documentation
- [Kerbiter](https://github.com/Metadorius) - Client contributions, draft of the updater documentation, original player status indicator icons
- [tomsons26](https://github.com/tomsons26) - Edited Yuri's Revenge UI assets originally for use with CnCNet Yuri's Revenge
- [Sad Pencil](https://github.com/SadPencil) - QRes DPI awareness fix

Screenshots
-------
![Screenshot of client main menu.](modbaseclient-mainmenu.png?raw=true "Main menu in example configuration.")
![Screenshot of client skirmish game lobby.](modbaseclient-skirmishlobby.png?raw=true "Skirmish game lobby in example configuration.")