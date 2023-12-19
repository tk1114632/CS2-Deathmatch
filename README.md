# CS2 Deathmatch plugin
CS2 Deathmatch plugin for [CounterStrikeSharp](https://github.com/roflmuffin/CounterStrikeSharp).

### Main features
- [Weapon selection](#how-weapon-selection-works)
- [Spawns editor](#spawns-editor)
- [Creating custom modes (multicfg)](#creating-custom-modes)
- [Weapon restrict for custom modes](#blocked-weapons-list)
- Free For All (FFA)
- Spawn protection
- Refill ammo or health per kill/headshot/killstreak

### To-do list
- Client preferences

<h1 align="center">Wiki</h1>

### Installation
1. Unzip into your servers `csgo/addons/counterstrikesharp/plugins/` dir
2. Restart server
3. Configure config files and custom modes
<h1></h1>

### Configuration
```/game/csgo/addons/counterstrikesharp/configs/plugins/Deathmatch/Deathmatch.json```
|   | What it does |
| ------------- | ------------- |
| `free_for_all`  | If the game will be FFA or Team. - `true` or `false` |
| `custom_modes`  | Allow the custom modes (multicfg)? - `true` or `false` |
| `custom_modes_interval` | Works only if custom modes is enabled - `minutes` |
| `map_start_custom_mode` | Which custom mode will the map start with? - `ID of mode from custom_modes.json` |
| `spawn_protection_time` | How long will the spawn protection be? - `seconds` |
| `round_restart_time` | How long will it take for the round to restart when a new mode is selected - `seconds` |
| `hide_round_seconds` | Display the round timer? - `true` or `false` |
| `reffil_ammo_kill` | Refill ammo when a player eliminates someone? - `true` or `false` |
| `reffil_ammo_headshot` | Refill ammo when a player eliminates someone with headshot? - `true` or `false` |
| `refill_health_kill` | How much health does a player regenerate when they eliminate someone? - `number` |
| `refill_health_headshot` | How much health does a player regenerate when they eliminate someone with headshot? - `number` |
<h1></h1>

### How Weapon Selection works
- Players can set their primary and secondary weapons using the buy menu.
- They just need to purchase a weapon once, and it will be saved.
- If the saved weapon is in the blocked weapons, the player will not receive it upon spawning.
<h1></h1>

### Spawns Editor
- Spawn points must be added more than originally present on the map, because the plugin overwrite the default spawns.
- So for example: If map de_mirage contains 10 CT spawns and 8 T spawns, so you need to create at least 10 CT spawns and 8 T spawns.
<br>

- Commands (permission: @css/root): <br>
`css_dm_editor` - Enable/disabled editor mode<br>
`css_dm_addspawn_ct` - Add a new CT spawn at your curent position <br>
`css_dm_addspawn_t` - Add a new T spawn at your curent position<br>
`css_dm_removespawn` - Remove a nearest spawn
<h1></h1>

### Creating Custom Modes
```/game/csgo/addons/counterstrikesharp/plugins/Deathmatch/custom_modes.json```
- The default mode is always [ID 0](https://i.imgur.com/mbmiOF6.png), so even if you have custom_modes turned off in the config, the game will follow the data set for the mode with [ID 0](https://i.imgur.com/mbmiOF6.png).
- When creating a custom mode, pay attention to the mode ID. Modes must be consecutive starting from 0, and no numbers should be skipped; otherwise, an error will occur.

- <b>Parameters for custom modes</b>
1. `mode_name` - What will the mode be named?
2. `armor` - What type of armor will players receive at spawn? <b>0</b> - None | <b>1</b> - Armor Only | <b>2</b> - Armor and Helmet
3. `only_hs` - Will this mode be only headshots? <b>true</b> or <b>false</b>
4. `primary_weapon` - Which weapon will be the primary? If none, leave blank
5. `seconday_weapon` - Which weapon will be the secondary? If none, leave blank
6. `allow_saved_weapons` - Disallowing saved weapons is useful in cases where, for example, a new mode like 'Only Rifles' started, and a players saved weapon is a Shotgun. This serves as protection to prevent the player from equip a Shotgun weapon in such cases. So if primary_weapon/secondary_weapon or is allowed all weapons set it true. Avaible values <b>true</b> or <b>false</b>
7. `allow_select_weapons` - Allow select the weapons throung the buy menu ? <b>true</b> or <b>false</b>
8. `weapons_type` - Which type of weapons can be set through the buy menu? Avaible values: <b>all</b>, <b>rifles</b>, <b>pistols</b>, <b>smgs</b>, <b>snipers</b>, <b>heavy</b>, <b>shotguns</b>. If primary_weapon or secondary_wepon is set leave blank or if allow_select_weapons is false leave also blank!
9. `allow_knife_damage` - Will knife damage be enabled? <b>true</b> or <b>false</b>
10. `allow_center_message` - Allow center message? <b>true</b> or <b>false</b>
11. `center_message_text` - What message will be displayed in the center message during the mode if allow_center_message is true? [Preview](https://google.cz)
12. `blocked_weapons` - Which weapons from <b>blocked_weapons.json</b> will be disabled in this mode. Leave blank for enable all weapons or if primary_weapon/secondary_weapon is set leave also blank

- <b>Some examples:</b> [Only Pistols but deagle is disabled](https://github.com/NockyCZ/) , [Only AK47 & Headshot](https://github.com/NockyCZ/) , [Only AWP](https://github.com/NockyCZ/) , [Only Rifles but AK,M4,M1,AUG,SG553 is disabled](https://github.com/NockyCZ/) , [Only Deagle](https://github.com/NockyCZ/) , [Only Shotguns](https://github.com/NockyCZ/)
<h1></h1>

### Blocked Weapons List
```/game/csgo/addons/counterstrikesharp/plugins/Deathmatch/blocked_weapons.json```
- Create a list of blocked weapons for specific modes
```
{
  "blocked_weapons": {
    "LIST NAME": [
      "WEAPON NAME",
      "WEAPON NAME",
      "weapon_ak47",
      "weapon_deagle"
    ]
}
```
- <b>LIST NAME</b> is the name of the list that will be written in `custom_modes.json` as the value in `"blocked_weapons"`.
