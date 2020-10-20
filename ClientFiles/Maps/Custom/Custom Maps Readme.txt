Any custom maps you made or downloaded are to be placed in this directory. 
Custom maps need to have .map file extension.

The game mode of custom maps is defined in [Basic] -> GameMode. Only existing gamemodes are accepted values.

Following keys are also read from map file's Basic section.

Name                        - Display name of map in match setup.
Author                      - Display author of map in match setup.
MaxPlayer                   - Maximum amount of players who can play on the map. On co-op maps, this is the number of players that can join from match setup, not total number of players counting pre-set ones.
ClientMaxPlayer             - Can be used instead of MaxPlayer (which map editor might override), and has higher precedence than it as well.
IsCoopMission               - If set to yes, tells the client this map uses special logic associated with co-op maps.
Briefing                    - Co-op / challenge map briefing text. @ is a newline character.
DisallowedPlayerSides       - Comma-separated list of side indices to disallow from players on co-op maps.
DisallowedPlayerColors      - Comma-separated list of colors indices to disallow from players on co-op maps.
ClientMultiplayerOnly       - Allow to be played in multiplayer only.
HumanPlayersOnly            - Disallow AI players. Requires ClientMultiplayerOnly to be set to true.
ForceRandomStartLocations   - Force no preset starting locations. Does not work on IsCoopMission=true maps.
ForceNoTeams                - No preset teams allowed on the map. Does not work on IsCoopMission=true maps. Might also want to enforce no ingame allying through ForcedOptions if using this.

Sections ForcedOptions and ForcedSpawnIniOptions are also parsed from map files. Look at MPMaps.ini under INI directory for a reference how to set them up.

To get a custom map preview, use Map Renderer included in Map Editor\Map Renderer to render a preview. Enable thumbnail output (make sure aspect ratio matches the size of the map preview box (837,380)) and rename thumb_*.png to match map filename (e.g customap.map & custommap.png).
