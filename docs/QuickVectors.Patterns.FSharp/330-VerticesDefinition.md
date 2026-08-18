# QuickVectors.Patterns.FSharp

# Vertices Definition

This type lets you define what the possible number of vertices will be.

- The [Vertices Definition Type](#the-vertices-definition-type)
    - [Fields](#fields)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
    - [Generation](#generation)
    - [Ready-made Vertices Definitions](#ready-made-vertices-definitions)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Vertices Definition Type

The `VerticesDefinition` **type** defines a record which is used to specify which numbers of vertices are generated.

> **Note:** The numbers of vertices are integers between a minimum of 3 and a maximum of 20 (inclusive).

Vertices are only applicable to certain shapes:

| [Shape](../QuickVectors.Core.FSharp/020-Shape.md "The Shape type and module") **1*          | Affects **2*                  |
| ------------------- | ----------------------------- |
| RegularPolygon      | Number of corners/sides       |
| ShuffledPolygon     | Number of corners/sides       |
| RandomPolygon       | Number of corners/sides       |
| Star                | Number of points              |
| DoubleStar          | Number of points in each star |
| Flower              | Number of 'petals'            |
| Spikey              | Number of spikes              |
| Blob                | Number of control points      |
| Squiggle            | Number of control points      |

- **1* : The name of the Shape case, e.g. `Shape.RandomPolygon`.
- **2* : Which part(s) of the shape the number of vertices affects.

If the selected shape is not one of those in the table above then the vertices are ignored.

### Fields 

The fields of the vertices definition are as follows:

| Field Name                | Type                      | Description                                                                               |
| ------------------------- | ------------------------- | ----------------------------------------------------------------------------------------- |
| **Range** **3*            | [NumberOfVerticesRange](010-Ranges.md "The NumberOfVerticesRange type and module")     | The range of possible numbers of vertices for each shape                                  |
| **Profile** **4*          | [Profile](../QuickVectors.Core.FSharp/080-Profile.md "The Profile type and module")                   | The profile used to determine the number of vertices for each shape                       |
| **Reordering** **4*       | [SequenceReordering](020-ReorderingAndModification.md "The SequenceReordering type and module") **5*   | The sequence ordering which can modify the modifer values generated via the profile       |
| **Modification**          | [ValueModification](020-ReorderingAndModification.md "The ValueModification type and module") **5*    | The value modification which can take place whether reordering happened or not            |

- **3* : Use a single-value range to have all values the same.
- **4* : Irrelevant (ignored) for a single value range.
- **5* : An Option field.

Below is an example vertices definition where all the values have been chosen manually:

```fsharp 
let custom = 
    {   VerticesDefinition.Range = NumberOfVerticesRange.fromInts 4 15
        Profile = Profile.SineWave 
        Reordering = None 
        Modification = Some ValueModification.InvertValues }
    // -> { Range = VerticesRange(4,15)
    //      Profile = SineWave
    //      Reordering = None
    //      Modification = Some InvertValues }
```

### Construction

There are no construction functions, as such, but there are some convenience functions which allow you to
create some basic definitions without having to specify the values for lots of fields.

These convenience functions are:

- `fromSingleInt` : Create a vertices definition where the number of vertices will all be the value as specified;
- `fromIns` : Create a vertices definition where the number of vertices will be between the values specified;
- `fromRange` : Create a vertices definition where the range will be as specified.

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
let sixToNine= VerticesDefinition.fromInts 6 9 
    // -> { Range = VerticesRange(6,9)
    //      Profile = Random
    //      Reordering = None
    //      Modification = None }

let modified = 
    { sixToNine with 
        Profile = Profile.HockeyStick 
        Reordering = Some SequenceReordering.ReversedSequence } 
    // -> { Range = VerticesRange(6,9)
    //      Profile = HockeyStick
    //      Reordering = Some ReversedSequence
    //      Modification = None }
```

### Generation 

While you wouldn't normally need to generate the sequence from a vertices definition
manually - it's better to do that via a pattern - you can do so via the `generateSequence` function
if you wish, like this:

```fsharp 
let rng = System.Random 1397 // Randomly-chosen seed.

// Using the custom vertices definition from the earlier example.

let vertices = 
    custom 
    |> VerticesDefinition.generateSequence rng 20 
    // -> seq { 9; 7; 6; 4; 4; 4; 4; 5; 6; 8; 
    //          10; 12; 13; 14; 14; 14; 14; 12; 11; 9 }
```

> **Note:** A random number generator is required even if the chosen profile has no randomness.

## Ready-made Vertices Definitions

The ready-made vertices definitions available are:

- `triangles` : Only shapes with three vertices will be generated (e.g. triangles);
- `quadrilaterals` : Only shapes with four vertices will be generated (e.g. quadrilaterals);
- `pentagons` : Only shapes with five vertices will be generated (e.g. pentagons);
- `hexagons` : Only shapes with six vertices will be generated (e.g. hexagons);
- `septagons` : Only shapes with seven vertices will be generated (e.g. septagons);
- `octagons` : Only shapes with eight vertices will be generated (e.g. octagons);
- `lowValuesRandom` : Randomly choose the number of vertices between 3 (triangle) and 8 (octagon) (inclusive);
- `pentToDecRandom` : Randomly choose the number of vertices between 5 (pentagon) and 10 (decagon) (inclusive);
- `middleValuesRandom` : Randomly choose the number of vertices between 9 (nonagon) and 14 (tetradecagon) (inclusive).
- `fullRangeRandom` : Allow all possible number of vertices and choose from them randomly.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.