# Getting Started
## What do I work on?
As an aspiring SUSY developer, there are a few channels of information you can look at to see what to work on:

- On the [official Discord server](https://discord.gg/KYF5a4scRj), the #workorders channel has plenty of small tasks for you to choose from of varying difficulty.
  - #bug-discussions and #bug-reports can also be useful for getting ideas, or just lurk in #susy-general.
- If you don't want to join the Discord (fair), you can also look at the [GitHub issues page](https://github.com/SymmetricDevs/Supersymmetry/issues) for Supersymmetry (or [Susy-Core](https://github.com/SymmetricDevs/Susy-Core/issues)). These issues may be rather difficult to fix, however.

Some easy starting tasks I would recommend are editing a quest, changing a recipe, or adding a new multiblock. Once you've selected a task, you'll need to clone a repository. You can learn more about the various repositories that we work on in [Supersymmetry Projects](./project-structure.md), but the basics are:

- If you want to tweak the configurations of mods or change/add basic items and recipes, you'll want to use our main repository, [SymmetricDevs/Supersymmetry](https://github.com/SymmetricDevs/Supersymmetry/). We'll comment more on how to set this repository up here.
- If you instead want to work with creating new multiblocks or other more complex features, you'll want to work on the core mod, which is found at [SymmetricDevs/Susy-Core](https://github.com/SymmetricDevs/Susy-Core). More information on this is contained in the [Susy-Core section](./susy-core-structure.md).

## Working with SymmetricDevs/Supersymmetry
Most basic code-oriented text editors work fine for the main repository, but [Visual Studio Code](https://code.visualstudio.com/) works well enough. Once you've installed it, pick "Clone Git Repository" on the start screen, click "Clone from GitHub" in the small popup, and type in SymmetricDevs/Supersymmetry.

The modpack development cycle primarily works around building the modpack through a program called [packwiz](https://packwiz.infra.link/). Packwiz creates the ZIP files that can be imported into modpack launchers like PrismLauncher or ATLauncher. The Supersymmetry repository wraps packwiz using Python, which you'll need if you want to use packwiz most efficiently. You may download Python [here](https://www.python.org/downloads/).

Once you've downloaded Python, you may now build the pack. Open any command terminal to the directory in which the Supersymmetry repository is copied, and then run the following command:

Windows:
```python3 build\main.py -c```

Linux:
```python3 build/main.py -c```

(You may need to modify the above command based on what your Python command is named. Common names include `python`, `python3`, and `python3.x`.)

Once you've performed this command, look in the `buildOut` folder to see your `client.zip`! You may now import this into the modpack launcher of your choice. If you want a server instance, remove the `-c` argument in the command.

## Running a test instance of Supersymmetry on PrismLauncher

One way to test in-development versions of Supersymmetry is to create an instance of Supersymmetry on PrismLauncher and then making the following modifications to the instance's `minecraft` folder:

- Replacing the `groovy`, `resources`, `structures` folders using the command (on Linux) `ln -s "ORIGINAL FOLDER LOCATION" "SYMLINK LOCATION"`
- In some cases, you may need to build a special version of Susy-Core and replace it in the mods folder.

