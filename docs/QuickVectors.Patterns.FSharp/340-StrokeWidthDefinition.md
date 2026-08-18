# QuickVectors.Patterns.FSharp

# Stroke Width Definition

This type lets you define what the possible stroke widths will be.

- The [Stroke Width Definition Type](#the-stroke-width-definition-type)
    - [Fields](#fields)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
    - [Generation](#generation)
    - [Ready-made Stroke Width Definitions](#ready-made-stroke-width-definitions)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Stroke Width Definition Type

The `StrokeWidthDefinition` **type** defines a record which is used to specify which stroke widths are generated.

> **Note:** Stroke Widths are between a minimum of 0.0 and a maximum of 25.0 (inclusive).

Stroke Widths are applicable to all shapes.

### Fields 

The fields of the stroke width definition are as follows:

| Field Name                | Type                      | Description                                                                               |
| ------------------------- | ------------------------- | ----------------------------------------------------------------------------------------- |
| **Range** **1*            | [StrokeWidthRange](010-Ranges.md "The StrokeWidthRange type and module")          | The range of possible stroke widths                                                       |
| **Profile** **2*          | [Profile](../QuickVectors.Core.FSharp/080-Profile.md "The Profile type and module")                   | The profile used to determine the stroke widths                                           |
| **Reordering** **2*       | [SequenceReordering](020-ReorderingAndModification.md "The SequenceReordering type and module") **3*   | The sequence ordering which can modify the modifer values generated via the profile       |
| **Modification**          | [ValueModification](020-ReorderingAndModification.md "The ValueModification type and module") **3*    | The value modification which can take place whether reordering happened or not            |

- **1* : Use a single-value range to have all values the same.
- **2* : Irrelevant (ignored) for a single value range.
- **3* : An Option field.

Below is an example stroke width definition where all the values have been chosen manually:

```fsharp 
let custom = 
    {   StrokeWidthDefinition.Range = StrokeWidthRange.fromFloats 1.0 10.0 
        Profile = Profile.QuarterPipe 
        Reordering = None 
        Modification = Some ValueModification.InvertValues }
    // -> { Range = StrokeWidthRange(1,10)
    //      Profile = QuarterPipe
    //      Reordering = None
    //      Modification = Some InvertValues }
```

### Construction

There are no construction functions, as such, but there are some convenience functions which allow you to
create some basic definitions without having to specify the values for lots of fields.

These convenience functions are:

- `fromSingleFloat` : Create a stroke width definition where all widths will have the same value as specified;
- `fromFloats` : Create a stroke width definition where all widths will be between the values specified;
- `fromRange` : Create a stroke width definition where the range will be as specified.

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
let fiveFifteen = StrokeWidthDefinition.fromFloats 5.0 15.0 
    // -> { Range = StrokeWidthRange(5,15)
    //      Profile = Random
    //      Reordering = None
    //      Modification = None }

let modified = 
    { fiveFifteen with 
        Profile = Profile.HockeyStick 
        Reordering = Some SequenceReordering.ReversedSequence } 
    // -> { Range = StrokeWidthRange(5,15)
    //      Profile = HockeyStick
    //      Reordering = Some ReversedSequence
    //      Modification = None }
```

### Generation 

While you wouldn't normally need to generate the sequence from a stroke width definition
manually - it's better to do that via a pattern - you can do so via the `generateSequence` function
if you wish, like this:

```fsharp 
let rng = System.Random 6803 // Randomly-chosen seed.

// Using the custom stroke width definition from the earlier example.

let modifiers = 
    custom 
    |> StrokeWidthDefinition.generateSequence rng 20 
    // -> seq { 10.0; 9.987525982; 9.949999613; 9.887103545; 
    //          9.798293715; 9.682775001; 9.539463547; 9.366931347; 
    //          9.163325866; 8.926252883; 8.652602621; 8.338284235; 
    //          7.977804145; 7.563560955; 7.084583853; 6.52405969;
    //          5.853818784; 5.019343809; 3.881308567; 1.0 }
```

> **Note:** A random number generator is required even if the chosen profile has no randomness.

## Ready-made Stroke Width Definitions

The ready-made stroke width definitions available are:

- `one` : A stroke width of one only;
- `two` : A stroke width of two only;
- `five` : A stroke width of five only;
- `ten` : A stroke width of ten only;
- `fullRange` : A stroke width range of maximum extent, i.e. a low value of 0.0 and a high value of 25.0.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.