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

Server (DBC)
- CharBaseInfo.dbc
- CharStartOutfit.dbc


### Server Action (add race/class combination)

1. Add the relevant row to wotlkmangos\playercreateinfo:

```INSERT INTO `playercreateinfo` (`race`, `class`, `map`, `zone`, `position_x`, `position_y`, `position_z`, `orientation`)
VALUES
(7, 6, 609, 4298, 2355.05, --5661.7, 426.026, 3.65997);```

### Client Reversal (remove race/class combination)

1. Delete the relevant race/class row from CharBaseInfo.dbc.

3. Save it and import it into patch-9.dbc.

3. Ensure patch-9.dbc is in the Data folder of your World of Warcraft client.

### Client Reversal (remove race/class combination)

1. Remove the relevant race/class row from wotlkmangos\playercreateinfo:

```DELETE FROM playercreateinfo WHERE race = X AND class = Y;```

2. Copy the updated CharBaseInfo.dbc (from Client Reversal steps) tp your server dbc folder.

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
