By E1 Elite @ https://ppmforums.com/post-590841/final-alert-2-yr-v102-patches

FinalAlert2 v1.02 for YR (EXE only, not the installer) is patched with the following:

1. More undo/redo hack from cybermind, raised from 15 to 127:
https://ppmforums.com/viewtopic.php?p=551827#551827

2. Resource hacking for Repeat/AND/OR dropdown fixes:
https://ppmforums.com/viewtopic.php?t=39454

3. Sounds volume have been reduced.

4. Ignore RA2 install path from the registry and use path from FinalAlert.ini only. It allows having individual copies of FA2 for mods. Hack is same as was done by CCHyper and shared by Bittah Commander for FinalSun.

[IgnoreRegistryFA2]
Name=Use FinalAlert.ini RA2 install path
Description=Ignore the RA2 install path from the registry and always use the one from FinalAlert.ini.
Type=FinalAlert2
Offset=0x1FDDB
Original=55 68 3C B1 5C 00 50 55 FF 15 6C 15 59 00
Modified=90 90 90 90 90 90 90 90 90 90 90 90 90 90
Offset=0x1FFDF
Original=55 68 3C B1 5C 00 50 55 FF 15 6C 15 59 00
Modified=90 90 90 90 90 90 90 90 90 90 90 90 90 90
Offset=0x1CB4A4
Original=53 6F 66 74 77 61 72 65 5C 57 65 73 74 77 6F 6F 64 5C 52 65 64 20 41 6C 65 72 74 20 32
Modified=00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

5. Raised the map width, height limit from 200 to 511 on the new map creation screen along with its instructions. Avoid crossing limit of W + H <= 512 and W * H < ~43500 which could cause glitches/crash/hang in FA2.

[MapSizeFA2]
Name=Raises the map width, height limit from 200 to 511.
Description=Raises the 200 limit to 511 when creating new maps.
Type=FinalAlert2
Offset=0xD2F4F
Original=C8 00
Modified=FF 01
Offset=0xD2F59
Original=C8 00
Modified=FF 01

6. Reference to ecahemd is changed to expandmd.

7. FALanguage.ini is modified for high bridge frame's usage. Overwrite the one in the FA2 folder with the one provided. Changes are done for English only. For details check: 
https://ppmforums.com/viewtopic.php?p=572963#572963

8. The coordinates shown on the status bar are now reversed to show X / Y - H (was Y / X - H).

[StatusBarYXToXYFA2]
Name=Statusbar coordinates to be shown as X / Y - H instead of Y / X - H
Description=Coordinates on the statusbar reversed to show X / Y instead of Y / X.
Type=FinalAlert2
Offset=0x5AEFF
Original=8B 7C 24 38 8D 8C 24 58 04 00 00 6A 0A 51 57
Modified=8B 5C 24 30 8D 84 24 58 04 00 00 6A 0A 50 53
Offset=0x5AF40
Original=8B 5C 24 30 8D 84 24 58 04 00 00 6A 0A 50 53
Modified=8B 7C 24 38 8D 8C 24 58 04 00 00 6A 0A 51 57

9. Edit menu items re-ordered and Edit menu popup windows now open centered by default.

10. Teams window: Resized and checkbox options are given some space.

11. AI Trigger Types window: Side dropdown entry changed from 0 None to 0 All, renamed Multi-Side to Side, Weight to InitialWeight and Unittype to TechnoType.

12. Infantry, Unit and Aircraft windows: Resized and arranged components, changed Recruitable to AutocreateNo Recruitable and AI Recruitable to AutocreateYes Recruitable in FALanguage.ini for English. 

13. On new map creation, default LocalSize (visible area) is now set to 3,5,Width-6,Height-11 (was 2,4,Width-4,Height-6). This is to compensate for in-game blackening of the top row, bottom rows cuttoff and increasing 1 cell gap on the sides.
Addresses: 0xB8A77 FC to FA, 0xB8AAB from FA to F5, 0xC5E05 from FC to FA, 0xC5E3A from FA to F5, 0x1CFE20 from 32 to 33 and 0x1CFE22 from 34 to 35.

14. New map creation minimum WidthxHeight is now set to 20x20 (was 16x16). Warning message on map creation are set for less than 20 (was 16) and greater than 511 (was 200). Warning message for Width+Height being greater than 256 is extended to 512.
Addresses: 0xD2F61 from 10 to 14, 0xD2F66 from 10 to 14, 0xD2F6D from 01 to 02, 0x1D0206 from 31 36 to 32 30, 0x1D020D from 32 30 30 to 35 31 31 and 0x1D0232 from 32 35 36 to 35 31 32.

15. Trigger Editor window: Size of description box for action and event tabs is increased so that the descriptions can be viewed without scrolling.

16. Map resize through tool script restriction raised from 200 to 511. Script can contain command like Resize("PositionX","PositionY","NewWidth","NewHeight"); where the parameters are number in cells. For example:
Resize("-8","0","204","207"); // will resize the currect map to new size of 204x207 and place the map contents shifted by 8 cells to the left.
Addresses: 0x1131A5 from C8 00 to FF 01 and 0x1131C3 from C8 00 to FF 01.

17. Map resize through Map popup window upper limit raised from 200 to 511. A second warning message changed to values between 20 to 511 (was 16 and 250) .
Addresses: 0x1B10A and 0x1B138 from C8 00 to FF 01. 0x99D5C, 0x99D75 from 10 to 14 and 0x99D65, 0x99D7D from FA 00 to FF 01. 0x1CF909 from 31 36 to 32 30 and 0x1CF910 from 32 35 30 to 35 31 31.

18. Resize script added to the Scripts folder.

19. Descriptions changed in Tags, ScriptType, TaskForce etc. windows and FALanguage.ini is updated.

20. Added map size limits for the tool to Map resize UI and script.

21. New map default size set to 80x80 (was 50x50).
Addresses: 0xD2F14 from 32 to 50.

22. New TeamType default value for Full and Autocreate checkboxes set to no (was yes).
Addresses: Full - 0xEEEC0 from 20 A6 to 2C B4 and Autocreate - 0xEF138 from 20 A6 to 2C B4.

23. Toolbar - second row removed and buttons from it merged to first row. Brush size also touched for position.
Resources changed - Bitmap [225 : 1031], resource [241 : 225 : 1031].
Second row hiding address - 0x24250 from 03 to 04 (Credits: Bittah Commander).

24. Default global AI Trigger enable checkbox is set as unchecked in map creation window. Text resources related to AI Triggers enabling changed.
Addresses:  0xD2D42 from 01 to 00.

25. Disable Beginner mode (and thereby no message of beginner/advanced modes) by default on first run. Text changed for new map creation radio button for singleplayer map.
Addresses: 0x21BCE from 8A 44 24 1F to 90 90 B0 00

26. Unit window text changed from Follows ID to Follower's ID in FALanguage.ini for English.

27. Hotkeys for menu items. Menu and accelerator resources updated.

28. AI Trigger window improved. Unused Base Defense value is unchecked by default when creating new trigger.
Address 0x1CA6C0 from 31 to 30.

29. Tab stop orders changed in several windows.

30. Dropdown heights increased so as to minimize the use of scrollbars.

31. Search waypoints window improved.

32. Veteran status text appended with (0-200) for pre-placed units in FALanguage.ini for English.

#################################################

Changelog:

Changes (2020-05-10):
- Dropdown heights increased so as to minimize the use of scrollbars.
- Search waypoints window improved.
- Veteran status text appended with (0-200) for pre-placed units in FALanguage.ini for English.
- Tab stop orders changed for most of the windows.

Changes (2020-05-04): 
- AI Trigger window improved. Unused Base Defense value is unchecked by default when creating new trigger. 
- Tab stop orders changed in a few windows. 

Changes (2020-04-03): 
- Hotkeys for menu items. 

Changes (2019-12-26): 
- Second row in toolbar is removed and buttons from it merged to first row. 
- Default global AI Trigger enable checkbox is set as unchecked in new map creation window. 
- Disabled Beginner mode by default on first run. 
- Unit window text changed from Follows ID to Follower's ID in FALanguage.ini. 

Changes (2019-08-31): 
- New map default size set to 80x80 (was 50x50). 
- New TeamType default value for Full and Autocreate checkboxes set to no (was yes). 

Changes (2019-08-30): 
- Added map size limits message for the tool to Map resize UI and script. 

Changes (2019-08-29): 
- Map resize through Map popup window upper limit raised from 200 to 511. 
- Resize script added to the Scripts folder. 
- Descriptions changed in Tags, ScriptType, TaskForce etc. windows and FALanguage.ini is updated. 

Changes (2019-08-27 Patch 2): 
- Map resize through tool script restriction raised from 200 to 511. 

Changes (2019-08-27 Patch 1): 
- On new map creation, default LocalSize (visible area) is now set to 3,5,Width-6,Height-11 (was 2,4,Width-4,Height-6). 
- Trigger Editor window: Size of description box for action and event tabs is increased so that the descriptions 
can be viewed without scrolling. 

Changes (2019-08-26): 
- More undo/redo (from 15 to 127) hack applied (from cybermind). 
- Repeat/AND/OR dropdown fixes for Trigger and Tag windows 
- Ignore RA2 install path from the registry and use path from FinalAlert.ini 
only. It enables having individual copies of FA2 for mods. 
- Low volume sound. 
- New map creation window limit of 200 size for width/height extended with instructions. 
- Reference ecahemd changed to expandmd. 
- FALanguage.ini is modified for high bridge frame's usage. Changes are done for English only. 
- Status bar coordinates are shown as X / Y - H (was Y / X - H). 
- Edit menu items re-ordered and Edit menu popup windows now open centered by default. 
- Teams window: Resized and checkbox options are given some space. 
- AI Trigger Types window: Side dropdown entry changed from 0 None to 0 All, 
renamed Multi-Side to Side, Weight to InitialWeight and Unittype to TechnoType. 
- Infantry, Unit and Aircraft windows: Resized and arranged components, changed Recruitable to 
AutocreateNo Recruitable and AI Recruitable to AutocreateYes Recruitable in FALanguage.ini for English. 
- On new map creation, default LocalSize (visible area) is now set to 2,5,Width-4,Height-11 (was 2,4,Width-4,Height-6). 
This is to compensate for in-game blackening of the top row and bottom rows cuttoff. 
- New map creation minimum WidthxHeight is now set to 20x20 (was 16x16). Warning message on map creation 
are set for less than 20 (was 16) and greater than 511 (was 200). Warning message for Width+Height being greater 
than 256 is extended to 512. 

#################################################
