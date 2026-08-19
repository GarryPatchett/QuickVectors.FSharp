# QuickVectors.Export.Svg.FSharp

# Samples

It can be difficult to remember what each profile, grid route, standard palette etc. looks like.
Because of this various sample designs are available.

- The [Sample Module](#the-sample-module)
    - [Grid Routes](#grid-routes-sample)
    - [Palettes](#palettes-sample)
    - [Profiles](#profiles-sample)
    - [Shapes](#shapes-sample)
    - [Tessellators](#tessellators-sample) 
- [Viewing The Sample](#viewing-the-sample)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Sample Module

The `Sample` **module** contains functions to create the sample designs, which are (in alphabetical order):

| Sample.RollCall.      | Provides a sample of              | Associated Type                                                                                       |
| --------------------- | --------------------------------- | ----------------------------------------------------------------------------------------------------- |
| **gridRoutes**        | Every grid route                  | [GridRoute](../QuickVectors.Core.FSharp/090-GridRoute.md "The GridRoute type and module")             |
| **palettes**          | Most of the standard palettes     | [StandardPalette](../QuickVectors.Core.FSharp/050-Palette.md "The StandardPalette type and module")   |
| **profiles**          | Every profile                     | [Profile](../QuickVectors.Core.FSharp/080-Profile.md "The Profile type and module")                   |
| **shapes**            | Every shape                       | [Shape](../QuickVectors.Core.FSharp/020-Shape.md "The Shape type and module")                         |
| **tessellators**      | Every tessellator                 | [Tessellator](../QuickVectors.Core.FSharp/110-Tessellator.md "The Tessellator type and module")       |

> **Notes:** 
>
> 1. The module is actually contained in the `QuickVectors.Elements.FSharp` package but it is documented here for convenience.
>
> 2. The form and/or content of each sample is liable to change between package versions so you should not rely on getting the same output after upgrading.

### Grid Routes Sample

When generating the grid routes sample you need to supply one parameter:

- `random` : A random number generator (from System.Random).

An example of specifying the sample is:

```fsharp 
Sample.RollCall.gridRoutes System.Random.Shared 
```

You can also see visual examples of the grid routes [here](../QuickVectors.Core.FSharp/images/GridRoute-Examples.png "Visual roll call of the available grid routes").

### Palettes Sample

The palettes sample has no parameters.

```fsharp 
Sample.RollCall.palettes() 
```

> **Note:** The palettes in the `FiveShades` and `SevenShades` groups are not included in the sample.

You can also see visual examples of (some of) the standard palettes [here](../QuickVectors.Core.FSharp/images/StandardPalette-Examples.png "Visual roll call of the available standard palettes").

### Profiles Sample

When generating the profiles sample you need to supply one parameter:

- `random` : A random number generator (from System.Random).

An example of specifying the sample is:

```fsharp 
Sample.RollCall.profiles System.Random.Shared 
```

You can also see visual examples of the profiles [here](../QuickVectors.Core.FSharp/images/Profile-Examples.png "Visual roll call of the available profiles").

### Shapes Sample

When generating the shapes sample you need to always supply four parameters:

- `random` : A random number generator (from System.Random);
- `geometryModifier` : The geometry modifier to use when creating the shapes (only used where applicable);
- `rotation` : The rotation of every shape;
- `numberOfVertices` : The number of vertices (only used where applicable).

The last three parameters are clamped to their respective ranges so that you can only generate a sample containing
shapes which are possible via normal usage.

An example of specifying the sample is:

```fsharp 
Sample.RollCall.shapes System.Random.Shared 40.0 0.0 7
```

...where 40.0 is the geometry modifier percentage, 0.0 is the rotation, and 7 is the number of vertices.

You can also see visual examples of the shapes [here](../QuickVectors.Core.FSharp/images/Shape-Examples.png "Visual roll call of the available shapes").

### Tessellators Sample

The tessellators sample has no parameters.

```fsharp 
Sample.RollCall.tessellators() 
```

You can also see visual examples of the tessellators [here](../QuickVectors.Core.FSharp/images/Tessellator-Examples.png "Visual roll call of the available tessellators").

## Viewing The Sample

To create one of the samples as an SVG you can use code such as:

```fsharp 
Sample.RollCall.palettes() // Create the palettes sample.
|> Svg.export SvgExportSettings.standard // Use the standard settings.
|> fun svg -> File.WriteAllText(@"PalettesRollCall.svg", svg) 
```

> **Note:** No generation step is required when creating a sample as would normally be necessary, via
for example `Scatter.generate`, as the sample is automatically generated.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.