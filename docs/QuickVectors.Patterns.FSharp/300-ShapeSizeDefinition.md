# QuickVectors.Patterns.FSharp

# Shape Size Definition

This type lets you define what the possible shapes sizes will be in some patterns.

- The [Shape Size Definition Type](#the-shape-size-definition-type)
    - [Fields](#fields)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
    - [Generation](#generation)
    - [Ready-made Shape Size Definitions](#ready-made-shape-size-definitions)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Shape Size Definition Type

The `ShapeSizeDefinition` **type** defines a record which is used to specify which shape sizes are generated.

### Fields 

The fields of the shape size definition are as follows:

| Field Name                    | Type                                                                                                  | Description                                                                               |
| ----------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| **WidthRange** **1*           | [ShapeDimensionRange](010-Ranges.md "The ShapeDimensionRange type and module")                        | The range of possible widths for the shapes                                               |
| **WidthProfile** **2*         | [Profile](../QuickVectors.Core.FSharp/080-Profile.md "The Profile type and module")                   | The profile used to determine the widths of the shapes                                    |
| **WidthReordering** **2*      | [SequenceReordering](020-ReorderingAndModification.md "The SequenceReordering type and module") **3*  | The sequence ordering which can modify the width values generated via the profile         |
| **WidthModification**         | [ValueModification](020-ReorderingAndModification.md "The ValueModification type and module") **3*    | The width value modification which can take place whether reordering happened or not      |
| **HeightsEqualWidths**        | bool                                                                                                  | Determines whether the generated heights will equal the generated widths                  |
| **HeightRange** **1*          | [ShapeDimensionRange](010-Ranges.md "The ShapeDimensionRange type and module")                        | The range of possible heights for the shapes                                              |
| **HeightProfile** **2*        | [Profile](../QuickVectors.Core.FSharp/080-Profile.md "The Profile type and module")                   | The profile used to determine the heights of the shapes                                   |
| **HeightReordering** **2*     | [SequenceReordering](020-ReorderingAndModification.md "The SequenceReordering type and module") **3*  | The sequence ordering which can modify the height values generated via the profile        |
| **HeightModification**        | [ValueModification](020-ReorderingAndModification.md "The ValueModification type and module") **3*    | The height value modification which can take place whether reordering happened or not     |

- **1* : Use a single-value range to have all values the same.
- **2* : Irrelevant (ignored) for a single value range.
- **3* : An Option field.

When `HeightsEqualWidths` is true, the Height... field values are ignored and the values for the widths are also used for the heights.

Below is an example shape size definition where all the values have been chosen manually:

```fsharp 
let custom = 
    {   ShapeSizeDefinition.WidthRange = ShapeDimensionRange.fromFloats 30.0 70.0 
        WidthProfile = Profile.Linear 
        WidthReordering = None 
        WidthModification = None 
        HeightsEqualWidths = false 
        HeightRange = ShapeDimensionRange.fromFloats 20.0 80.0 
        HeightProfile = Profile.HockeyStick
        HeightReordering = Some SequenceReordering.ReversedSequence 
        HeightModification = Some ValueModification.InvertValues }
    // -> { WidthRange = ShapeDimRange(30,70)
    //      WidthProfile = Linear
    //      WidthReordering = None
    //      WidthModification = None
    //      HeightsEqualWidths = false
    //      HeightRange = ShapeDimRange(20,80)
    //      HeightProfile = HockeyStick
    //      HeightReordering = Some ReversedSequence
    //      HeightModification = Some InvertValues }
```

### Construction

There are no construction functions, as such, but there are some convenience functions which allow you to
create some basic definitions without having to specify the values for lots of fields.

These convenience functions are:

- `fromSingleFloat` : Create a shape size definition where all shapes will have the same size (width and height) as specified;
- `fromWidthAndHeight` : Create a shape size definition where all shapes will have the same width and the same height as specified;
- `fromWidthSpread` : Create a shape size definition where all shapes will have widths between the two values and the heights will equal the widths.

When using a convenience function, all fields other than those mentioned are given default values as defined
in the respective modules or Option.None as appropriate.

> **Note:** Sequence reordering, if any, will always occur before value modification, if any.

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
let twentyByFourty = 
    ShapeSizeDefinition.fromWidthAndHeight 20.0 40.0 
    // -> { WidthRange = ShapeDimOnly(20)
    //      WidthProfile = Random
    //      WidthReordering = None
    //      WidthModification = None
    //      HeightsEqualWidths = false
    //      HeightRange = ShapeDimOnly(40)
    //      HeightProfile = Random
    //      HeightReordering = None
    //      HeightModification = None }

let modified = 
    { twentyByFourty with 
        WidthProfile = Profile.Linear 
        HeightsEqualWidths = false 
        HeightRange = ShapeDimensionRange.fromFloats 50.0 80.0 
        HeightProfile = Profile.QuarterPipe
        HeightReordering = Some SequenceReordering.ReversedSequence } 
    // -> { WidthRange = ShapeDimOnly(20)
    //      WidthProfile = Linear
    //      WidthReordering = None
    //      WidthModification = None
    //      HeightsEqualWidths = false
    //      HeightRange = ShapeDimRange(50,80)
    //      HeightProfile = QuarterPipe
    //      HeightReordering = Some ReversedSequence
    //      HeightModification = None }
```

### Generation 

While you wouldn't normally need to generate the width and height sequences from a shape size definition
manually - it's better to do that via a pattern - you can do so via the `generateSequences` function
if you wish, like this:

```fsharp 
let widthRng = System.Random 35921 // Randomly-chosen seed.
let heightRng = System.Random 4982 // Randomly-chosen seed.

// Using the custom shape size definition from the earlier example.

let widths, heights = 
    custom 
    |> ShapeSizeDefinition.generateSequences widthRng heightRng 20 

// widths = seq { 30.0; 32.10526316; 34.21052632; 36.31578947;
//                38.42105263; 40.52631579; 42.63157895; 44.73684211;
//                46.84210526; 48.94736842; 51.05263158; 53.15789474;
//                55.26315789; 57.36842105; 59.47368421; 61.57894737;
//                63.68421053; 65.78947368; 67.89473684; 70.0 }

// heights = seq { 20.0; 24.95476072; 29.87567541; 34.72912922;
//                 39.48196814; 44.10172547; 48.55684357; 52.81688948;
//                 56.85276276; 60.63689429; 64.14343464; 67.34843056;
//                 70.22998869; 72.76842507; 74.9463996; 76.7490345;
//                 78.16401596; 79.1816782; 79.79506958; 80.0 }
```

> **Note:** Random number generators are required even if the chosen profiles have no randomness.

## Ready-made Shape Size Definitions

The ready-made shape size definitions available are:

- `basic` : All shapes will be 50x50 - useful to minimise the number of fields that you need to specify;
- `fullRangeRandom` : Shapes can have any width or height and these dimensions are chosen at random;
- `fullWidthHalfHeight` : All shapes have a maximum width and a height which is half of that;
- `halfWidthFullHeight` : All shapes have a maximum height and a width which is half of that.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.