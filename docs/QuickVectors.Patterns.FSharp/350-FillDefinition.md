# QuickVectors.Patterns.FSharp

# Fill Definition

This type lets you define what the possible fill colours will be.

- The [Fill Definition Type](#the-fill-definition-type)
    - [Fields](#fields)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
    - [Conversion](#conversion)
    - [Generation](#generation)
    - [Ready-made Fill Definitions](#ready-made-fill-definitions)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Fill Definition Type

The `FillDefinition` **type** defines a record which is used to specify which fill colours are generated.

### Fields 

The fields of the fill definition are as follows:

| Field Name                | Type                      | Description                                                                                   |
| ------------------------- | ------------------------- | --------------------------------------------------------------------------------------------- |
| **ColourScheme**          | [ColourScheme](../QuickVectors.Core.FSharp/060-ColourScheme.md "The ColourScheme type and module")              | The colour scheme to be used to generate the colours                                          |
| **Reordering**            | [ColourReordering](020-ReorderingAndModification.md "The ColourReordering type and module") **1*     | The sequence reordering which can modify the fill colour sequence generated via the profile   |
| **Modification**          | [ColourModification](020-ReorderingAndModification.md "The ColourModification type and module") **1*   | The colour modification which can take place whether reordering happened or not               |
| **Noise**                 | [Noise](050-Noise.md "The Noise type and module") **1*                | The type of noise which can be applied to the fill colours                                    |

- **1* : An Option field.

Below is an example fill definition where all the values have been chosen manually:

```fsharp 
let custom = 
    {   FillDefinition.ColourScheme = ColourScheme.RandomColourFull
        Reordering = Some ColourReordering.SortedByAscendingLuminosity
        Modification = None 
        Noise = None } 
    // -> { ColourScheme = RandomColourFull
    //      Reordering = Some SortedByAscendingLuminosity
    //      Modification = None 
    //      Noise = None }
```

### Construction

There are no construction functions, as such, but there are some convenience functions which allow you to
create some basic definitions without having to specify the values for lots of fields.

These convenience functions are:

- `fromColourScheme` : Create a fill definition with the specified colour scheme.

When using a convenience function, all fields other than those mentioned are given default values as defined in the respective modules.

> **Note:** Colour reordering, if any, will always occur before colour modification, if any, and the noise, if any, will be applied at the end.

### Deconstruction

There are no deconstruction functions for the type itself but you can deconstruct each field with the
deconstruction function appropriate for the type of that field.

### Variations 

Since all field values are type-checked and valid you an change the values in the same way as you would with any F# record.  
For example: `let newRecord = { oldRecord with FieldName = newValue }`.

If you want something fairly simple, you can use one of the convenience functions (as mentioned above),
or a ready-made value (mentioned below), to start a definition and then change whichever fields you need to, for example:

```fsharp 
let bricks = 
    FillDefinition.fromColourScheme 
        (ColourScheme.CycledFromPalette StandardPalette.Architectural.brickReds) 
    // -> { ColourScheme =
    //        CycledFromPalette
    //         { NumberOfColours = 5
    //           Colours =
    //              [|Rgb(211,70,58); Rgb(200,74,46); Rgb(189,78,61); Rgb(162,79,77);
    //                Rgb(155,60,57)|]
    //           Weights = [|1; 1; 1; 1; 1|]
    //           ExpandedColourIndices = [|0; 1; 2; 3; 4|] }
    //      Reordering = None
    //      Modification = None 
    //      Noise = None }
    
let modified = 
    { bricks with 
        Reordering = Some ColourReordering.SortedByDescendingLuminosity 
        Noise = Some Noise.Least }
    // -> { ColourScheme =
    //       CycledFromPalette
    //          { NumberOfColours = 5
    //         Colours =
    //          [|Rgb(211,70,58); Rgb(200,74,46); Rgb(189,78,61); Rgb(162,79,77);
    //            Rgb(155,60,57)|]
    //         Weights = [|1; 1; 1; 1; 1|]
    //         ExpandedColourIndices = [|0; 1; 2; 3; 4|] }
    //      Reordering = Some SortedByDescendingLuminosity 
    //      Modification = None 
    //      Noise = Some Least }
```

> **Note:** Colour reordering does not affect the order of the colours in a palette which is specified, if any. 
Rather it only affects the order of the colours in the output sequence.

Alternatively you can use a convenience function to change one field:

- `withReordering` : Returns a copy of the definition with the specified colour reordering;
- `withoutReordering` : Returns a copy of the definition without any colour reordering;
- `withModification` : Returns a copy of the definition with the specified colour modification;
- `withoutModification` : Returns a copy of the definition without any colour modification;
- `withNoise` : Returns a copy of the definition with the specified noise;
- `withoutNoise` : Returns a copy of the definition without any noise.

### Conversion

The [StrokeDefinition](360-StrokeDefinition.md "The StrokeDefinition type and module") **module** provides functions for converting a fill definition to or from a stroke definition.

### Generation 

While you wouldn't normally need to generate the sequence from a fill definition
manually - it's better to do that via a pattern - you can do so via the `generateSequence` function
if you wish, like this:

```fsharp 
let colourRng = System.Random 4681 // Randomly-chosen seed.
let noiseRng = System.Random 58130 // Randomly-chosen seed.

// Using the custom fill definition from the earlier example.

let colours = 
    custom
    |> FillDefinition.generateSequence colourRng noiseRng 10 
    // -> e.g. seq { Some Rgb(0,0,69); Some Rgb(255,236,151);
    //               Some Rgb(60,204,18); Some Rgb(118,253,255); 
    //               Some Rgb(193,243,183); Some Rgb(60,98,9);
    //               Some Rgb(44,153,143); Some Rgb(65,23,78); 
    //               Some Rgb(136,85,143); Some Rgb(14,123,243) } 
```

> **Note:** The random number generators are required even if the chosen definition has no randomness.

## Ready-made Fill Definitions

The ready-made fill definitions available are:

- `noFill` : None of the shapes will have a fill;
- `black` : All of the shapes will have a black fill;
- `white` : All of the shapes will have a white fill;
- `alternatingBlackAndWhite` : The shapes will alternate between a black fill and a while fill;
- `greyscaleLinear` : The shapes will start with a black fill and get progressively lighter, finishing with a white fill;
- `randomGreyscale` : The shapes will have fills which are chosen randomly from all of the possible greys;
- `randomFullColour` : The shapes will have fills which are chosen randomly from all of the possible colours;
- `randomRainbow` : The shapes will have fills which are chosen randomly from the colours of a rainbow.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.