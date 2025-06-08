```admonish warning "TODO"
This section is currently unfinished! Help contribute more information.
```

# Creating Multiblocks

A multiblock is implemented as a MetaTileEntity (GregTech's buffed tile entities). Therefore, all multiblocks have a controller block.
However, we do not suggest that you use a MetaTileEntity superclass for most multiblocks. Usually, a RecipeMapMultiblockController or a MultiblockWithDisplayBase is what you want as the superclass.

When using a RecipeMapMultiblockController, you must create a field of SusyRecipeMaps and initialize it with a name to begin registering recipes in GroovyScript. The initialization is used to set up the GUI and the associated sounds. This is convenient, because appropriate recipe logic can be set up immediately based on the type argument.

For a MultiblockWithDisplayBase, the recipe system and GUI are customizable to a greater extent, but you will have to create them yourself.

Here is an example implementation of createStructurePattern for a launch pad.

![A method called createStructurePattern is shown. It returns FactoryBlockPattern.start(), followed by aisles that indicate rows of blocks, stacked vertically, facing the controller. Letters in the rows represent blocks, with the translations provided by .where() clauses and predicates such as any(), air(), selfPredicate(), and states(). The pattern formed by the letters resembles two wheels, with the right one being slightly smaller due to it representing the top portion of the launch pad. This long sequence of method calls is ended with .build().](structure_formatting.png "Multiblock Structure Format Code")

## Multiblock Parts