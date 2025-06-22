```admonish warning "TODO"
This section is currently unfinished! Help contribute more information.
```

Block textures in Supersymmetry come from their assigned mods, but Gregtech-based mods have a strange quirk. MetaItems, generic block form types, item material sets defined in Supersymmetry have to have their textures/"models" defined in the ```gregtech``` folder within resources/assets, while other items and blocks defined by a particular mod have to have their textures/"models" in that mod's folder. This is because GTCEU provides registering services for certain items and blocks.

Some reminders for blocks:
- Each textured block has an entry in blockstates, where block variants are defined.
- Blocks have models in models/block, where textures with resource location somemod:somepath exist in somemod/textures/somepath.json.
- When importing from Blockbench, be sure to rename all mod prefixes to their correct values!