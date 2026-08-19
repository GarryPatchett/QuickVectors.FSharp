# QuickVectors.Export.Svg.FSharp

# Exporting To An SVG File

- The [Svg Module](#the-svg-module)
- A [Basic Example](#basic-example) of how to use the functionality
- A [Custom Example](#custom-example) showing a different way to use it
- [Compiling a Design](#compiling-a-design)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Svg Module

The `Svg` **module** defines a function `export` with which you can create an SVG from a generated design.

Once you have exported you will have a string containing the SVG text as defined by the settings supplied.

Once you have the SVG text you can do anything you like with it - it's just a string - but it is usual to save it to a file.

While you are experimenting with design possibilities it would be useful if you can see the results immediately.
You can do this by placing the first exported file into a graphics application which can automatically check that
a file has been changed and update the display accordingly. Then, each time you re-generate/export the file, you will
see the results. Alternatively you can view the file in a web browser and refresh the page as necessary.

### Basic Example 

Here's a basic example of exporting one of the ready-made designs to an SVG with the standard settings and then saving the SVG to a file.

```fsharp 
open System.IO // Required for the File functionality.
open QuickVectors.Patterns.FSharp // Required for generating the design.
open QuickVectors.Export.Svg.FSharp // Required for exporting.

ShapeGrid.brickWall // A ready-made design.
|> ShapeGrid.generate // Generate the design.
|> Svg.export SvgExportSettings.standard // Create the SVG text.
|> fun svg -> File.WriteAllText("BrickWall.svg", svg) // Save to file.
```

### Custom Example

Here's an example of exporting a custom-defined design to an SVG with custom export settings and then saving the SVG to a file.

```fsharp 
open System.IO // Required for the File functionality.
open QuickVectors.FSharp // Required for customisation.
open QuickVectors.Patterns.FSharp // Required for generating the design.
open QuickVectors.Export.Svg.FSharp // Required for exporting.

let exportSettings = 
    {   SvgExportSettings.ColourFormat = ExportColoursAsHex
        TransformFormat = MatrixTransform
        InvisibilityPolicy = ExportInvisibleElements } 

let custom = 
    {   ShapeGrid.RandomSeed = RandomSeed.generate()
        Shape = Rectellipse
        ShapeSize = 
            { ShapeSizeDefinition.WidthRange = ShapeDimensionRange.fiftyAndAbove
              WidthProfile = Profile.CosineWave
              WidthReordering = Some SequenceReordering.SortedAscending
              WidthModification = None 
              HeightsEqualWidths = false
              HeightRange = ShapeDimensionRange.fiftyAndAbove
              HeightProfile = Profile.Random
              HeightReordering = Some SequenceReordering.SortedDescending
              HeightModification = None }
        Geometry = GeometryDefinition.fromFloats 20.0 40.0
        Rotation = RotationDefinition.fromFloats -40.0 40.0 
        Vertices = VerticesDefinition.pentToDecRandom 
        GridSize = GridSize.fromColumnsAndRows 20 20 
        GridRoute = GridRoute.Cascade
        ColumnGap = Some (ColumnGap.fromFloat 14.0) 
        RowGap = Some (RowGap.fromFloat 14.0) 
        GridOffset = Some (GridOffset.alternating 50.0)
        Fill = StandardPalette.Nature.forestBerries
               |> ColourScheme.RandomFromPalette
               |> FillDefinition.fromColourScheme 
               |> Some
        Stroke = None
        BoundaryFrame = None 
        ExtentsFrame = None }

custom
|> ShapeGrid.generate 
|> Svg.export exportSettings
|> fun svg -> File.WriteAllText("CustomDesign.svg", svg) 
```

See the relevant documentation elsewhere for information about how to specify a custom design and the options available.

### Compiling a Design

Alternatively, you can create an array of string, with each element being a different part of the SVG design via
the `Svg.compile` function (same parameters as the `export` function).

You would not normally need to do this but you might find it useful if you want to manipulate the elements further before
saving the design to a file.

The compiled string array cannot be passed to the `export` function; once you have compiled the design to a collection 
of strings it's your responsibility.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.