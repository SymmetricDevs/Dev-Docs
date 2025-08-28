# Getting Started
To set up a repository, we recommend installing [IntelliJ IDEA Community Edition](https://www.jetbrains.com/idea/) and the Java 8 JDK (which IntelliJ can help you install).
Once you do this, you can create a new IDEA project by cloning one of our repositories. In fact, there is an option for this on the IDEA launch page.

## Which repository do I clone?
If you want to tweak the configurations of mods or recipes, you'll want to use our main repository, [SymmetricDevs/Supersymmetry](https://github.com/SymmetricDevs/Supersymmetry/). If you instead want to work with creating new multiblocks or other more complex features, you'll want to work on the core mod, which is found at [SymmetricDevs/Susy-Core](https://github.com/SymmetricDevs/Susy-Core). You can learn more about the various repositories that Supersymmetry developers work on in [Supersymmetry Projects](./project-structure.md)

In order to actually clone it, you will want to select "Project from Version Control" in IDEA.

<img width="800" height="245" alt="image" src="https://github.com/user-attachments/assets/cdf359dd-9994-49a9-b637-0d0b1304ea03" />

You can then navigate to the repository you want to clone in your browser and copy this URL found under the "Code" button:

<img width="900" height="357" alt="image" src="https://github.com/user-attachments/assets/e538cf64-a6d3-4abc-aadd-618efd7ee4e2" />

Inserting that into the URL field in IDEA and then setting the main repository folder will start the process of downloading it onto your computer.

## Working with SymmetricDevs/Supersymmetry
The modpack development cycle primarily works around building the modpack through a program called [packwiz](https://packwiz.infra.link/). Packwiz creates the ZIP files that can be imported into modpack launchers like PrismLauncher or ATLauncher. The Supersymmetry repository wraps packwiz using Python, which you'll need if you want to use packwiz most efficiently. You may download Python [here](https://www.python.org/downloads/).

Once you've downloaded Python, you may now build the pack. Open any command terminal to the directory in which the Supersymmetry repository is copied, and then run the following command:

Windows:
```python3 build/main.py -c```

Linux:
```python3 build\main.py -c```

(You may need to modify the above command based on what your Python command is named. Common names include `python`, `python3`, and `python3.x`.)

Once you've performed this command, look in the `buildOut` folder to see your `client.zip`! You may now import this into the modpack launcher of your choice. If you want a server instance, remove the `-c` argument in the command.

## Working with SymmetricDevs/Susy-Core
Susy-Core also has a build system known as Gradle (as is used for the majority of Minecraft mods).

Once you've cloned and entered the repository in IntelliJ IDEA, look for a notification in the bottom right that tells you to "Load Gradle Project." Once you click it, it will configure a set of commands you can use to test Susy-Core in a minimal environment. You can look for some particularly common ones in the top-right corner:

<img width="319" height="526" alt="image" src="https://github.com/user-attachments/assets/ff2b296a-0e99-438b-a356-06766684daa8" />

Selecting any of these will override the selected top-line command "Setup Workspace," allowing you to work more efficiently. Below are some important Gradle "run configurations" for you to know.

### 2. Run Client
This particular command starts a client instance of Minecraft including Susy-Core and a few other mods required to load it (including GregTech and JEI). If you want to debug Susy-Core, you can click the green bug icon you see here:

<img width="307" height="50" alt="image" src="https://github.com/user-attachments/assets/51fcdeb2-b6a9-42f5-bb7b-eb057551b268" />

Careful tracing of the code in debugging mode, involving setting breakpoints, going step-by-step through each line, and looking for points before the glitch has necessarily occurred are essential for finding and fixing bugs.

### 6. Build Jars
This command builds a set of JAR files in the `build/libs` folder. After navigating there, you'll notice quite a few files:

<img width="579" height="171" alt="image" src="https://github.com/user-attachments/assets/0c9da9a3-179e-4da8-a613-5dfb5bbf1a88" />

However, the only one that can be brought into your modpack's `mods` folder without issue is the one that does NOT have `dev` at the end of the name (the first one in the picture above). The others are deobfuscated files that only work with IntelliJ IDEA, and they will crash your game if you try to use them in a real modpack instance. (Also, I recommend clearing out this folder before running the command as to not get confused about which version to pick.)
