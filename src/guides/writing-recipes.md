```admonish warning "TODO"
This section is currently unfinished! Help contribute more information.
```

# Writing Recipes

Recipes are written in GroovyScript. Here's an example:

~~~
MIXER.recipeBuilder()
        .fluidInputs(fluid('fermented_biomass') * 1000)
        .inputs(ore('nutrientPhosphorous'))
        .outputs(metaitem('fertilizer') * 5)
        .EUt(30)
        .duration(100)
        .buildAndRegister()
~~~

MIXER is a RecipeMap that is generated as such:
~~~
MIXER = recipemap('mixer')
~~~

To create a recipe, one has to call the ```recipeBuilder``` method first, which allows developers to add the properties of the recipe. The recipe is registered with the ```buildAndRegister``` recipe.

Conveniently, the voltage requirement of the recipe is determined by the ```EUt``` method.

# Materials

Items that exist as a variant of a material are specified by the ```ore``` function with a string argument consisting of an _ore prefix_ and a material, such as ```nutrientPhosphorous```, ```foilPlastic```, ```dustSilver```, etc.

Material definitions and initializations can be found in groovy/material, and importantly, most of them contain sub-materials. SuSyMaterials.groovy defines all materials defined by the modpack and calls their initialization functions. Within FirstDegreeMaterials.groovy, the high-purity elements and materials that depend only on elements are initialized. SecondDegreeMaterials.groovy contains materials that depend on materials within FirstDegreeMaterials.groovy, and so on to avoid nasty errors. Materials of unknown or complex composition are initialized in UnknownCompositionMaterials.groovy. Sometimes, one needs to initialize materials in Susy-Core.

# Metaitems

Metaitems can be thought of as individual item variants with unlocalized names and numerical IDs, meaning that one does have to be careful when merging. They are set up in SusyMetaItems.java, along with their tooltips and stack size.