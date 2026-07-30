## IntelliJ IDEA for Susy-Core
To set up Susy-Core, we recommend installing [IntelliJ IDEA Community Edition](https://www.jetbrains.com/idea/) and the Java 8 JDK (which IntelliJ can help you install).
Once you do this, you can create a new IDEA project by cloning one of our repositories. In fact, there is an option to directly clone a repository and set up a project on the IDEA launch page.

In order to actually clone it, you will want to select "Project from Version Control" in IDEA.

<img width="800" height="245" alt="image" src="https://github.com/user-attachments/assets/cdf359dd-9994-49a9-b637-0d0b1304ea03" />

You can then navigate to the repository you want to clone in your browser and copy this URL found under the "Code" button:

<img width="900" height="357" alt="image" src="https://github.com/user-attachments/assets/e538cf64-a6d3-4abc-aadd-618efd7ee4e2" />

Inserting that into the URL field in IDEA and then setting the main repository folder will start the process of downloading it onto your computer.

## Working with SymmetricDevs/Susy-Core
Susy-Core also has a build system known as Gradle (as is used for the majority of Minecraft mods).

Once you've cloned and entered the repository in IntelliJ IDEA, look for a notification in the bottom right that tells you to "Load Gradle Project." Once you click it, it will configure a set of commands you can use to test Susy-Core in a minimal environment. You can look for some particularly common ones in the top-right corner:

<img width="319" height="526" alt="image" src="https://github.com/user-attachments/assets/ff2b296a-0e99-438b-a356-06766684daa8" />

Selecting any of these will override the selected top-line command "Setup Workspace," allowing you to work more efficiently. Below are some important Gradle "run configurations" for you to know.

It is also possible to interface with Gradle over the command line, either by using `./gradlew` to call commands or by using a system installation. We advise using a Gradle version of 8.9 with Java 21.0.2 at the current moment. To view all tasks from the command line, use `gradle tasks`.

### 2. Run Client
This particular command starts a client instance of Minecraft including Susy-Core and a few other mods required to load it (including GregTech and JEI). If you want to debug Susy-Core, you can click the green bug icon you see here:

<img width="307" height="50" alt="image" src="https://github.com/user-attachments/assets/51fcdeb2-b6a9-42f5-bb7b-eb057551b268" />

Careful tracing of the code in debugging mode, involving setting breakpoints, going step-by-step through each line, and looking for points before the glitch has necessarily occurred are essential for finding and fixing bugs.

### 6. Build Jars
This command builds a set of JAR files in the `build/libs` folder. After navigating there, you'll notice quite a few files:

<img width="579" height="171" alt="image" src="https://github.com/user-attachments/assets/0c9da9a3-179e-4da8-a613-5dfb5bbf1a88" />

However, the only one that can be brought into your modpack's `mods` folder without issue is the one that does NOT have `dev` at the end of the name (the first one in the picture above). The others are deobfuscated files that only work with IntelliJ IDEA, and they will crash your game if you try to use them in a real modpack instance. (Also, I recommend clearing out this folder before running the command as to not get confused about which version to pick.)

## Where is everything?

Most of the useful programming in the Supersymmetry mod is located in `src/main/java/supersymmetry`. We'll go over the most important folders there first, before covering the rest of the project structure.

### /common

The common folder covers systems that both the Minecraft client and the Minecraft server need to use. If you're unfamiliar with these concepts, you can reference [this link](https://jamieswhiteshirt.github.io/resources/the-client-server-architecture/1-side-concepts/). Anyway, the common folder contains things such as advancements, blocks, entities, items, tile entities, meta-tile entities, UI widgets, etc.

#### /common/items

Items in many mods for Minecraft versions 1.12.2 and earlier have to contend with the item limit: the base game has a limited number of numerical IDs (4,096) it can give to items. 

GregTechCEu addresses this problem by indexing special items called **metaitems** using the `itemDamage` field, packing many "items" into one item ID. Minecraft 1.12.2 allows for up to 32,768 different values for durability, and each one can be given its own texture, behavior, and so on, making it a very flexible system. Susy-Core leverages this system for its own purposes, creating several of its own metaitems. 

As such, most "items" in Susy-Core are declared and initialized in `common/item/SusyMetaItems.java`, and a very similar metaitem is declared in the GroovyScript files for the modpack repository (RegisterMetaitems.groovy). In SusyMetaItems.java, each metaitem is declared as a `MetaValueItem` and is initialized in the method `initMetaItem`. 

Note that the IDs given to each `MetaValueItem` are unique and must not be changed. As Minecraft only stores the `itemDamage` for each item, shifting MetaValueItem IDs around would cause items with one damage value to mutate into whatever happened to be given that same damage value in the next version. That is, you get massive amounts of item transmutation!

#### /common/metatileentities

Tile entities are not physical entities, despite the name. Instead, they represent systems that are attached and saved alongside a block. For example, in vanilla Minecraft, signs, furnaces, crafting tables, and beds have tile entities attached to them (that is, they implement ITileEntityProvider). As such, their job is to handle rendering, saves, and client-server communication. 

However, we rarely use tile entities directly: we instead use meta-tile entities.

**Meta-tile entities** from GTCEu implement common features that are useful to many GregTech machines, solving the same limited-ID problem for tile entities as metaitems do for items. They are implemented similarly to GregTech-based tile entities, but they inherit from MetaTileEntity. They are registered in `common/metatileentities/SuSyMetaTileEntities.java` with unique IDs. MetaTileEntities can be given specialized UIs, and they can even represent special multiblocks!
