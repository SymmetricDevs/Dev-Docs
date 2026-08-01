```admonish warning "TODO"
This section is currently unfinished! Help contribute more information.
```

# Writing Recipes

Most recipes in SUSY are written using GroovyScript, a scripting mod like CraftTweaker that works off of the Groovy language. It's very similar to Java, with just a few extra nice syntax changes. Here's an example recipe:

~~~
MIXER.recipeBuilder()
        .fluidInputs(fluid('fermented_biomass') * 1000)
        .inputs(ore('nutrientPhosphorous'))
        .outputs(metaitem('fertilizer') * 5)
        .EUt(30)
        .duration(100)
        .buildAndRegister()
~~~

Clearly, this is a mixer recipe for making fertilizer, but let's break down what it does more precisely and how you would be able to make this yourself.

MIXER stands for the mixer **recipe map**: a group of recipes that specific machines can run broadly. Of course, like in Java, it's not defined from nowhere; it's actually an import:

~~~
import static prePostInit.Recipemaps.*
~~~

As every GroovyScript file is defined in `/groovy/`, one can just take a quick peek at `/groovy/prePostInit/Recipemaps.groovy` to see where it's defined (press Ctrl-P to navigate to a file quickly in VS Code):

~~~
MIXER = recipemap('mixer')
~~~

The "mixer" string is just an identifier defined by GregTechCEu itself. The `recipemap` function should strike you as being odd, however. If you look around, it's not defined in the file or imported! So where did it come from?

GroovyScript actually allows mod authors to provide special functions to give priority access to their code, such as [this code](https://github.com/GregTechCEu/GregTech/blob/52c04cd7bf03e5749a653580c12ef5856cc12e31/src/main/java/gregtech/integration/groovy/GroovyScriptModule.java#L265-L268) in GTCEu defining `recipemap` to just call a function getting a recipe map. Several more such "Groovy extensions" are also used throughout the rest of the above example!

Well, anyway, now that we have our recipe map, we need to produce a recipe builder from it. The term "builder" refers to the [builder pattern](https://en.wikipedia.org/wiki/Builder_pattern#Java), the fact that we call multiple functions to help initialize a recipe (rather than use an unwieldy constructor). To get our builder, we call `recipeBuilder` on the recipe map.

The next line adds a fluid input to the recipe with the `fluidInputs` method. The `fermented_biomass` string passed into `fluid` is the name of that fluid itself. To find the correct fluid name, one can use the `/gs hand` command in-game as such:
<img width="457" height="263" alt="image" src="https://github.com/user-attachments/assets/75c4d0b3-eb90-409d-8cce-0035a0bc4cae" />
<img width="870" height="331" alt="image" src="https://github.com/user-attachments/assets/c1566c65-fffc-4339-957e-7c3e70f47079" />

Here's a quick reference to the various methods on a recipe builder:
~~~
.fluidInputs(
~~~

Conveniently, the voltage requirement of the recipe is determined by the ```EUt``` method.

# Materials

Items that exist as a variant of a material are specified by the ```ore``` function with a string argument consisting of an _ore prefix_ and a material, such as ```nutrientPhosphorous```, ```foilPlastic```, ```dustSilver```, etc.

Material definitions and initializations can be found in groovy/material, and importantly, most of them contain sub-materials. SuSyMaterials.groovy defines all materials defined by the modpack and calls their initialization functions. Within FirstDegreeMaterials.groovy, the high-purity elements and materials that depend only on elements are initialized. SecondDegreeMaterials.groovy contains materials that depend on materials within FirstDegreeMaterials.groovy, and so on to avoid nasty errors. Materials of unknown or complex composition are initialized in UnknownCompositionMaterials.groovy. Sometimes, one needs to initialize materials in Susy-Core.

# Metaitems

Metaitems can be thought of as individual item variants with unlocalized names and numerical IDs, meaning that one does have to be careful when merging. They are set up in SusyMetaItems.java, along with their tooltips and stack size.
