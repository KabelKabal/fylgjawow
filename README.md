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
| Gnome | X |  |  | X | X |X |  | X | X |  |
| Draenei | X | X | X |  | | X | X | X |  |  |
| Orc | X |  | X | X |  | X | X |  | X |  |
| Undead | X |  |  | X | X | X |  | X | X |  |
| Tauren | X | $\color{green}{\textsf{ADDED}}$ | X |  | | X |X  |  |  | X |
| Troll | X |  | X | X | X | X | X | X |  |  |
| Blood Elf |  | X | X | X | X | X |  | X | X |  |

Server-side (DBC)
- CharBaseInfo.dbc
- CharStartOutfit.dbc

### Changes: Death Knight

Addition

DELETE FROM playercreateinfo WHERE race = 5 AND class = 6;

Reversal

INSERT INTO `playercreateinfo` (`race`, `class`, `map`, `zone`, `position_x`, `position_y`, `position_z`, `orientation`) 
VALUES
(7, 6, 609, 4298, 2355.05, --5661.7, 426.026, 3.65997);


## patch-10.mvq

TBD
