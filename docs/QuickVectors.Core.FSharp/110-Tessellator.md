# QuickVectors.Core.FSharp

# Tessellator

Defines a tessellating shape which can be used in a tessellation pattern.

- The [Tessellator Type](#the-tessellator-type)
- [Discriminated Union Identity Values](#discriminated-union-identity-values)
- [Exception-free Processing](#exception-free-processing)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Tessellator Type

The `Tessellator` **type** defines a discriminated union used to specify the tessellating shape in a tessellation pattern.

The cases are (in aphabetical order):

| Case Name                     | Description                                                           |
| ----------------------------- | --------------------------------------------------------------------- | 
| **Crystals**                  | Like tall and thin hexagons                                           | 
| **Diamonds** **1*             | Squares rotated by fourty-five degrees                                |
| **Hexagons**                  | Just simple hexagons                                                  |
| **Isocubes** **2*             | Three quadrilaterals which together look like an isometric cube       | 
| **Kites** **3*                | Two kite shapes, like stretched diamonds                              | 
| **Octodiamonds** **3*         | An octagon with a diamond attached to one 'corner'                    | 
| **RectangularWeave** **3*     | Two rotated rectangles                                                | 
| **Triangles** **3*            | Two equilateral triangles                                             | 

- **1* : The default case.
- **2* : Comprised of three shapes; shading is applicable.
- **3* : Comprised of two shapes; shading is applicable.

To specify a tessellator simply supply its name, such as `Tessellator.Hexagons`.

## Discriminated Union Identity Values

Functions are available for converting to and from POCO types and DU cases.
See the Overview documentation for more information about these.

## Exception-free Processing

Exception-free processing versions - FailSafe, Option, and Result - of some functions are available.
See the Overview documentation for more information about these.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp)* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.
