# CnCNet Client Quick Start Guide #

A list of instructions to follow to perform a basic set-up of the CnCNet client for Ares-based C&C: Yuri's Revenge mod using the Mod Base.

1. Edit `Resources\GameCollectionConfig.ini`:
   1. Change `InternalName` under section `CustomGame` to your chosen, unique abbreviation (max. 4 characters in length).
   2. Change `UIName` under section `CustomGame` to full name of your mod.
   3. Set `ChatChannel` and `GameBroadcastChannel` under section `CustomGame` to valid IRC channel names. For an example, `#cncnet-X` for `ChatChannel` and `#cncnet-X-games` for `GameBroadcastChannel`, where `X` is replaced by the abbreviation from `InternalName`.
      - **NOTE:** If you wish to register and moderate the channels yourself, you can't use the `cncnet` name in the channel names. In that case, it is recommended to use the full name of the mod instead, f.ex `#customgame` / `#customgame-games`.
   4. Set `IconFilename` under section `CustomGame` to a valid filename of a 16x16px icon to display in CnCNet lobby & CnCNet options. The file (ideally in PNG format) should be placed in `Resources` directory.
   5. Make sure `0=CustomGame` under the `CustomGames` section is uncommented. This can be done by removing the semicolon. 
2. Edit `Resources\ClientDefinitions.ini`:
   1. Set `LocalGame` under section `Settings` to match the abbreviation from custom game's `InternalGame`.
   2. Set `LongGameName` under section `Settings` to full name of your mod.
   3. Set `WindowTitle` under section `Settings` to what you wish to display in client window titlebar.
   4. *Optional:* If you are planning on setting up the updater, set `ModMode` under section `Settings` to `false`. For information on how to set up the updater, refer to the [updater documentation](Updater.md).
3. Edit `Resources\GameOptions.ini`:
   1. Change `Sides` list under section `General` to match the `Countries` list from your `rulesmd.ini`.
      - If you wish to list the `Countries` in different order between client and `rulesmd.ini`, use `InternalSideIndices` to override the used side (country) indices for `Sides` list to match the actual order in `rulesmd.ini`.
   2. Set up random selectors under section `RandomSelectors` to match the `Sides` list, or remove keys under the section if don't wish to use additional random side selectors.
   3. If you have changed in-game colors, or added more available multiplayer colors through use of Ares, adjust the colors list under section `MPColors` accordingly.
4. Edit `Resources\FHCConfig.ini`:
   1. Adjust the filenames list under section `FilenameList` accordingly if need to remove or add additional files that are compared between players to see if anyone might be cheating by modifying files. The list included by default works well if `expandmd99.mix` contains all INI files and a copy of `shroud.shp`. Certain client files like `FHCConfig.ini` itself are always included in the check even if absent from `FilenameList`.
   2. *Optional:* `CalculateGameExeHash` under section `Settings` can be set to `true` if it is guaranteed that the game executable (`gamemd.exe`) is identical between all players. With almost all C&C: Yuri's Revenge mods, as the game files are not distributed together with mods, this is not the case.
