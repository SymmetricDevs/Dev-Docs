## Using Susy-Core

Most of the useful programming in the Supersymmetry mod is located in `src/main/java/supersymmetry`. We'll go over the most important folders there first, before covering the rest of the project structure.

### The common folder

The common folder covers systems that both the Minecraft client and the Minecraft server need to use. If you're unfamiliar with these concepts, you can reference [this link](https://jamieswhiteshirt.github.io/resources/the-client-server-architecture/1-side-concepts/). Anyway, the common folder contains things such as advancements, blocks, entities, items, tile entities, meta-tile entities, UI widgets, etc.

#### Items (the items folder)

Items in many mods for Minecraft versions 1.12.2 and earlier have to contend with the item limit: the base game has a limited number of numerical IDs (4096) it can give to items. Susy-Core addresses this problem by indexing so-called "metaitems" with one item ID and many damage values. Minecraft 1.12.2 allows for up to 32,768 different values for durability, and it allows for each one to receive a different texture. This is why `common/item/SusyMetaItems.java` is where many items are stored. Within this file, each metaitem is declared as a `MetaValueItem` and is initialized in the method `initMetaItem`. The IDs given to each item in this method are unique and must not be changed. Otherwise, metaitems that players possess could mutate into another type of item when they update their Supersymmetry instance.

#### Tile Entities (the tileentities folder)

Tile entities are not physical entities, despite the name. Instead, they represent systems that are attached to a block. For example, in vanilla Minecraft, signs, furnaces, crafting tables, and beds have tile entities attached to them (that is, they implement `ITileEntityProvider`). As such, their job is to handle rendering and client-server communication. For example, when a GregTech-based tile entity is initialized as it is placed, the client calls `writeInitialSyncData` to initialize the tile entity on the server, and the server calls `readInitialSyncData` to process the information they received from the client. Another common pair of methods that must be implemented for tile entities is `writeNBT` and `readNBT`, for when the server saves and loads the tile entity from the world data. Tile entities are registered in `common/tileentities/SusyTileEntities.java` in the `register` method.

#### MTEs (the metatileentities folder)

MTEs are managed by GTCEU to implement common features that are useful to many GregTech machines. They are implemented similarly to GregTech-based tile entities, but they inherit from MetaTileEntity. They are registered in `common/metatileentities/SuSyMetaTileEntities.java` with a unique ID. MetaTileEntities can be given specialized UIs, and they can even represent special multiblocks!