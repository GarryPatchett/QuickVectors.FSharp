# QuickVectors.Patterns.FSharp

# Scatter Area Definition

This type lets you define where and how the shapes will be scattered.

- The [Scatter Area Definition Type](#the-scatter-area-definition-type)
    - [Fields](#fields)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
    - [Generation](#generation)
    - [Ready-made Scatter Area Definitions](#ready-made-scatter-area-definitions)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Scatter Area Definition Type

The `ScatterAreaDefinition` **type** defines a record which is used to specify where and how the shapes will be scattered.

### Fields 

The fields of the scatter area definition are as follows:

| Field Name                | Type                      | Description                                                               |
| ------------------------- | ------------------------- | ------------------------------------------------------------------------- |
| **AreaShape**             | [ScatterAreaShape](070-ScatterAreaShape.md "The ScatterAreaShape type and module")          | The shape of the scatter area                                             |
| **HorizontalProfile**     | [Profile](../QuickVectors.Core.FSharp/080-Profile.md "The Profile type and module")                   | Defines the profile used to scatter the shapes horizontally               |
| **VerticalProfile**       | [Profile](../QuickVectors.Core.FSharp/080-Profile.md "The Profile type and module")                   | Defines the profile used to scatter the shapes vertically                 |
| **HoleSize**              | [ScatterHoleSize](080-ScatterHoleSize.md "The ScatterHoleSize type and module")           | The size of the hole                                                      |

Below is an example scatter area definition where all the values have been chosen manually:

```fsharp 
let custom = 
    {   ScatterAreaDefinition.AreaShape = ScatterAreaShape.Rectangular 
        HorizontalProfile = Profile.Random 
        VerticalProfile = Profile.Linear 
        HoleSize = ScatterHoleSize.fromFloat ScatterHoleSize.minimum }
        // -> { AreaShape = Rectangular
        //      HorizontalProfile = Random
        //      VerticalProfile = Linear
        //      HoleSize = HoleSize(10.0)% }
```

### Construction

There are no construction functions, as such, but there are some convenience functions which allow you to
create some basic definitions without having to specify the values for lots of fields.

These convenience functions are:

- `fromAreaShape`
    : Create a scatter area definition with the specified scatter area shape.

When using a convenience function, all fields other than those mentioned are given default values as defined in the respective modules.

> **Notes:**
>
> 1. The hole size is currently only applicable with the EllipticalRing scatter area shape.
>
> 2. The profiles are used in slightly different ways for rectangular and elliptical scattering.

### Deconstruction

There are no deconstruction functions for the type itself but you can deconstruct each field with the
deconstruction function appropriate for the type of that field.

### Variations 

There are no functions for varying the values of the fields but you can, since all field values are type-checked and valid,
change the values in the same way as you would with any F# record.  
For example: `let newRecord = { oldRecord with FieldName = newValue }`.

If you want something fairly simple, you can use one of the convenience functions (as mentioned above),
or a ready-made value (mentioned below), to start a definition and then change whichever fields you need to, for example:

```fsharp 
let rectangular = 
    ScatterAreaDefinition.rectangularRandom 
    // -> { AreaShape = Rectangular
    //      HorizontalProfile = Random
    //      VerticalProfile = Random
    //      HoleSize = HoleSize(10.0)% }

let modified = 
    { rectangular with 
        HorizontalProfile = Profile.SineWave 
        HoleSize = ScatterHoleSize.fromFloat 75.0 }
    // -> { AreaShape = Rectangular
    //      HorizontalProfile = SineWave
    //      VerticalProfile = Random
    //      HoleSize = HoleSize(75.0)% }
    
```

## Ready-made Scatter Area Definitions

The ready-made scatter area definitions available are:

- `rectangularRandom` : A rectangular area with the minimum (unused) hole size and random profiles;
- `ellipticalRandom` : An elliptical area with the minimum (unused) hole size and random profiles;
- `ellipticalPictureBorder` : An elliptical area with a hole size of 60% and linear profiles.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.