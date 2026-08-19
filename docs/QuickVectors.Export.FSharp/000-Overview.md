# QuickVectors.Export.FSharp 

## Contents

This document gives an overview of the QuickVectors.Export.FSharp package.  

- [Overview](#overview)
- [Types and Modules](#types-and-modules)
- [Samples](#samples)
- [Discriminated Union Identity Values](#discriminated-union-identity-values)
- [Exception-free Processing](#exception-free-processing)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)
- [Dependencies](#dependencies)
- [Usage](#usage)

> **Note:** The words ***colour*** and ***grey*** in this package use the **British** spelling.

## Overview

This QuickVectors.Export.FSharp package contains the `QuickVectors.Export.Svg.FSharp` **namespace** for F# developers
which provides some types and their related functions.

With the functionality in this package you can easily create an SVG (Scalable Vector Graphic) of a design
which was (usually) generated via the `QuickVectors.Patterns.FSharp` package.

For more information about the types, modules, and functions provided, please see the relevant documentation elsewhere.

> **Note:** You can use IntelliSense in your code editor to get more information about each type and function.

To use the QuickVectors.FSharp packages it is expected that you have a basic knowledge of how to define
and use colours in an RGB colour space. If you need to know more about this then there are many resources
available on the web; just search for ***rgb color space*** to find lots of useful information.

## Types and Modules

The types/modules provided are:

| Type/Module                                                                                           | Defines/Provides                                                  |
| ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| **[SvgExportTransformFormat](010-SvgExportSettings.md "The SvgExportTransformFormat type")**          | How the transformations in the SVG will be expressed              |
| **[SvgExportColourFormat](010-SvgExportSettings.md "The SvgExportColourFormat type")**                | How the colours in the SVG will be expressed                      |
| **[SvgExportInvisibilityPolicy](010-SvgExportSettings.md "The SvgExportInvisibilityPolicy type")**    | Whether invisible elements will be exported                       |
| **[Svg](100-ExportingToAnSvgFile.md "The Svg module")**                                               | The actual export functionality                                   |

> **Note:** There is no concept of a unit of measure in this package. All measurements can be considered to be of "as yet to be determined" units.

## Samples

Some sample designs are available which can be useful when you are learning what the various types define.

Instructions for generating these samples can be found [here](900-Samples.md "Sample designs").

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

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.

## Dependencies 

This package is dependent upon:
- `FSharp.Core` (which you will be using anyway);
- `QuickData.Core.FSharp` (for types such as Normal);
- `QuickData.Numbers.FSharp` (for generating sequences of numbers);
- `QuickVectors.Core.FSharp` (for various shared types and functionalities);
- `QuickVectors.Elements.FSharp` (for internal use).

> **Notes:** 
>
> 1. The QuickData.FSharp packages mentioned above will normally be automatically installed when you install this package so you normally don't need to manually install them yourself.
>
> 2. The QuickVectors.FSharp packages mentioned above will normally be automatically installed when you install this package so you normally don't need to manually install them yourself.

## Usage

The types and functions in this package have been designed to be used only with F#.

However, they may also be usable with C# but this has not been tested, so use them with C# at your own risk.