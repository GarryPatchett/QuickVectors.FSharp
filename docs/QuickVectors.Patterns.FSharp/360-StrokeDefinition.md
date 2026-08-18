# QuickVectors.Patterns.FSharp

# Stroke Definition

This type lets you define what the possible strokes will be.

- The [Stroke Definition Type](#the-stroke-definition-type)
    - [Fields](#fields)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
    - [Conversion](#conversion)
    - [Generation](#generation)
    - [Ready-made Stroke Definitions](#ready-made-stroke-definitions)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Stroke Definition Type

The `StrokeDefinition` **type** defines a record which is used to specify which strokes are generated.

### Fields 

The fields of the stroke definition are as follows:

| Field Name                | Type                      | Description                                                                                   |
| ------------------------- | ------------------------- | --------------------------------------------------------------------------------------------- |
| **ColourScheme**          | [ColourScheme](../QuickVectors.Core.FSharp/060-ColourScheme.md "The ColourScheme type and module")              | The colour scheme to be used to generate the colours                                          |
| **Width**                 | [StrokeWidthDefinition](340-StrokeWidthDefinition.md "The StrokeWidthDefinition type and module")     | The width definition used to generate the stroke widths                                       |
| **Reordering**            | [ColourReordering](020-ReorderingAndModification.md "The ColourReordering type and module") **1*     | The sequence reordering which can modify the stroke colour sequence generated via the profile |
| **Modification**          | [ColourModification](020-ReorderingAndModification.md "The ColourModification type and module") **1*   | The colour modification which can take place whether reordering happened or not               |
| **Noise**                 | [Noise](050-Noise.md "The Noise type and module") **1*                | The type of noise which can be applied to the stroke colours                                  |

- **1* : An Option field.

Below is an example stroke definition where all the values have been chosen manually:

```fsharp 
let custom = 
    {   StrokeDefinition.ColourScheme = ColourScheme.RandomColourFull 
        Width = StrokeWidthDefinition.fromFloats 1.0 6.0 
        Reordering = Some ColourReordering.SortedByAscendingLuminosity
        Modification = None 
        Noise = None }
    // -> { ColourScheme = RandomColourFull
    //      Width = { Range = StrokeWidthRange(1,6)
    //                Profile = Random
    //                Reordering = None
    //                Modification = None }
    //      Reordering = Some SortedByAscendingLuminosity
    //      Modification = None
    //      Noise = None }
```

### Construction

There are no construction functions, as such, but there are some convenience functions which allow you to
create some basic definitions without having to specify the values for lots of fields.

These convenience functions are:

- `fromColourScheme` : Create a stroke definition with the specified colour scheme;
- `fromFillDefinition` : Create a stroke definition from a [fill definition](350-FillDefinition.md "The FillDefinition type and module").

When using `fromColourScheme`, all fields other than those mentioned are given default values as defined in the respective modules.

When using `fromFillDefinition`, all fields will be given the values in the fill definition except `Width` which
will be given the value as defined by `StrokeWidthDefinition.one`.

> **Note:** Colour reordering, if any, will always occur before colour modification, if any, and the noise, if any, will be applied at the end.

### Deconstruction

There are no deconstruction functions for the type itself but you can deconstruct each field with the
deconstruction function appropriate for the type of that field.

### Variations 

Since all field values are type-checked and valid you can change the values in the same way as you would with any F# record.  
For example: `let newRecord = { oldRecord with FieldName = newValue }`.

If you want something fairly simple, you can use one of the convenience functions (as mentioned above),
or a ready-made value (mentioned below), to start a definition and then change whichever fields you need to, for example:

```fsharp 
let randomGreys = 
    StrokeDefinition.randomGreyscale 
    // -> { ColourScheme = RandomGreyscaleFull
    //      Width = { Range = StrokeWidthOnly(1)
    //                Profile = Random
    //                Reordering = None
    //                Modification = None }
    //      Reordering = None
    //      Modification = None
    //      Noise = None }
    
let modified = 
    { randomGreys with 
        Width = StrokeWidthDefinition.fromFloats 2.0 6.0 
        Reordering = Some ColourReordering.SortedByAscendingLuminosity 
        Noise = Some Noise.Less }
    // -> { ColourScheme = RandomGreyscaleFull
    //      Width = { Range = StrokeWidthRange(2,6)
    //                Profile = Random
    //                Reordering = None
    //                Modification = None }
    //      Reordering = Some SortedByAscendingLuminosity
    //      Modification = None
    //      Noise = Some Less }
```

Alternatively you can use a convenience function to change one field:

- `withReordering` : Returns a copy of the definition with the specified colour reordering;
- `withoutReordering` : Returns a copy of the definition without any colour reordering;
- `withModification` : Returns a copy of the definition with the specified colour modification;
- `withoutModification` : Returns a copy of the definition without any colour modification;
- `withNoise` : Returns a copy of the definition with the specified noise;
- `withoutNoise` : Returns a copy of the definition without any noise.

### Conversion

You can create a [fill definition](350-FillDefinition.md "The FillDefinition type and module") from a stroke definition via the `toFillDefinition` functon.

When using `toFillDefinition`, all fields in the new fill definition will be given the values in the stroke
definition except `Width` which will be lost.

### Generation 

While you wouldn't normally need to generate the colour sequence from a stroke definition
manually - it's better to do that via a pattern - you can do so via the `generateColourSequence` function
if you wish, like this:

```fsharp 
let colourRng = System.Random 45691 // Randomly-chosen seed.
let noiseRng = System.Random 9723 // Randomly-chosen seed.

// Using the custom stroke definition from the earlier example.

let colours = 
    custom
    |> StrokeDefinition.generateColourSequence colourRng noiseRng 10 
    // -> e.g. seq { Some Rgb(255,165,120); Some Rgb(255,19,219);
    //               Some Rgb(21,235,187); Some Rgb(255,102,63); 
    //               Some Rgb(163,34,20); Some Rgb(16,137,111);
    //               Some Rgb(182,65,247); Some Rgb(83,203,202); 
    //               Some Rgb(180,58,123); Some Rgb(20,224,166) } 
```

Similarly you can, but would normally not need to, manually generate the stroke widths via the
`generateStrokeWidthSequence` function, like this.

```fsharp 
let widthsRng = System.Random 781 // Randomly-chosen seed.

// Using the custom stroke definition from the earlier example.

let widths = 
    custom
    |> StrokeDefinition.generateStrokeWidthSequence widthsRng 10 
    // -> seq { 4.702068258; 5.886328487; 4.388216262; 2.285449893; 
    //          5.081979554; 1.365359069; 5.191539413; 2.288482359; 
    //          4.001463883; 2.341558581 }
```

> **Note:** The random number generators are required even if the chosen definition has no randomness.

## Ready-made Stroke Definitions

The ready-made stroke definitions available are:

- `black` : All of the shapes will have a black stroke;
- `white` : All of the shapes will have a white stroke;
- `alternatingBlackAndWhite` : The shapes will alternate between a black stroke and a while stroke;
- `greyscaleLinear` : The shapes will start with a black stroke and get progressively lighter, finishing with a white stroke;
- `randomGreyscale` : The shapes will have stroke colours which are chosen randomly from all of the possible greys;
- `randomFullColour` : The shapes will have stroke colours which are chosen randomly from all of the possible colours;
- `randomRainbow` : The shapes will have stroke colours which are chosen randomly from the colours of a rainbow.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.