# Fylgja WoW
CMaNGOS WOTLK server with loreful classic+ features

All patch files go in the client-side Data\ folder.
All build\dbc files go in the server-side <build>\dbc folder.
All SQL DB edits are made via provided command-line scripts.

## patch-9.mvq

Rebalances race/class combinations to better fit lore.

|       | Warrior | Paladin | Hunter | Rogue | Priest | Death Knight | Shaman | Mage | Warlock | Druid |
| --- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Human | X | X |  | X | X | X |  | X | X |  |
| Dwarf | X | X | X | X | X | X |  |  |  |  |
| Night Elf | X |  | X | X | X | $\color{red}{\textsf{REMOVED}}$ |  |  |  | X |
| Gnome | X |  |  | X | X | $\color{red}{\textsf{REMOVED}}$ |  | X | X |  |
| Draenei | X | X | X |  | | $\color{red}{\textsf{REMOVED}}$ | X | X |  |  |
|       | Warrior | Paladin | Hunter | Rogue | Priest | Death Knight | Shaman | Mage | Warlock | Druid |
| Orc | X |  | X | X |  | $\color{red}{\textsf{REMOVED}}$ | X |  | X |  |
| Undead | X |  |  | X | X | X |  | X | X |  |
| Tauren | X | $\color{green}{\textsf{ADDED}}$ | X |  | | $\color{red}{\textsf{REMOVED}}$ | X |  |  | X |
| Troll | X |  | X | X | X | $\color{red}{\textsf{REMOVED}}$ | X | X |  |  |
| Blood Elf |  | X | X | X | X | X |  | X | X |  |

Client-side

- patch-9.mvq

Server-side

- CharBaseInfo.dbc
- CharStartOutfit.dbc


### Implementing patch 9 changes

1a. Add the relevant race/class row to CharBaseInfo.dbc.

1b. Add the relevant race/class row to CharStartOutfit.dbc.

2. Save both and import them into patch-9.mvq.

3. Copy the updated .dbc files to your server \dbc folder.

3. Add the relevant race/class row to wotlkmangos\playercreateinfo:

```INSERT INTO `playercreateinfo` (`race`, `class`, `map`, `zone`, `position_x`, `position_y`, `position_z`, `orientation`)
VALUES
(X, X, X, X, Y, Y, Y, Z);```

5. Ensure the updated patch-9.mvq is in the \Data folder of your World of Warcraft client.

### Removing patch 9 changes

1a. Delete the relevant race/class row from CharBaseInfo.dbc.

1b. Delete the relevant race/class row from CharStartOutfit.dbc.

2. Save both and import them into patch-9.mvq.

3. Copy the updated .dbc files to your server \dbc folder.

4. Remove the relevant race/class row from wotlkmangos\playercreateinfo:

```DELETE FROM playercreateinfo WHERE race = X AND class = Y;```

5. Ensure the updated patch-9.mvq is in the \Data folder of your World of Warcraft client.

<details>
	<summary>Changes: Paladin</summary>

### Summary

- Added for Tauren.

</details>

<details>
	<summary>Changes: Death Knight</summary>

### Summary

- Disabled for all races except Humans, Dwarfs, Undead, and Blood Elves.

</details>

<details>
	<summary>Integration: PlayerBots</summary>

### Summary
This patch is fully comaptible with PlayerBots, due to the provision of the 'ClassRaceProb' string in aiplayerbot.conf.
Further, PlayerBots is not modified in any way by default. This section is present only to provides helpful details for troubleshooting existing playerbots in your SQL database.

### Action (prevent conflicting race/class characters)
If you want to prevent the PlayerBots from auto-generating certain classes, this can be modified with the 'ClassRaceProb' string.
This allows tweaking of race/class combinations, including standalone classes. Further change can be made to disable certain classes outright.

### Action (remove conflicting race/class characters)
Server failing to launch due to existing playerbots being illegal? Follow this process.

1. Delete the cursory data for the characters in question:

```DELETE FROM character_spell WHERE guid IN (SELECT guid FROM characters WHERE race = X AND class = Y);```

```DELETE FROM character_inventory WHERE guid IN (SELECT guid FROM characters WHERE race = X AND class = Y);```

```DELETE FROM character_talent WHERE guid IN (SELECT guid FROM characters WHERE race = X AND class = Y);```

3. Now delete the character data itself:

```DELETE FROM characters WHERE race = X AND class = Y;```

</details>

## patch-10.mvq

TBD
