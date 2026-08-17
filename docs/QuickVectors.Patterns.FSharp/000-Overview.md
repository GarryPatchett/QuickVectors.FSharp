# QuickVectors.Patterns.FSharp 

## Contents

This document gives an overview of the QuickVectors.Patterns.FSharp package.

- [Overview](#overview)
- [Types and Modules](#types-and-modules)
- [Discriminated Union Identity Values](#discriminated-union-identity-values)
- [Exception-free Processing](#exception-free-processing)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)
- [Dependencies](#dependencies)
- [Usage](#usage)

> **Note:** The words ***colour*** and ***grey*** in this package use the **British** spelling.

## Overview

This QuickVectors.Patterns.FSharp package contains the `QuickVectors.Patterns.FSharp` **namespace** for F# developers
which provides some types and their related functions, and also some helper functions.

With the functionality in this package you can easily create patterns of vector shapes.

> **IMPORTANT:** While you can generate designs with this package you can't do much with them so it is recommended that you install
the `QuickVectors.Export.FSharp` package instead which will install this package, and others, and allow you to
generate designs and export them.

For more information about the types, modules, and functions provided, please see the relevant documentation elsewhere.

> **Note:** You can use IntelliSense in your code editor to get more information about each type and function.

To use the QuickVectors.FSharp packages it is expected that you have a basic knowledge of how to define
and use colours in an RGB colour space. If you need to know more about this then there are many resources
available on the web; just search for ***rgb color space*** to find lots of useful information.

> **IMPORTANT** To get the best from this package you should understand the types and modules implemented in the
`QuickVectors.Core.FSharp` package ([documentation here](../QuickVectors.Core.FSharp/000-Overview.md "Core Overview")) as they are used extensively here.

## Types and Modules

The shared types provided, with associated modules, are (in alphabetical order):

> **IMPORTANT:**
>
> 1. There are a lot of types to get to grips with here so it is recommended that you look at each pattern
in turn (see below), learning what each type does with each pattern. None of the individual types is particularly complicated individually
but they are easier to understand when looking at only one pattern at a time.
>
> 2. It is also highly recommended that you learn the types in the `Core` package before looking at the types here as the
`Core` types are fundamental to how the types in this package work.

The pattern types provided, with associated modules, are (in the recommended order of learning):

| Type/Module                                                                   | Produces                                                          |
| ----------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| **[ShapeGrid](500-ShapeGrid.md "The ShapeGrid type and module")**             | Shapes aligned to a grid                                          |
| **[Scatter](510-Scatter.md "The Scatter type and module")**                   | Shapes scattered across an area                                   |
| **[Tessellation](520-Tessellation.md "The Tessellation type and module")**    | Tessellating shapes                                               |
| **[Centric](530-Centric.md "The Centric type and module")**                   | Con**centric** shapes rotating around the same centre-point       |
| **[Pane](540-Pane.md "The Pane type and module")**                            | Shapes which cover an area (like a stained-glass window)          |

The associated/shared types are (in alhpabetical order):

| Type/Module                                                                                                               | Defines/Specifies                                             |
| ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| **[BoundaryDimension](090-BoundaryDimension.md "The BoundaryDimension type and module")**                                 | A dimension of a boundary                                     |
| **[BoundarySize](100-BoundarySize.md "The BoundarySize type and module")**                                                | The size of a boundary                                        |
| **[CentrePercentage](150-CentrePercentage.md "The CentrePercentage type and module")** **4*                               | Where the centre of the design will be                        |
| **[CentricRotationDefinition](390-CentricRotationDefinition.md "The CentricRotationDefinition type and module")** **1*    | How centrics will be rotated                                  |
| **[CentricSpacingDefinition](380-CentricSpacingDefinition.md "The CentricSpacingDefinition type and module")** **1*       | How centrics will be spaced                                   |
| **[ColourModification](020-ReorderingAndModification.md "The ColourModification type and module")**                       | How the generated colours might be further modified           |
| **[ColourReordering](020-ReorderingAndModification.md "The ColourReordering type and module")**                           | How the generated colours might be reordered                  |
| **[ColumnGap](040-Gaps.md "The ColumnGap type and module")**                                                              | The width of gaps between columns                             |
| **[FillDefinition](350-FillDefinition.md "The FillDefinition type and module")**                                          | The options for the shape fills                               |
| **[FrameDefinition](490-Frames.md "The FrameDefinition type and module")**                                                | The options for a frame                                       |
| **[FrameStrokeWidth](490-Frames.md "The FrameStrokeWidth type and module")**                                              | A stroke width for a frame                                    |
| **[GeometryDefinition](310-GeometryDefinition.md "The GeometryDefinition type and module")**                              | The options for shape geometries                              |
| **[GeometryModifierRange](010-Ranges.md "The GeometryModifierRange type and module")**                                    | A range of values for shape geometries                        |
| **[GridOffset](030-GridOffset.md "The GridOffset type and module")**                                                      | The offset of a grid                                          |
| **[IncrementalRotationAmount](130-IncrementalRotationAmount.md "The IncrementalRotationAmount type and module")** **1*    | An amount by which centrics can be rotated incrementally      |
| **[JigglePercentage](140-JigglePercentage.md "The JigglePercentage type and module")** **4*                               | How far the vertices can be from their 'natural' positions    |
| **[Noise](050-Noise.md "The Noise type and module")**                                                                     | A (semi-)natural noise used in various situations             |
| **[NumberOfCentrics](120-NumberOfCentrics.md "The NumberOfCentrics type and module")** **1*                               | The number of centrics to generate                            |
| **[NumberOfShapes](060-NumberOfShapes.md "The NumberOfShapes type and module")**                                          | The number of shapes to generate                              |
| **[NumberOfVerticesRange](010-Ranges.md "The NumberOfVerticesRange type and module")**                                    | A range of values for the number of vertices                  |
| **[RotationDefinition](320-RotationDefinition.md "The RotationDefinition type and module")**                              | The options for shape rotation                                |
| **[RotationModifierRange](010-Ranges.md "The RotationModifierRange type and module")**                                    | A range of values for shape rotation                          |
| **[RowGap](040-Gaps.md "The RowGap type and module")**                                                                    | The height of gaps between rows                               |
| **[ScatterAreaDefinition](370-ScatterAreaDefinition.md "The ScatterAreaDefinition type and module")** **2*                | The options for a scatter area                                |
| **[ScatterAreaShape](070-ScatterAreaShape.md "The ScatterAreaShape type and module")** **2*                               | The shape of a scatter area                                   |
| **[ScatterHoleSize](080-ScatterHoleSize.md "The ScatterHoleSize type and module")** **2*                                  | The size of a hole in a scatter area                          |
| **[SequenceReordering](020-ReorderingAndModification.md "The SequenceReordering type and module")**                       | How the generated values might be reordered                   |
| **[ShapeDimensionRange](010-Ranges.md "The ShapeDimensionRange type and module")**                                        | A range of values for the dimension of a shape                |
| **[ShapeSizeDefinition](300-ShapeSizeDefinition.md "The ShapeSizeDefinition type and module")**                           | The options for shape sizes                                   |
| **[SideLength](110-SideLength.md "The SideLength type and module")** **3*                                                 | The length of a side                                          |
| **[SpreadRotationRange](010-Ranges.md "The SpreadRotationRange type and module")** **1*                                   | A range of values defining how centrics can be rotated        |
| **[StrokeDefinition](360-StrokeDefinition.md "The StrokeDefinition type and module")**                                    | The options for the shape strokes                             |
| **[StrokeWidthDefinition](340-StrokeWidthDefinition.md "The StrokeWidthDefinition type and module")**                     | The options for the widths of shape strokes                   |
| **[StrokeWidthRange](010-Ranges.md "The StrokeWidthRange type and module")**                                              | A range of values for the stroke widths                       |
| **[ValueModification](020-ReorderingAndModification.md "The ValueModification type and module")**                         | How the generated values might be further modified            |
| **[VerticesDefinition](330-VerticesDefinition.md "The VerticesDefinition type and module")**                              | The options for the number of vertices                        |

- **1* : Only relevant to Centric patterns.
- **2* : Only relevant to Scatter patterns.
- **3* : Only relevant to Tessellation patterns.
- **4* : Only relevant to Pane patterns.

Some of the above types are not used/appropriate in all patterns.

> **Note:** There is no concept of a unit of measure in this package.
All measurements can be considered to be of "as yet to be determined" units and all sizes,
stroke widths, etc. use the same unit of measure.

> **IMPORTANT:** The origin of all patterns is at 0,0 which is at the top-left with positive horizontal
values going right and positive vertical values going downwards. However, some patterns in some circumstances
may be extend beyond the origin to the left and/or above the top.

## Discriminated Union Identity Values

In all of the QuickVectors.FSharp packages, where a discriminated union exists to specify a parameter for a function,
there often will be two functions related to that discriminated union which return an integer identity value from the union
case - `toInt` - or return a union case from an integer identity value - `fromInt`.

These can be useful if you need to store a value in a data structure which does not cater for 
discriminated unions, e.g. in a file, in JSON, etc.

The `toInt` function will always return a valid identity value.

> **Notes:** 
>
> 1. Where a `fromInt` function exists there often will be [exception-free versions](#exception-free-processing) available.
>
> 2. All valid identity values are in the range 100 to 999 (inclusive). Any value which has fewer,
or more, than three digits can be immediately identified as being invalid, but not all three-digit values are valid.
> 3. While identity values are unique within a discriminated union, some identity values may be shared by cases
in different discriminated unions but no functional equality or relationship between the two should be inferred.
Identity values will not change unless specifically mentioned in the release notes.

The `defaultCase` value (where available) contains the default case for the discriminated union.

The `allCases` value (where available) contains a list of all of the cases for the discriminated union.

The `displayName` function (where available) will produce a string description of the specified DU case.

Where the above differs for a particular type it will be noted in the documentation for that type.

## Exception-free Processing

In all of the QuickVectors.FSharp packages, some functions will raise an exception if the internal processing fails
for some reason or if the input was not as expected.

Many of this type of function will also have alternative exception-free versions which do not
raise an exception.

These alternative functions are:
- `<module-name>.FailSafe.<function-name>`
    : Returns a default value, instead of raising an exception;
- `<module-name>.Option.<function-name>`
    : Returns `None` instead of raising an exception, otherwise `Some value`;
- `<module-name>.Result.<function-name>`
    : Returns `Error <error-type>` instead of raising an exception, otherwise `Ok value`.

In general, if there is no exception-free version of a function then it can be assumed that the function will not raise an exception.

Where the above differs for a particular type it will be noted in the documentation for that type.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.

## Dependencies 

This package is dependent upon:
- `FSharp.Core` (which you will be using anyway);
- `QuickData.Core.FSharp` (for types such as Normal);
- `QuickData.Numbers.FSharp` (for generating sequences of numbers);
- `QuickVectors.Core.FSharp` (for various shared types and functionalities);
- `QuickVectors.Elements.FSharp`(for internal use).

> **Notes:** 
>
> 1. The QuickData.FSharp packages mentioned above will normally be automatically installed when you install this package so you normally don't need to manually install them yourself.
>
> 2. The QuickVectors.FSharp packages mentioned above will normally be automatically installed when you install this package so you normally don't need to manually install them yourself.

## Usage

The types and functions in this package have been designed to be used only with F#.

However, they may also be usable with C# but this has not been tested, so use them with C# at your own risk.