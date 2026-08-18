# QuickVectors.Patterns.FSharp

# Scatter Area Shape

The shape of a scatter area.

- The [Scatter Area Shape Type](#the-scatter-area-shape-type)
- [Discriminated Union Identity Values](#discriminated-union-identity-values)
- [Exception-free Processing](#exception-free-processing)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Scatter Area Shape Type

The `ScatterAreaShape` **type** defines a discriminated union used to specify the shape of a scatter area.

The cases are (in alphabetical order):

| Case Name             | Description                               |
| --------------------- | ----------------------------------------- |
| **Elliptical**        | An elliptical area                        |
| **EllipticalRing**    | An elliptical area with a hole            |
| **Rectangular** **1*  | A rectangular area                        |

- **1* : The default case.

To specify a scatter area shape simply supply its name, such as `ScatterAreaShape.Rectangular`.

## Discriminated Union Identity Values

Functions are available for converting to and from POCO types and DU cases.
See the [overview documentation](000-Overview.md "Package overview") for more information about these.

## Exception-free Processing

Exception-free processing versions - FailSafe, Option, and Result - of some functions are available.
See the [overview documentation](000-Overview.md "Package overview") for more information about these.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.