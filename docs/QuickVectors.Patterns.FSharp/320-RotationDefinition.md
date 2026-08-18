# QuickVectors.Patterns.FSharp

# Rotation Definition

This type lets you define what the possible rotation modifiers will be.

- The [Rotation Definition Type](#the-rotation-definition-type)
    - [Fields](#fields)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
    - [Generation](#generation)
    - [Ready-made Rotation Definitions](#ready-made-rotation-definitions)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Rotation Definition Type

The `RotationDefinition` **type** defines a record which is used to specify which rotation modifiers are generated.

> **Note:** Rotation modifiers are number of degrees between a minimum of -180.0 and a maximum of +180.0 (inclusive).

A positive rotation is a clockwise rotation.

A shape is rotated about its centre.

Rotation modifiers are applicable to all shapes.

### Fields 

The fields of the rotation definition are as follows:

| Field Name                | Type                      | Description                                                                               |
| ------------------------- | ------------------------- | ----------------------------------------------------------------------------------------- |
| **Range** **1*            | [RotationModifierRange](010-Ranges.md "The RotationModifierRange type and module")     | The range of possible rotation modifiers for the shapes                                   |
| **Profile** **2*          | [Profile](../QuickVectors.Core.FSharp/080-Profile.md "The Profile type and module")                   | The profile used to determine the rotation modifiers of the shapes                        |
| **Reordering** **2*       | [SequenceReordering](020-ReorderingAndModification.md "The SequenceReordering type and module") **3*   | The sequence ordering which can modify the modifer values generated via the profile       |
| **Modification**          | [ValueModification](020-ReorderingAndModification.md "The ValueModification type and module") **3*    | The value modification which can take place whether reordering happened or not            |

- **1* : Use a single-value range to have all values the same.
- **2* : Irrelevant (ignored) for a single value range.
- **3* : An Option field.

Below is an example rotation definition where all the values have been chosen manually:

```fsharp 
let custom = 
    {   RotationDefinition.Range = RotationModifierRange.fromFloats -20.0 20.0 
        Profile = Profile.Random
        Reordering = None 
        Modification = None }
    // -> { Range = RotationRange(-20,20)
    //      Profile = Random
    //      Reordering = None
    //      Modification = None }
```

### Construction

There are no construction functions, as such, but there are some convenience functions which allow you to
create some basic definitions without having to specify the values for lots of fields.

These convenience functions are:

- `fromSingleFloat` : Create a rotation definition where all modifiers will have the same value as specified;
- `fromFloats` : Create a rotation definition where all modifiers will be between the values specified;
- `fromRange` : Create a rotation definition where the range will be as specified.

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
let tens = RotationDefinition.fromFloats -10.0 10.0 
    // -> { Range = RotationRange(-10,10)
    //      Profile = Random
    //      Reordering = None
    //      Modification = None }

let modified = 
    { tens with 
        Profile = Profile.HockeyStick 
        Reordering = Some SequenceReordering.ReversedSequence } 
    // -> { Range = RotationRange(-10,10)
    //      Profile = HockeyStick
    //      Reordering = Some ReversedSequence
    //      Modification = None }
```

### Generation 

While you wouldn't normally need to generate the sequence from a rotation definition
manually - it's better to do that via a pattern - you can do so via the `generateSequence` function
if you wish, like this:

```fsharp 
let rng = System.Random 4501 // Randomly-chosen seed.

// Using the custom rotation definition from the earlier example.

let modifiers = 
    custom 
    |> RotationDefinition.generateSequence rng 20 
    // -> seq { -13.49670259; -0.219074702; 16.51871316; -9.408329739;
    //          -6.266086468; 18.91650692; 4.368916463; 0.9469977305; 
    //          13.05673267; -19.10420218; -7.359498026; -1.47870184; 
    //          13.99499884; -14.46084741; 2.220754876; 19.9568483; 
    //          15.94179468; 4.492726095; 0.8396040373; -15.04930036 }
```

> **Note:** A random number generator is required even if the chosen profile has no randomness.

## Ready-made Rotation Definitions

The ready-made rotation definitions available are:

- `noRotation` : No shapes will be rotated;
- `fullRangeRandom` : Allow all possible rotation modifiers and choose from them randomly;
- `fifteensRandom` : Randomly choose rotation modifiers from -15.0 to +15.0 (inclusive);
- `thirtiesRandom` : Randomly choose rotation modifiers from -30.0 to +30.0 (inclusive);
- `fourtyFivesRandom` : Randomly choose rotation modifiers from -45.0 to +45.0 (inclusive);
- `ninetiesRandom` : Randomly choose rotation modifiers from -90.0 to +90.0 (inclusive).

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.