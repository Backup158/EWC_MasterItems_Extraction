# Extended Weapon Customization - Getting a List of Possible Attachment Points
For developing plugins for the Darktide mod Extended Weapon Customization.

These are the values an addon plugin can put into the `attach_nodes` entry when creating kitbashes

## I don't even know how much of this is true
The game stores information about the game content (weapon attachments, cosmetics, etc.) in the MasterItems table. `MasterItems.json` is ripped from there, though I don't know how comprehensive it is nor when it was ripped, so there may be new attachment points we don't know about.

`MasterItems_split.json` is a copy that has the `'MasterItems: { <all_the_content> }` part removed, so pandas automatically puts the content address as the dataframe column names. Basically it's easier to manipulate this way, and I was too lazy to find a way programmatically to do that with the original file.

## What This Script Does
1. Imports the MasterItems data
2. Filters out all the entries that are not `content/items/weapons/player/melee/...` or `content/items/weapons/player/ranged/...`
    - Checking by the column name
    - These are the starts of the addresses for weapon attachments (muzzles, barrels, etc.)
    - This ignores attachments from skins and body cosmetics (`skins/...`, `human/...`, `ogryn/...`)
3. Gets the value of the `attach_node` entry for each column (without the addresses)
4. Filters those by unique values
5. Writes each value into `weapon_attachments_list_of_attach_nodes.txt`