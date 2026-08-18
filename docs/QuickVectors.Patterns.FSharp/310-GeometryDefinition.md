# QuickVectors.Patterns.FSharp

# Geometry Definition

This type lets you define what the possible geometry modifiers will be.

- The [Geometry Definition Type](#the-geometry-definition-type)
    - [Fields](#fields)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
    - [Generation](#generation)
    - [Ready-made Geometry Definitions](#ready-made-geometry-definitions)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Geometry Definition Type

The `GeometryDefinition` **type** defines a record which is used to specify which geometry modifiers are generated.

> **Note:** Geometry modifiers are percentages between a minimum of 0.0% and a maximum of 100.0% (inclusive).

Geometry modifiers are only applicable to certain shapes and they affect different things depending on the shape:

| [Shape](../QuickVectors.Core.FSharp/020-Shape.md "The Shape type and module") **1*            | Affects **2*                  | Larger modifier = **3* |
| --------------------- | ----------------------------- | ---------------------- |
| RectangleRing         | The size of the hole          | Larger hole            |
| RoundedRectangle      | The size of the corner        | Larger corner          |
| RoundedRectanglePath  | The size of the corner        | Larger corner          |
| EllipseRing           | The size of the hole          | Larger hole            |
| RandomQuadrilateral   | The offset distances          | Larger possible offset |
| Plus                  | The thicknesses of the 'bars' | Thicker 'bars'         |

- **1* : The name of the Shape case, e.g. `Shape.RectangleRing`.
- **2* : Which part(s) of the shape the geometry modification affects.
- **3* : How a larger value affects the shape.

For example, with the RectangleRing, a geometry modifier of 75% will make the width of the hole 75% of the
width of the shape and the height of the hole will be 75% of the height of the shape (if the width and height
of the shape are different then the width and height of the hole will be different).

If the selected shape is not one of those in the table above then the geometry modifiers are ignored.

### Fields 

The fields of the geometry definition are as follows:

| Field Name                | Type                      | Description                                                                               |
| ------------------------- | ------------------------- | ----------------------------------------------------------------------------------------- |
| **Range** **1*            | [GeometryModifierRange](010-Ranges.md "The GeometryModifierRange type and module")     | The range of possible geometry modifiers for the shapes                                   |
| **Profile** **2*          | [Profile](../QuickVectors.Core.FSharp/080-Profile.md "The Profile type and module")                   | The profile used to determine the geometry modifiers of the shapes                        |
| **Reordering** **2*       | [SequenceReordering](020-ReorderingAndModification.md "The SequenceReordering type and module") **3*   | The sequence ordering which can modify the modifer values generated via the profile       |
| **Modification**          | [ValueModification](020-ReorderingAndModification.md "The ValueModification type and module") **3*    | The value modification which can take place whether reordering happened or not            |

- **1* : Use a single-value range to have all values the same.
- **2* : Irrelevant (ignored) for a single value range.
- **3* : An Option field.

Below is an example geometry definition where all the values have been chosen manually:

```fsharp 
let custom = 
    {   GeometryDefinition.Range = GeometryModifierRange.fromFloats 25.0 75.0 
        Profile = Profile.QuarterPipe 
        Reordering = None 
        Modification = Some ValueModification.InvertValues }
    // -> { Range = GeometryModRange(25,75)%
    //      Profile = QuarterPipe
    //      Reordering = None
    //      Modification = Some InvertValues }
```

### Construction

There are no construction functions, as such, but there are some convenience functions which allow you to
create some basic definitions without having to specify the values for lots of fields.

These convenience functions are:

- `fromSingleFloat` : Create a geometry definition where all modifiers will have the same value as specified;
- `fromFloats` : Create a geometry definition where all modifiers will be between the values specified;
- `fromRange` : Create a geometry definition where the range will be as specified.

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
let fiveNinetyFive = GeometryDefinition.fromFloats 5.0 95.0 
    // -> { Range = GeometryModRange(5,95)%
    //      Profile = Random
    //      Reordering = None
    //      Modification = None }

let modified = 
    { fiveNinetyFive with 
        Profile = Profile.HockeyStick 
        Reordering = Some SequenceReordering.ReversedSequence } 
    // -> { Range = GeometryModRange(5,95)%
    //      Profile = HockeyStick
    //      Reordering = Some ReversedSequence
    //      Modification = None }
```

### Generation 

While you wouldn't normally need to generate the sequence from a geometry definition
manually - it's better to do that via a pattern - you can do so via the `generateSequence` function
if you wish, like this:

```fsharp 
let rng = System.Random 90316 // Randomly-chosen seed.

// Using the custom geometry definition from the earlier example.

let modifiers = 
    custom 
    |> GeometryDefinition.generateSequence rng 20 
    // -> seq { 75.0; 74.9306999; 74.72222007; 74.37279747;
    //          73.87940953; 73.23763889; 72.44146415; 71.48295193;
    //          70.35181037; 69.03473824; 67.514459; 65.76824575;
    //          63.76557859; 61.46422753; 58.80324363; 55.6892205;
    //          51.96565991; 47.32968783; 41.00726982; 25.0 }
```

> **Note:** A random number generator is required even if the chosen profile has no randomness.

## Ready-made Geometry Definitions

The ready-made geometry definitions available are:

- `fullRangeRandom` : Allow all possible geometry modifiers and choose from them randomly;
- `tenNinetyRandom` : Randomly choose geometry modifiers from 10% to 90% (inclusive);
- `twentyEightyRandom` : Randomly choose geometry modifiers from 20% to 80% (inclusive);
- `thirtySeventyRandom` : Randomly choose geometry modifiers from 30% to 70% (inclusive);
- `fiftyFifty` : All geometry modifiers will be 50%.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.