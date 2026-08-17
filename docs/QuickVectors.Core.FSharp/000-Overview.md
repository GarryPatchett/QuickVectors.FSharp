# QuickVectors.Core.FSharp 

## Contents

This document gives an overview of the QuickVectors.Core.FSharp package.
  
Please see the other related documentation for specific information about the different areas.

- [Overview](#overview)
- [Types and Modules](#types-and-modules)
- [Helpers](#helpers)
- [Discriminated Union Identity Values](#discriminated-union-identity-values)
- [Exception-free Processing](#exception-free-processing)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)
- [Dependencies](#dependencies)
- [Usage](#usage)

> **Note:** The words ***colour*** and ***grey*** in this package use the **British** spelling.

## Overview

This QuickVectors.Core.FSharp package contains the `QuickVectors.FSharp` **namespace** for F# developers
which provides some types and their related functions, and also some helper functions.

> **IMPORTANT:** There's not a lot that you can do with this package by itself and it is recommended that you install
the `QuickVectors.Export.FSharp` package instead which will install this package, and others, and allow you to
generate designs and export them.

For more information about the types, modules, and functions provided, links are provided below.

> **Note:** You can use IntelliSense in your code editor to get more information about each type and function.

To use the QuickVectors.FSharp packages it is expected that you have a basic knowledge of how to define
and use colours in an RGB colour space. If you need to know more about this then there are many resources
available on the web; just search for ***rgb color space*** to find lots of useful information.

> **IMPORTANT** To get the best from the other `QuickVectors.FSharp` packages you should understand the
types and modules implemented here as they are used extensively in those other packages.

All luminosities and colours are 8-bit, meaning that the value for a luminosity or a colour component
can be held in a single unsigned byte ( e.g. a value between 0 to 255, inclusive).

## Types and Modules

The types provided, with associated modules, are (in aphabetical order):

| Type/Module                   | Defines/Specifies                                                 |
| ----------------------------- | ----------------------------------------------------------------- |
| **[Colour](040-Colour.md "The Colour type and module")**                    | A colour in an 8-bit RGB colour space                             |
| **[ColourScheme](060-ColourScheme.md "The ColourScheme type and module")**              | How colours are chosen                                            |
| **[GridRoute](090-GridRoute.md "The GridRoute type and module")**                 | The route of a grid (how the cells will be visited)               |
| **[GridSize](100-GridSize.md "The GridSize type and module")**                  | The size of a grid                                                |
| **[Luminosity](030-Luminosity.md "The Luminosity type and module")**                | A colour component in an 8-bit RGB colour space                   |
| **[Palette](050-Palette.md "The Palette type and module")**                   | A selection of colours which can be used by some colour schemes   |
| **[PaneForm](130-PaneForm.md "The PaneForm type and module")**                  | The form of a pane pattern                                        |
| **[Profile](080-Profile.md "The Profile type and module")**                   | The 'shape' of the generated numerical values                     |
| **[RandomSeed](010-RandomSeed.md "The RandomSeed type and module")**                | A seed used to generate various things randomly                   |
| **[Range](070-Range.md "The Range type and module")**                     | A range of values                                                 |
| **[Shape](020-Shape.md "The Shape type and module")**                     | A shape which can be used in some patterns                        |
| **[StandardPalette](050-Palette.md "The StandardPalette type and module")**           | Some ready-made palettes                                          |
| **[Tessellator](110-Tessellator.md "The Tessellator type and module")**               | A tessellating shape which can be used in a tessellator pattern   |
| **[TessellatorShadingPolicy](120-TessellatorShadingPolicy.md "The TessellatorShadingPolicy type and module")**  | How/if shading will be applied to the colours                     |

## Helpers

Some modules exist which provide some helper functions which might be useful, and these are:

- `ByteHelpers` : Provides [functions](900-HelperModules.md "The helper modules") for manipulating byte values.

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

In general, but not always (as documented elsewhere), if there is no exception-free version of a function then
it can be assumed that the function will not raise an exception.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.

## Dependencies 

This package is dependent upon:
- `FSharp.Core` (which you will be using anyway);
- `QuickData.Core.FSharp` (for types such as Normal);
- `QuickData.Numbers.FSharp` (for generating sequences of numbers).

> **Notes:** 
>
> 1. This package will normally be automatically installed if you install any other QuickVectors.FSharp package, so you normally don't need to manually install this package yourself.
>
> 2. The QuickData.FSharp packages mentioned above will normally be automatically installed when you install this package so you normally don't need to manually install them yourself.

## Usage

The types and functions in this package have been designed to be used only with F#.

However, they may also be usable with C# but this has not been tested, so use them with C# at your own risk.