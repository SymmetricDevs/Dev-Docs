# Main Modpack Structure

In this guide, we use the term "main modpack" to refer to the repository SymmetricDevs/Supersymmetry for disambiguation.

## Setting up SymmetricDevs/Supersymmetry

Most basic code-oriented text editors work fine for the main modpack, but [Visual Studio Code](https://code.visualstudio.com/) works well enough. Once you've installed it, pick "Clone Git Repository" on the start screen, click "Clone from GitHub" in the small popup, and type in SymmetricDevs/Supersymmetry.

The Supersymmetry repository uses several Python scripts for making ZIPped instances and formatting quests. You may download Python [here](https://www.python.org/downloads/).

## Testing Supersymmetry on PrismLauncher

You can test in-development versions of Supersymmetry by downloading an instance of Supersymmetry on PrismLauncher and then making one of the following modifications to the instance's folder:

- Replacing the `groovy`, `resources`, `structures`, and `config/betterquesting` folders manually from your main modpack repository
- Create **virtual folder links** to those repository folders. On Linux, the command to make such a "symlink" is: `ln -s "REPOSITORY ORIGINAL FOLDER LOCATION" "INSTANCE SYMLINK LOCATION"`

If you're working with a branch requiring mod versions not found in any particular release of Supersymmetry yet (e.g. you're trying to update mods), you can change those mod versions manually, or you can rebuild the main modpack through packwiz (as described below), import it into PrismLauncher, and just copy its mods folder into your favorite test instance.

You may also have to replace Susy-Core with your own compiled jar in certain cases if you want to test changes in it.

## Where is everything?

### Making instance ZIPs
  
The modpack development cycle primarily works around building the modpack through a program called [packwiz](https://packwiz.infra.link/). Packwiz creates the ZIP files that can be imported into modpack launchers like PrismLauncher or ATLauncher. The Supersymmetry repository wraps packwiz using Python, which you'll need if you want to use packwiz most efficiently. You may download Python [here](https://www.python.org/downloads/).

Once you've downloaded Python, you may now build the pack. Open any command terminal to the directory in which the Supersymmetry repository is copied, and then run the following command:

Windows:
```python3 build\main.py -c```

Linux:
```python3 build/main.py -c```

(You may need to modify the above command based on what your Python command is named. Common names include `python`, `python3`, and various `python3.x`.)

Once you've performed this command, look in the `buildOut` folder to see your `client.zip`! You may now import this into the modpack launcher of your choice. If you want a server instance, remove the `-c` argument in the command.

### Changing mods

The mod version info itself is managed by packwiz itself in the /mods/ folder, where you'll see a lot of .toml files. You probably won't have to change them directly, except rarely to change the "side" field to "client" or "server" for client-only or server-only mods.

To work with it, use the packwiz file through the command line. It has a decent help menu, but the most important command is `packwiz cf add [CURSEFORGE URL OR MOD SLUG]`, which allows you to add or update a mod directly. The mod slug is just the name in a CurseForge URL, like "[ae2-extended-life](https://www.curseforge.com/minecraft/mc-mods/ae2-extended-life)", and using it automatically selects the latest version that works.

```admonish warning "Do not commit changes to index.toml!"
When you change mod versions through packwiz, it will also update index.toml, which contains a list of hashes for every single mod file. This updates every time mods are changed, and can easily cause merge conflicts if you commit its changes too. As the file merely only needs to exist, it is left empty. We will not accept a PR with changes to index.toml.
```

### Questing

The questline files are all contained within /config/betterquesting, including the questline text (the English text is in /config/betterquesting/resources/supersymmetry/lang/en_us.lang). More information can be found in the [dedicated quest-writing guide](../guides/writing-quests.html).

```admonish warning "Format your quests!"
When you save quests in-game, BQu does not automatically translate your quest text, and it also adds a large amount of unneeded information to your files. We use the python script /build/questbook.py to format the files and fix them. When you copy your changes to your repository folder for committing, make sure you run this file with ```python3 build/questbook.py``` or so. If you try to commit unformatted files, you will see a bunch of changes (hundreds) in the commit staging area, so make sure to not commit those. Again, we will not accept PRs that unformat BQu files.
```

### Items/Recipes

For scripting in the main modpack, we use the mod [GroovyScript](https://cleanroommc.com/groovy-script/). It's like CraftTweaker if you've used that before. It uses the Groovy language for its scripts, but it's nearly identical to Java, so if you know Java, it's very easy to pick up.

What makes GroovyScript (GrS) so good is that you can reload certain scripts within the game itself with the command /gs reload! This only works for the scripts in /groovy/prePostInit and /groovy/postInit, as everything else is baked into the game too early to reload, but those two folders do contain almost every recipe in SUSY.

Most items and fluids are defined in /groovy/material through **materials** that generate many different items at once: e.g. the bronze material helps register bronze dust, bronze screws, liquid bronze, etc. Items that cannot be defined through materials are instead registered in /preInit/RegisterMetaItems.groovy, where each is given a static ID.

In order to give your materials and custom items actual names, you'll need to translate them in /resources/langfiles/lang. Other helpful locations include /groovy/globals, which contains some helper classes (such as carbon sources), while /preInit/ChangeFlags.groovy allows one to modify GTCEu-defined materials.

More information on how to make recipes is contained in the [recipe guide](../guides/writing-recipes.md).
