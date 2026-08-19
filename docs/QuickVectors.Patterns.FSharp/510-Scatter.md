# QuickVectors.Patterns.FSharp

# Scatter

This type lets you define a pattern which is based around shapes being scattered across an area.

- The [Scatter Type](#the-scatter-type)
    - [Fields](#fields)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
    - [Generation](#generation)
    - [Ready-made Scatter Patterns](#ready-made-scatter-patterns)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

![Scatter Examples Image](images/Scatter-Examples.png "Scatter Examples")

## The Scatter Type

The `Scatter` **type** defines a record which is used to specify a scatter pattern.

### Fields 

The fields of the scatter pattern are as follows:

| Field Name                | Type                                                                                              | Purpose / Defines                                             |
| ------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| **RandomSeed**            | [RandomSeed](../QuickVectors.Core.FSharp/010-RandomSeed.md "The RandomSeed type and module")      | Random seed used to generate random numbers                   |
| **NumberOfShapes**        | [NumberOfShapes](060-NumberOfShapes.md "The NumberOfShapes type and module")                      | The number of shapes to generate                              |
| **Shape**                 | [Shape](../QuickVectors.Core.FSharp/020-Shape.md "The Shape type and module")                     | Shape to be used in the pattern                               |
| **ShapeSize**             | [ShapeSizeDefinition](300-ShapeSizeDefinition.md "The ShapeSizeDefinition type and module")       | Size(s) of the shapes which will be generated                 |
| **Geometry**              | [GeometryDefinition](310-GeometryDefinition.md "The GeometryDefinition type and module")          | Geometries of the shapes                                      |
| **Rotation**              | [RotationDefinition](320-RotationDefinition.md "The RotationDefinition type and module")          | Rotations of the shapes                                       |
| **Vertices**              | [VerticesDefinition](330-VerticesDefinition.md "The VerticesDefinition type and module")          | Vertices of the shapes                                        |
| **BoundarySize**          | [BoundarySize](100-BoundarySize.md "The BoundarySize type and module")                            | The size of the area over which the shapes will be scattered  |
| **KeepShapesInBoundary**  | bool                                                                                              | Make sure that the shapes will be contained in the boundary   |
| **ScatterArea**           | [ScatterAreaDefinition](370-ScatterAreaDefinition.md "The ScatterAreaDefinition type and module") | The type of area over which the shapes will be scattered      |
| **Fill**                  | [FillDefinition](350-FillDefinition.md "The FillDefinition type and module") **1*                 | Fill colours of the shapes                                    |
| **Stroke**                | [StrokeDefinition](360-StrokeDefinition.md "The StrokeDefinition type and module") **1*           | Colours and widths of the shape strokes                       |
| **BoundaryFrame**         | [FrameDefinition](490-Frames.md "The FrameDefinition type and module") **1*                       | The boundary frame                                            |

- **1* : An Option field.

> **Notes:**
>
> 1. If you specify `None` for both the Fill and Stroke fields then all of the shapes will be invisible.
>
> 2. You can specify a StrokeDefinition with a ColourScheme of `ColourScheme.allNoColour` to get strokes that will be
in the exported design but not visible.
>
> 3. `KeepShapesInBoundary`, when true, makes sure that the shapes will fit inside the boundary no matter how they are rotated.
This can be useful if you want to align different scatter patterns.

Below is an example scatter pattern where all the values have been chosen manually:

```fsharp 
let bubbles = 
    {   Scatter.RandomSeed = RandomSeed.generate()
        NumberOfShapes = NumberOfShapes.fromInt 250
        Shape = Shape.Ellipse
        ShapeSize = {   ShapeSizeDefinition.basic with 
                            WidthRange = ShapeDimensionRange.fromFloats 10.0 50.0 
                            WidthProfile = Profile.Linear 
                            WidthReordering = Some SequenceReordering.ReversedSequence}
        Geometry = GeometryDefinition.fullRangeRandom
        Rotation = RotationDefinition.noRotation
        Vertices = VerticesDefinition.fromInts 3 5
        BoundarySize = BoundarySize.thousandByThousand
        KeepShapesInBoundary = false
        ScatterArea = {   AreaShape = ScatterAreaShape.Rectangular 
                          HorizontalProfile = Profile.Random
                          VerticalProfile = Profile.Linear 
                          HoleSize = ScatterHoleSize.fromFloat 50.0 }
        Fill = StandardPalette.Shades.coolBlue 
               |> Palette.lighter Luminosity.oneFifth 
               |> ColourScheme.RandomFromPalette 
               |> FillDefinition.fromColourScheme 
               |> Some 
        Stroke = None 
        BoundaryFrame = None }
```

(The above example is the `Scatter.bubbles` ready-made pattern as mentioned below.)

As noted elsewhere in the documentation, not all fields are used/valid in all situations.
For example, the `Vertices` field is ignored when the `Shape` specified does not have any vertices, such as Ellipse.

The type has been designed in this way to make it easier to experiment with different shapes without you having to remember
which shape uses which other fields; otherwise you would have to create new shape definitions to use different shapes
with similar configurations, and that's just a bit of a pain. (The design would be 'cleaner' but it would be more
awkward to use in practice, so doing it this way lets you try different ideas more quickly.)

### Construction

There are no construction functions, just specify the fields as you would with any normal F# record.

> **Note:** The contents of some fields may, under certain circumstances:
>
> - not do anything (e.g. vertices only affect certain shapes), or;
>
> - not make any noticable difference (e.g. some Profiles are quite similar), or;
> 
> - negate the effect of one or more other fields (e.g. reversing a sequence **and** inverting the values at the same time).
>
> Because of this it is recommended that you experiment with lots of different combinations of field values to find what can be achieved.

### Deconstruction

There are no deconstruction functions for the type itself but you can deconstruct each field with the
deconstruction function appropriate for the type of that field or the fields in that type.

### Variations 

There are no functions for varying the values of the fields but you can, since all field values are type-checked and valid,
change the values in the same way as you would with any F# record.  
For example: `let newRecord = { oldRecord with FieldName = newValue }`.

Some convenience functions are available which can be useful:

- `withNewRandomSeed` : Randomly generates a new random seed;
- `withDifferentShape` : Uses a different shape;
- `withDifferentNumberOfShapes` : Sets the number of shapes to a new value;
- `withFrame` : Adds a standard boundary frame to a pattern;
- `withoutFrame` : Removes the frame from a pattern.

```fsharp 
Scatter.bubbles // A ready-made design.
|> Scatter.withDifferentNumberOfShapes 500 // With more shapes.
|> Scatter.withFrame // With a frame.
```

### Generation 

You can generate the design information for a scatter pattern by using the
`Scatter.generate` function, passing in a `Scatter` type as the only parameter.

You would not usually need to investigate or manipulate the generated design information, rather you would
usually pass the design information into an export function in the `QuickVectors.Export.FSharp` package, like this:

```fsharp 
open System.IO // Required for the File functionality.
open QuickVectors.Patterns.FSharp // Required for generating the design.
open QuickVectors.Export.Svg.FSharp // Required for exporting.

Scatter.bubbles // A ready-made design.
|> Scatter.generate // Generate the design.
|> Svg.export SvgExportSettings.standard // Create the SVG text.
|> fun svg -> File.WriteAllText("Bubbles.svg", svg) // Save to file.
```

If there is a problem generating or exporting the design then an exception will be raised.
Please report any exceptions along with the circumstances under which they occurred.

> **IMPORTANT:**
>
> 1. The pattern itself does not contain any shapes/elements and is only a 'promise' of a design. Shapes/elements
are only created when you generate the pattern into a design.
>
> 2. When you generate pattern into a design, the random numbers used in the design are 'baked in' at the time
of generation so that if you generate the design again, or export the same design again, you will get the same design
with the same randomness. This allows you to save the parameters used in the pattern for replication at another time.
If you don't want this then you can change the RandomSeed field before (re-)generation.

## Ready-made Scatter Patterns

The ready-made scatter patterns available are:

- `confetti` : A pattern which looks like paper confetti has been thrown;
- `heartthrob` : A pattern which looks like an elliptical ring of hearts (maybe to put round an image);
- `bubbles` : A pattern which looks (a bit) like bubbles floating up;
- `seventiesWallpaper` : A pattern which looks like wallpaper from the 1970's.

You can make variations of these ready-made patterns or examine them to give you ideas
for your own patterns.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.