# QuickVectors.Core.FSharp

# Shape

Defines a shape which can be used in some types of pattern.

- The [Shape Type](#the-shape-type)
- [Discriminated Union Identity Values](#discriminated-union-identity-values)
- [Exception-free Processing](#exception-free-processing)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Shape Type

The `Shape` **type** defines a discriminated union used to specify the shape.

The cases are:

| Case Name                     | Description                                                                                                   |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------- | 
| **Rectangle**                 | A basic rectangle, or square if the width and height are equal                                                |
| **RectanglePath**             | A basic rectangle drawn with a path rather than a shape                                                       |
| **RectangleRing**             | A rectangle with a rectangular hole in it                                                                     |
| **RoundedRectangle** **1*     | A rectangle with rounded corners                                                                              |
| **RoundedRectanglePath**      | A rectangle with rounded corners, drawn with a path                                                           |
| **Rectellipse**               | A cross between a rectangle and an ellipse. Sometimes called a squircle                                       |
| **Ellipse**                   | A basic ellipse, or circle if the width and height are equal                                                  |
| **EllipsePath**               | A basic ellipse drawn with a path rather than a shape                                                         |
| **EllipseRing**               | An ellipse with an elliptical hole in it                                                                      |
| **RegularPolygon** **2*       | A regular polygon                                                                                             |
| **ShuffledPolygon**           | A polygon where the order in which the vertices are drawn has been randomly shuffled                          |
| **RandomPolygon**             | A polygon where the vertices positions have been randomly positioned around the circumference                 |
| **Star** **2*                 | A basic star                                                                                                  |
| **DoubleStar** **2*           | A small star 'joined with' a larger star                                                                      |
| **Flower** **2*               | A flower with rounded 'petals'                                                                                |
| **Spikey** **2*               | A shape with spikes                                                                                           |
| **Blob** **3*                 | An amorphous shape with curves drawn randomly through regular polygon vertices                                |
| **Squiggle** **3*             | A wildly-amorphous shape with curves drawn randomly through regular ploygon vertices                          |
| **RandomQuadrilateral** **4*  | A quadrilateral where the corners are positioned randomly                                                     |
| **Quaternate**                | A symmetrical shape made from four 'pointy leaves'                                                            |
| **Quatrefoil**                | A symmetrical shape made from four overlapping circles                                                        |
| **Plus**                      | A shape which looks like a wide plus sign                                                                     |
| **Heart**                     | A heart                                                                                                       |
| **Egg**                       | An egg                                                                                                        |
| **LinePlus**                  | Two lines in the form of a plus sign                                                                          |
| **LineCross**                 | Two lines in the form of a cross or multiplication sign                                                       |
| **HorizontalLine**            | A horizontal line                                                                                             |
| **HorizontalLinePath**        | A horizontal line drawn with a path rather than a line                                                        |
| **VerticalLine**              | A vertical line                                                                                               |
| **VerticalLinePath**          | A vertical line drawn with a path rather than a line                                                          |

- **1* : Some applications don't parse/draw the RoundedRectangle shape properly (they seem to ignore the radii).
In these cases you can try using the RoundedRectangle*Path* shape instead.
- **2* : The starting vertex/position of these shapes is always at, or aligned to, the top-centre (before rotation).
- **3* : These shapes can sometime produce some very strange results. Try generating the design again until
you get something you like.
- **4* : It's possible, but unlikely, that a RandomQuadrilateral will look like it's not there because the offsets
used make the sides overlap. In thses rare cases just generate the design again if necessary.

To specify a shape simply supply its name, such as `Shape.Rectangle`.

You can see visual examples of the different shapes [here](https://github.com/GarryPatchett/QuickVectors.FSharp/blob/main/docs/QuickVectors.Core.FSharp/images/Shape-Examples.png).

## Discriminated Union Identity Values

Functions are available for converting to and from POCO types and DU cases.
See the Overview documentation for more information about these.

## Exception-free Processing

Exception-free processing versions - FailSafe, Option, and Result - of some functions are available.
See the Overview documentation for more information about these.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp)* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.
