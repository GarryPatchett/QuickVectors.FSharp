# QuickVectors.FSharp 

This is a short tutorial for the QuickVectors.FSharp packages.

## Contents

- [Installation](#installation)
- [First Steps](#first-steps)
    - [Step 1 - Your First Design](#step-1---your-first-design)
    - [Viewing The Pattern](#viewing-the-pattern)
    - [Step 2 - Changing The Fill](#step-2---changing-the-fill)
    - [Step 3 - Changing The Colours](#step-3---changing-the-colours)
    - [Step 4 - Removing The Outline](#step-4---removing-the-outline)
    - [Step 5 - Adding Some Gaps](#step-5---adding-some-gaps)
    - [Step 6 - Adding Some Rotation](#step-6---adding-some-rotation)
    - [Step 7 - Adding Shape Size Variation](#step-7---adding-shape-size-variation)
    - [Step 8 - Changing The Shape](#step-8---changing-the-shape)
    - [Step 9 - Fills To Outlines](#step-9---fills-to-outlines)
    - [Step 10 - Adding Some Colour Variation](#step-10---adding-some-colour-variation)
    - [Step 11 - Using A Different Grid Size](#step-11---using-a-different-grid-size)
    - [Step 12 - Adding An Offset](#step-12---adding-an-offset)
- [What Next](#what-next)
- [Samples](#samples)

> **Note:** This tutorial only covers a small selection of the possibilities of just one of the available patterns.
A lot of the definitions used are shared between different patterns but some are different.
There is so much to see and learn that you might need to put some time aside to really get to grips with what's possible.

## Installation

You can use the `QuickVectors.FSharp` project within a script or within your own code.

If you are just looking to explore the project, or use it to produce something quickly, you
can access the project like this in a script:

```fsharp
#r "nuget: QuickVectors.Export.FSharp"
```

Or, to use it in your own code, add the `QuickVectors.Export.FSharp` Nuget package to your F# project, like this:

```console
dotnet add package QuickVectors.Export.FSharp
```

(The `Export` package is being referenced as it will 'pull in' the other packages as necessary.)

The examples in this tutorial use scripts and the FSI because that's the simplest way to get things happening. The only
difference is how you install/reference the packages as mentioned above, everything else is the same either way.

> **REMEMBER:** Intellisense documentation is available for all of the types and functions which you might need to use.
It is recommended that you refer to that documentation often until you are comfortable in knowing what each type does and how it works.

## First Steps

The `QuickVectors` packages offer dozens of types and modules which can be used in lots of different ways and trying to
learn them all at once could be difficult.

It's probably better to start looking at a ready-made design and then go on to learn the different types by seeing how to change that design. So here we go...

### Step 1 - Your First Design

You can start by making a very simple design based on a ready-made pattern.

In your code editor, create a new script file called "MyFirstDesign.fsx" and copy the code below into that file:

```fsharp
#r "nuget: QuickVectors.Export.FSharp"

// Required for saving the file.
open System.IO 
// Required for various functionalities.
open QuickVectors.FSharp 
// Required for creating the pattern and generating the design.
open QuickVectors.Patterns.FSharp 
// Required for exporting the design.
open QuickVectors.Export.Svg.FSharp 

// Use a ready-made pattern.
ShapeGrid.chessBoard 
// Generate a design from the pattern.
|> ShapeGrid.generate 
// Export the design to a string (contains the SVG description).
|> Svg.export SvgExportSettings.standard 
// Save the string to a file.
|> fun svg -> File.WriteAllText(@"MyFirstDesign.svg", svg) 
```

You can now send the file to the FSI (however you would normally do it via your code editor) to be evaluated and
you should have an SVG file in your current directory named "MyFirstDesign.svg".
(You can change the file path/name as appropriate to your set-up/requirements.)

You can view this SVG file using a web browser or any other application which can display SVG files.

When viewing the file you should see an eight-by-eight chessboard with alternating black- and white-filled squares, each with a thin black outline.

### Viewing The Pattern

If you want to look at the pattern definition you can, rather than simply passing it straight to the generate function,
assign it to a value (like you would any other F# value) and you will see something like this in the FSI output
(I've added comments as appropriate):

```fsharp
{   // The random seed used to generate random values.
    RandomSeed = Random(1009235079) 
    // The shape to be used.
    Shape = Rectangle 
    ShapeSize = { // The range of shape widths.
                  WidthRange = ShapeDimOnly(100) 
                  // The profile used to generate the shape widths.
                  WidthProfile = Random 
                  // How/whether the widths will be reordered.
                  WidthReordering = None 
                  // How/whether the widths will be further modified.
                  WidthModification = None 
                  // Keep the heights equal to the widths?
                  HeightsEqualWidths = false 
                  // The range of shape heights.
                  HeightRange = ShapeDimOnly(100) 
                  // The profile used to generate the shape heights.
                  HeightProfile = Random 
                  // How/whether the heights will be reordered.
                  HeightReordering = None 
                  // How/whether the heights will be further modified.
                  HeightModification = None 
                } 
    Geometry = { // The range of shape geometry modifiers.
                 Range = GeometryModOnly(50)% 
                 // The profile used to generate the geometry modifiers.
                 Profile = Random 
                 // How/whether the geometry modifiers will be reordered.
                 Reordering = None 
                 // How/whether the geometry modifiers will be further modified.
                 Modification = None 
                } 
    Rotation = { // The range of shape rotations.
                 Range = NoRotation 
                 // The profile used to generate the rotations.
                 Profile = LowValue 
                 // How/whether the rotations will be reordered.
                 Reordering = None 
                 // How/whether the roations will be further modified.
                 Modification = None 
                }
    Vertices = { // The range of number of vertices.
                 Range = VerticesOnly(4) 
                 // The profile used to generate the numbers of vertices.
                 Profile = LowValue 
                 // How/whether the numbers of vertices will be reordered.
                 Reordering = None 
                 // How/whether the numbers of vertices will be further modified.
                 Modification = None 
                }
    // The size of the grid (columns and rows).
    GridSize = Grid(8C/8R) 
    // How the cells of the grid will be 'visited'.
    GridRoute = Flow 
    // The size of the gap between columns.
    ColumnGap = None 
    // The size of the gap between rows. 
    RowGap = None 
    // How the even-numbered rows of the grid will be offset.
    GridOffset = None 
    Fill = Some { // The colour scheme used to generate the fill colours.
                  ColourScheme = AlternatingBlackAndWhite 
                  // How/whether the fill colours will be reordered.
                  Reordering = None 
                  // How/whether the fill colours will be further modified.
                  Modification = None 
                  // How/whether the fill colours will be varied 'naturally'.
                  Noise = None 
                }
    Stroke = Some { // The colour scheme used to generate the stroke colours.
                    ColourScheme = AllBlack 
                    Width = { // The range of stroke widths.
                              Range = StrokeWidthOnly(1) 
                              // The profile used to generate the stroke widths.
                              Profile = Random 
                              // How/whether the stroke widths will be reordered.
                              Reordering = None 
                              // How/whether the stroke widths will be further modified.
                              Modification = None 
                            }
                    // How/whether the stroke colours will be reordered.
                    Reordering = None 
                    // How/whether the stroke colours will be further modified.
                    Modification = None 
                    // How/whether the stroke colours will be varied 'naturally'.
                    Noise = None 
                  }
    // Defines a frame for the boundary of the design.
    BoundaryFrame = None 
    // Defines a frame for the extents of the design.
    ExtentsFrame = None 
}
```

As you can see there are a lot of fields but they are, for the most part, fairly self-explanatory
once you get the hang of things.

At the moment you don't need to worry too much about most of these fields; you can come back
later and experiment with them as much as you want.

### Step 2 - Changing The Fill

Now, what if you want red- and blue-filled squares instead? Well, you would need a different fill definition.

Change the code as shown below:

```fsharp
#r "nuget: QuickVectors.Export.FSharp"

open System.IO 
open QuickVectors.FSharp 
open QuickVectors.Patterns.FSharp 
open QuickVectors.Export.Svg.FSharp 

// Create a new fill definition.
let fillDefinition = 
    {   FillDefinition.ColourScheme = 
            ColourScheme.AlternatingBetween (First = Colour.brightRed, Second = Colour.brightBlue) 
        Reordering = None 
        Modification = None 
        Noise = None }

{   ShapeGrid.chessBoard with 
        // Replace the fill definition in the pattern.
        Fill = Some fillDefinition 
} 
|> ShapeGrid.generate 
|> Svg.export SvgExportSettings.standard
|> fun svg -> File.WriteAllText(@"MyFirstDesign.svg", svg) 
```

That's a bit more complicated but you don't need to know everything just yet. The two main things are:

1. You have created a new fill definition called `fillDefinition` which alternates between the colours `Colour.brightRed` and `Colour.brightBlue`;
2. You have created your own copy of the `chessboard` pattern where the fill definition has been replaced with your new fill definition.

You can ignore the `Reordering`, `Modification`, and `Noise` fields of the fill definition for now.

The two colours that you specified are ready-made colours and others are available or you can make your own (see later).

If you send the code to the FSI your design should have changed.

> **Note:** You specify the `Fill` field as `Some fillDefinition` because the `Fill` field is an Option.
If you don't want the shapes to be filled then you can specify the `Fill` field as None.
(Specifying both the `Fill` and `Stroke` fields as None will give you invisible shapes.)

### Step 3 - Changing The Colours 

What if you don't like those particular colours? Well, you can make your own.

Change the code as shown below and send it to the FSI:

(Comments from previous steps have been removed for clarity.)

```fsharp
#r "nuget: QuickVectors.Export.FSharp"

open System.IO 
open QuickVectors.FSharp 
open QuickVectors.Patterns.FSharp 
open QuickVectors.Export.Svg.FSharp 

// Create a new pink colour.
let pink = Colour.fromBytes 252uy 151uy 151uy 

// Create a new light-blue colour.
let lightBlue = Colour.fromHexString "97D5FC"

let fillDefinition = 
    {   FillDefinition.ColourScheme = 
            // Use a different colour scheme in the fill definition.
            ColourScheme.AlternatingBetween (First = pink, Second = lightBlue) 
        Reordering = None 
        Modification = None 
        Noise = None }

{   ShapeGrid.chessBoard with 
        Fill = Some fillDefinition
} 
|> ShapeGrid.generate 
|> Svg.export SvgExportSettings.standard
|> fun svg -> File.WriteAllText(@"MyFirstDesign.svg", svg) 
```

Here you have created two new colours:

1. `pink` by specifying the Red, Green, and Blue luminosities via byte values;
2. `lightBlue` by specifying a hex string.

(There are lots of other ways to create new colours.)

You have also changed the fill definition to use the new colours.

### Step 4 - Removing The Outline

What if you don't like the black outlines? Well, you can remove them.

Change the code as shown below and send it to the FSI:

```fsharp
#r "nuget: QuickVectors.Export.FSharp"

open System.IO 
open QuickVectors.FSharp 
open QuickVectors.Patterns.FSharp 
open QuickVectors.Export.Svg.FSharp 

let pink = Colour.fromBytes 252uy 151uy 151uy 

let lightBlue = Colour.fromHexString "97D5FC"

let fillDefinition = 
    {   FillDefinition.ColourScheme = 
            ColourScheme.AlternatingBetween (First = pink, Second = lightBlue) 
        Reordering = None 
        Modification = None 
        Noise = None }

{   ShapeGrid.chessBoard with 
        Fill = Some fillDefinition 
        // Removed outline.
        Stroke = None 
} 
|> ShapeGrid.generate 
|> Svg.export SvgExportSettings.standard
|> fun svg -> File.WriteAllText(@"MyFirstDesign.svg", svg) 
```

Here you have simply told the pattern to have no Stroke (None, rather than Some).

## Step 5 - Adding Some Gaps

What if you want to have some gaps between the squares. Well, that's easy enough to do.

Change the code as shown below and send it to the FSI:

```fsharp
#r "nuget: QuickVectors.Export.FSharp"

open System.IO 
open QuickVectors.FSharp 
open QuickVectors.Patterns.FSharp 
open QuickVectors.Export.Svg.FSharp 

let pink = Colour.fromBytes 252uy 151uy 151uy 

let lightBlue = Colour.fromHexString "97D5FC"

let fillDefinition = 
    {   FillDefinition.ColourScheme = 
            ColourScheme.AlternatingBetween (First = pink, Second = lightBlue) 
        Reordering = None 
        Modification = None 
        Noise = None }

{   ShapeGrid.chessBoard with 
        // Add a column gap.
        ColumnGap = 40.0 |> ColumnGap.fromFloat |> Some 
        // Add a row gap.
        RowGap = 40.0 |> RowGap.fromFloat |> Some 
        Fill = Some fillDefinition 
        Stroke = None 
} 
|> ShapeGrid.generate 
|> Svg.export SvgExportSettings.standard
|> fun svg -> File.WriteAllText(@"MyFirstDesign.svg", svg) 
```

Here you have added a column gap of 40.0 and a row gap of 40.0.

Both the column gap and the row gap are Option fields, so if you don't want one other the other, or both, you can set the one(s) you don't want to None.

### Step 6 - Adding Some Rotation

What if you want to rotate the shapes randomly? Not a problem.

Change the code as shown below and send it to the FSI:

```fsharp
#r "nuget: QuickVectors.Export.FSharp"

open System.IO 
open QuickVectors.FSharp 
open QuickVectors.Patterns.FSharp 
open QuickVectors.Export.Svg.FSharp 

let pink = Colour.fromBytes 252uy 151uy 151uy 

let lightBlue = Colour.fromHexString "97D5FC"

let fillDefinition = 
    {   FillDefinition.ColourScheme = 
            ColourScheme.AlternatingBetween (First = pink, Second = lightBlue) 
        Reordering = None 
        Modification = None 
        Noise = None }

{   ShapeGrid.chessBoard with 
        // Rotate the shapes randomly.
        Rotation = RotationDefinition.fourtyFivesRandom 
        ColumnGap = 40.0 |> ColumnGap.fromFloat |> Some 
        RowGap = 40.0 |> RowGap.fromFloat |> Some 
        Fill = Some fillDefinition 
        Stroke = None 
} 
|> ShapeGrid.generate 
|> Svg.export SvgExportSettings.standard
|> fun svg -> File.WriteAllText(@"MyFirstDesign.svg", svg) 
```

Here you have used a ready-made rotation definition which rotates shapes randomly between -45.0 and +45.0 degrees.

The rotation definition isn't an Option because, in this pattern, it's always available
to be used even if it is not used in every circumstance.

### Step 7 - Adding Shape Size Variation

And now you want to make the shapes different sizes? Again, not a difficult thing to do.

Change the code as shown below and send it to the FSI:

```fsharp
#r "nuget: QuickVectors.Export.FSharp"

open System.IO 
open QuickVectors.FSharp 
open QuickVectors.Patterns.FSharp 
open QuickVectors.Export.Svg.FSharp 

let pink = Colour.fromBytes 252uy 151uy 151uy 

let lightBlue = Colour.fromHexString "97D5FC"

let fillDefinition = 
    {   FillDefinition.ColourScheme = 
            ColourScheme.AlternatingBetween (First = pink, Second = lightBlue) 
        Reordering = None 
        Modification = None 
        Noise = None }

// Create new shape size definition by modifying a ready-made one.
// (You can also create your from scratch if that's what you prefer.)
let shapeSizeDefinition = 
    {   ShapeSizeDefinition.fullRangeRandom with 
            WidthRange = ShapeDimensionRange.fiftyAndAbove
            HeightsEqualWidths = true }

{   ShapeGrid.chessBoard with 
        // Use new shape size definition.
        ShapeSize = shapeSizeDefinition 
        Rotation = RotationDefinition.fourtyFivesRandom
        ColumnGap = 40.0 |> ColumnGap.fromFloat |> Some
        RowGap = 40.0 |> RowGap.fromFloat |> Some
        Fill = Some fillDefinition 
        Stroke = None 
} 
|> ShapeGrid.generate 
|> Svg.export SvgExportSettings.standard
|> fun svg -> File.WriteAllText(@"MyFirstDesign.svg", svg) 
```

Here you have created a new shape size defininition called `shapeSizeDefinition` which is a modification of a
ready-made definition, and used that in the pattern.

The shape size definition isn't an Option because, in this pattern, it's always applicable.

Remember that you can use Intellisense at any time to get information about any field or type.

### Step 8 - Changing the Shape

And now you want to use a different shape? Easy.

Change the code as shown below and send it to the FSI:

```fsharp
#r "nuget: QuickVectors.Export.FSharp"

open System.IO 
open QuickVectors.FSharp 
open QuickVectors.Patterns.FSharp 
open QuickVectors.Export.Svg.FSharp 

let pink = Colour.fromBytes 252uy 151uy 151uy 

let lightBlue = Colour.fromHexString "97D5FC"

let fillDefinition = 
    {   FillDefinition.ColourScheme = 
            ColourScheme.AlternatingBetween (First = pink, Second = lightBlue) 
        Reordering = None 
        Modification = None 
        Noise = None }

let shapeSizeDefinition = 
    {   ShapeSizeDefinition.fullRangeRandom with 
            WidthRange = ShapeDimensionRange.fiftyAndAbove
            HeightsEqualWidths = true }

{   ShapeGrid.chessBoard with 
        // Use different shape.
        Shape = Shape.RoundedRectanglePath 
        ShapeSize = shapeSizeDefinition 
        Rotation = RotationDefinition.fourtyFivesRandom
        ColumnGap = 40.0 |> ColumnGap.fromFloat |> Some
        RowGap = 40.0 |> RowGap.fromFloat |> Some
        Fill = Some fillDefinition 
        Stroke = None 
} 
|> ShapeGrid.generate 
|> Svg.export SvgExportSettings.standard
|> fun svg -> File.WriteAllText(@"MyFirstDesign.svg", svg) 
```

Here you have simply change the `Shape` field to use a different shape.

### Step 9 - Fills to Outlines

But now you want outlined shapes instead of filled ones? Okay, we can do that.

Change the code as shown below and send it to the FSI:

```fsharp
#r "nuget: QuickVectors.Export.FSharp"

open System.IO 
open QuickVectors.FSharp 
open QuickVectors.Patterns.FSharp 
open QuickVectors.Export.Svg.FSharp 

let pink = Colour.fromBytes 252uy 151uy 151uy 

let lightBlue = Colour.fromHexString "97D5FC"

let fillDefinition = 
    {   FillDefinition.ColourScheme = 
            ColourScheme.AlternatingBetween (First = pink, Second = lightBlue) 
        Reordering = None 
        Modification = None 
        Noise = None }

// No need to lose that fill definition, just make a stroke definition from it.
// (Or you can make one from scratch, it's up to you which you prefer.)
let strokeDefinition = 
    {   (fillDefinition |> StrokeDefinition.fromFillDefinition) with 
            // Change the width of the stroke.
            Width = StrokeWidthDefinition.ten 
    }

let shapeSizeDefinition = 
    {   ShapeSizeDefinition.fullRangeRandom with 
            WidthRange = ShapeDimensionRange.fiftyAndAbove
            HeightsEqualWidths = true }

{   ShapeGrid.chessBoard with 
        Shape = Shape.RoundedRectanglePath
        ShapeSize = shapeSizeDefinition 
        Rotation = RotationDefinition.fourtyFivesRandom
        ColumnGap = 40.0 |> ColumnGap.fromFloat |> Some
        RowGap = 40.0 |> RowGap.fromFloat |> Some
        // No fill now.
        Fill = None 
        // Use the new stroke definition.
        Stroke = Some strokeDefinition 
} 
|> ShapeGrid.generate 
|> Svg.export SvgExportSettings.standard
|> fun svg -> File.WriteAllText(@"MyFirstDesign.svg", svg) 
```

Here you have made a new stroke definition from an existing fill definition, changed the width from
the default of 1.0 to 10.0, and changed the Fill and Stroke fields in the pattern.

(The stroke width can be varied in lots of different ways.)

### Step 10 - Adding Some Colour Variation

And now you want some variety in the outline colours? Again, not a problem.

```fsharp
#r "nuget: QuickVectors.Export.FSharp"

open System.IO 
open QuickVectors.FSharp 
open QuickVectors.Patterns.FSharp 
open QuickVectors.Export.Svg.FSharp 

let pink = Colour.fromBytes 252uy 151uy 151uy 

let lightBlue = Colour.fromHexString "97D5FC"

let fillDefinition = 
    {   FillDefinition.ColourScheme = 
            ColourScheme.AlternatingBetween (First = pink, Second = lightBlue) 
        Reordering = None 
        Modification = None 
        Noise = None }

let strokeDefinition = 
    {   (fillDefinition |> StrokeDefinition.fromFillDefinition) with 
            Width = StrokeWidthDefinition.ten 
            // Generate quite a bit of noise.
            Noise = Some Noise.More 
    }

let shapeSizeDefinition = 
    {   ShapeSizeDefinition.fullRangeRandom with 
            WidthRange = ShapeDimensionRange.fiftyAndAbove
            HeightsEqualWidths = true }

{   ShapeGrid.chessBoard with 
        // Use a specific random seed for every generation.
        RandomSeed = RandomSeed.fromInt 567
        Shape = Shape.RoundedRectanglePath
        ShapeSize = shapeSizeDefinition 
        Rotation = RotationDefinition.fourtyFivesRandom
        ColumnGap = 40.0 |> ColumnGap.fromFloat |> Some
        RowGap = 40.0 |> RowGap.fromFloat |> Some
        Fill = None
        Stroke = Some strokeDefinition 
} 
|> ShapeGrid.generate 
|> Svg.export SvgExportSettings.standard
|> fun svg -> File.WriteAllText(@"MyFirstDesign.svg", svg) 
```

Here you have added some noise to the stroke definition.

You have also set a new specific random seed by defining it with a number. By doing this you
are telling the pattern to always generate the same sequence(s) of random values which means that
you can choose different numbers to get a design which you like and can recreate it exactly by
specifying that same number again. (All of the ready-made patterns, by default, use a new random
seed randomly each time you generate the design.)

### Step 11 - Using A Different Grid Size

And now you want a different grid size? That's simple enough.

```fsharp
#r "nuget: QuickVectors.Export.FSharp"

open System.IO 
open QuickVectors.FSharp 
open QuickVectors.Patterns.FSharp 
open QuickVectors.Export.Svg.FSharp 

let pink = Colour.fromBytes 252uy 151uy 151uy 

let lightBlue = Colour.fromHexString "97D5FC"

let fillDefinition = 
    {   FillDefinition.ColourScheme = 
            ColourScheme.AlternatingBetween (First = pink, Second = lightBlue) 
        Reordering = None 
        Modification = None 
        Noise = None }

let strokeDefinition = 
    {   (fillDefinition |> StrokeDefinition.fromFillDefinition) with 
            Width = StrokeWidthDefinition.ten 
            Noise = Some Noise.More }

let shapeSizeDefinition = 
    {   ShapeSizeDefinition.fullRangeRandom with 
            WidthRange = ShapeDimensionRange.fiftyAndAbove
            HeightsEqualWidths = true }

{   ShapeGrid.chessBoard with 
        RandomSeed = RandomSeed.fromInt 567
        Shape = Shape.RoundedRectanglePath
        ShapeSize = shapeSizeDefinition 
        Rotation = RotationDefinition.fourtyFivesRandom
        // Change the grid to have six columns and ten rows.
        GridSize = GridSize.fromColumnsAndRows 6 10 
        ColumnGap = 40.0 |> ColumnGap.fromFloat |> Some
        RowGap = 40.0 |> RowGap.fromFloat |> Some
        Fill = None
        Stroke = Some strokeDefinition 
} 
|> ShapeGrid.generate 
|> Svg.export SvgExportSettings.standard
|> fun svg -> File.WriteAllText(@"MyFirstDesign.svg", svg) 
```

Here you have changed the grid size by speficying the number of columns and rows.

As with a lot of types, there are also a variety of ready-made values for you to use without specifying them manually.

## Step 12 - Adding An Offset 

What if you want to offset the grid a bit? That's easily done.

```fsharp
#r "nuget: QuickVectors.Export.FSharp"

open System.IO 
open QuickVectors.FSharp 
open QuickVectors.Patterns.FSharp 
open QuickVectors.Export.Svg.FSharp 

let pink = Colour.fromBytes 252uy 151uy 151uy 

let lightBlue = Colour.fromHexString "97D5FC"

let fillDefinition = 
    {   FillDefinition.ColourScheme = 
            ColourScheme.AlternatingBetween (First = pink, Second = lightBlue) 
        Reordering = None 
        Modification = None 
        Noise = None }

let strokeDefinition = 
    {   (fillDefinition |> StrokeDefinition.fromFillDefinition) with 
            Width = StrokeWidthDefinition.ten 
            Noise = Some Noise.More }

let shapeSizeDefinition = 
    {   ShapeSizeDefinition.fullRangeRandom with 
            WidthRange = ShapeDimensionRange.fiftyAndAbove
            HeightsEqualWidths = true }

{   ShapeGrid.chessBoard with 
        RandomSeed = RandomSeed.fromInt 567
        Shape = Shape.RoundedRectanglePath
        ShapeSize = shapeSizeDefinition 
        Rotation = RotationDefinition.fourtyFivesRandom
        GridSize = GridSize.fromColumnsAndRows 6 10 
        ColumnGap = 40.0 |> ColumnGap.fromFloat |> Some
        RowGap = 40.0 |> RowGap.fromFloat |> Some
        // Added a new alternating grid offset.
        GridOffset = 70.0 |> GridOffset.alternating |> Some
        Fill = None
        Stroke = Some strokeDefinition 
} 
|> ShapeGrid.generate 
|> Svg.export SvgExportSettings.standard
|> fun svg -> File.WriteAllText(@"MyFirstDesign.svg", svg) 
```

Here you have added a new alternating grid offset with a size of 70.0 (which, because the maximum size of the
shapes is 100.0 - as defined by `ShapeDimensionRange.maximum` - and the columns gap is 40.0, puts the shapes on the
even-numbered rows approximately in the middle of the gaps between the shapes on the odd-numbered rows (100.0 + 40.0) / 2.0 = 70.0).

> **Note:** The first row is row zero (even), the second row is row one (odd), etc. Same sort of thing for the columns.

As with some other fields, the grid offset field is an Option, so don't forget to use Some if you aren't using None.

## What Next

And I could go on and on for quite some time as there are lots of fields and lots of possibilities for each of them, but I won't.

It's time for you to start experimenting.

Try looking at some of the ready-made patterns and changing some field values to see how things work.

> **REMEMBER:** All of the values are validated and you cannot make or use an invalid value so it's all
safe to tinker with as much as you want.

Or you can try and make your own patterns from scratch; maybe try to recreate something you've seen elsewhere.

## Samples 

Sample designs are available which show you what the shapes, profiles, standard palettes, grid routes, and tessellators look like.

It is recommended that you look at the samples and keep them handy to refer to them as necessary.

The documentation [here](QuickVectors.Export.FSharp/900-Samples.md "How to generate the samples") in the `Export` package shows you how to generate the samples.