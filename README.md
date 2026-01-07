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
| Night Elf | X |  | X | X | X | X |  |  |  | X |
| Gnome | X |  |  | X | X |$\color{red}{\textsf{REMOVED}}$ |  | X | X |  |
| Draenei | X | X | X |  | | X | X | X |  |  |
| Orc | X |  | X | X |  | X | X |  | X |  |
| Undead | X |  |  | X | X | X |  | X | X |  |
| Tauren | X | $\color{green}{\textsf{ADDED}}$ | X |  | | X |X  |  |  | X |
| Troll | X |  | X | X | X | X | X | X |  |  |
| Blood Elf |  | X | X | X | X | X |  | X | X |  |

Server-side (DBC/MVQ)
- CharBaseInfo.dbc
- CharStartOutfit.dbc

<details>
	<summary>Changes: Paladin</summary>

### Summary

- Added for Tauren.


### Change (wotlkmangos\playercreateinfo)
  

### Reversal (wotlkmangos\playercreateinfo)


```DELETE FROM playercreateinfo WHERE race = 6 AND class = 2;```

</details>

<details>
	<summary>Changes: Death Knight</summary>

### Summary

- Disabled for Gnomes.


### Change (wotlkmangos\playercreateinfo)
  
```DELETE FROM playercreateinfo WHERE race = 7 AND class = 6;```

### Reversal (wotlkmangos\playercreateinfo)

```INSERT INTO `playercreateinfo` (`race`, `class`, `map`, `zone`, `position_x`, `position_y`, `position_z`, `orientation`) VALUES 
(7, 6, 609, 4298, 2355.05, --5661.7, 426.026, 3.65997);```

</details>

<details>
	<summary>Integration: PlayerBots</summary>

### Summary
This patch is fully comaptible with PlayerBots, due to the provision of the 'ClassRaceProb' string in aiplayerbot.conf.
Further, PlayerBots is not modified in any way by default. This section is present only to provides helpful details for troubleshooting existing playerbots in your SQL database.

### Prevention (aiplayerbot.conf)
If you want to prevent the PlayerBots from auto-generating certain classes, this can be modified with the 'ClassRaceProb' string.
This allows tweaking of race/class combinations, including standalone classes. Further change can be made to disable certain classes outright.

### Change (wotlkcharacters\characters)
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
