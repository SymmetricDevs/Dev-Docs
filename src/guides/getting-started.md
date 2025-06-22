# Getting Started
To set up a repository, install [IntelliJ IDEA Community Edition](https://www.jetbrains.com/idea/) and the Java 8 JDK (which IntelliJ can help you install).
Once you do this, you can create a new IDEA project by cloning one of our repositories. In fact, there is an option for this on the IDEA launch page.
Currently, the modpack can only be launched from a development environment by running ```python3 build/build.py``` from the main directory. We use packwiz to generate the output.
As for the repositories for specific mods, you must run the Gradle task setupDecompWorkspace in order to compile the mods, test them, and integrate with the language server.