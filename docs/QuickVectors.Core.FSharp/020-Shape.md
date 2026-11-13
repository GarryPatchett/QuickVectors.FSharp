# QuickVectors.Core.FSharp

# Shape

Defines a shape which can be used in some patterns.

- The [Shape Construction Type](#the-shape-construction-type)
- The [Shape Type](#the-shape-type)
- The [Rectangle Type](#the-rectangle-type)
- The [Ellipse Type](#the-ellipse-type)
- The [Polygon Type](#the-polygon-type)
- The [Radial Type](#the-radial-type)
- The [Quadripartite Type](#the-quadripartite-type)
- The [Item Type](#the-item-type)
- The [Creature Type](#the-creature-type)
- The [Binary Type](#the-binary-type)
- The [CardSuit Type](#the-cardsuit-type)
- The [ChessPiece Type](#the-chesspiece-type)
- The [Linear Type](#the-linear-type)
- [Discriminated Union Identity Values](#discriminated-union-identity-values)
- [Exception-free Processing](#exception-free-processing)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

> **VERY IMPORTANT:** The method by which you specify a shape changed considerably from 0.3.0 to 0.3.2. Please make
sure that you use the new method as the old method will no longer work.

You can see visual examples of the shapes [here](images/Shape-Examples.png "Visual roll call of the available shapes").

## The Shape Construction Type

The `ShapeConstruction` **type** defines a discriminated union used to specify how some shapes are constructed.

The cases are:

| Case Name         | Description                                           |
| ----------------- | ----------------------------------------------------- | 
| **AsElement**     | Construct the shape via a specific element type       |
| **AsPath**        | Construct the shape via a path                        |

This type is only used for some shapes, as noted below.

The `AsElement` case will construct the shape from a specific element which is relevant to that shape.
For example, a rectangle will be constructed from a rectangle rather than a path containing linear segments which
make a rectangle.

The `AsPath` case will construct the shape from a path containing segments. This is the the only case for most shapes
and in these circumstances the construction modifier cannot be specified.

## The Shape Type

The `Shape` **type** defines a discriminated union used to specify a shape.

The cases are:

| Case Name                 | Field Type                                | Description                                                       |
| ------------------------- | ----------------------------------------- | ----------------------------------------------------------------- | 
| **Rectangle**             | [Rectangle](#the-rectangle-type)          | Shapes which are based on a rectangle, or square                  |
| **Ellipse**               | [Ellipse](#the-ellipse-type)              | Shapes which are based on an ellipse, or circle                   |
| **Polygon**               | [Polygon](#the-polygon-type)              | Shapes with multiple vertices, each joined by a straight line     |
| **Radial**                | [Radial](#the-radial-type)                | Shapes with multiple vertices                                     |
| **Quadripartite**         | [Quadripartite](#the-quadripartite-type)  | Shapes with four parts                                            |
| **Item**                  | [Item](#the-item-type)                    | Shapes which look like an object                                  |
| **Creature**              | [Creature](#the-creature-type)            | Shapes which look like a creature                                 |
| **Binary**                | [Binary](#the-binary-type)                | Shapes which signify yes/no, good/bad, right/wrong, etc.          |
| **CardSuit**              | [CardSuit](#the-cardsuit-type)            | Shapes which depict standard playing card suits                   |
| **ChessPiece**            | [ChessPiece](#the-chesspiece-type)        | Shapes which depict standard chess pieces                         |
| **Linear**                | [Linear](#the-linear-type)                | Shapes which are made from lines without a fill                   |

## The Rectangle Type

The `Rectangle` **type** defines a discriminated union used to specify a rectangle shape.

Rectangle shapes are those which are based on a rectangular form.

The cases are:

| Case Name         | Modifier Field Type                                   | Description                                                                                           |
| ----------------- | ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | 
| **Standard**      | [ShapeConstruction](#the-shape-construction-type)     | A standard rectangle (or square) with sharp corners                                                   |
| **Rounded**       | [ShapeConstruction](#the-shape-construction-type)     | A rectangle (or square) with rounded corners                                                          |
| **Rectellipse**   | None                                                  | A rectangle (or square) with corners which have been rounded in a specific way                        |
| **Ring**          | None                                                  | A pair of non-rounded rectangles, one normally larger than the other, which have the same centre      |

There are lots of ways to specify a rectangle shape and some of those are as follows:

```fsharp 
ShapeConstruction.AsElement |> Rectangle.Standard |> Shape.Rectangle 
// or 
Rectangle (Rectangle.Standard AsElement)
// or 
AsElement |> Rectangle.Standard |> Rectangle 
// or 
Rectangle.Standard <| AsElement |> Rectangle // Note the backward pipe operator.
// or 
Rectangle.Rectellipse |> Rectangle // No construction modifier for this shape. 
/// etc.
```

(As you might have noticed, these are just different ways to assign field values to DUs as you might normally do.)

You can choose whichever method suits your purposes/preferences.

Ready-made values for all possibilities are also available via the `Shape.Rectangle` **module**,
e.g. `Shape.Rectangle.standardAsElement`.

> **Note:** Some applications don't parse/draw the rounded rectangle as element shape properly (the radii aren't correctly
interpreted, or are ignored completely). In these cases you can try using the rounded rectangle as **path** shape instead.

## The Ellipse Type

The `Ellipse` **type** defines a discriminated union used to specify an ellipse shape.

Ellipse shapes are those which are based on a generally elliptical form.

The cases are:

| Case Name         | Modifier Field Type                                   | Description                                                                                           |
| ----------------- | ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | 
| **Standard**      | [ShapeConstruction](#the-shape-construction-type)     | A standard ellipse (or circle)                                                                        |
| **Ring**          | None                                                  | A pair of ellipses (or circles), one normally larger than the other, which have the same centre       |

There are lots of ways to specify an ellipse shape and some of those are as follows:

```fsharp 
ShapeConstruction.AsElement |> Ellipse.Standard |> Shape.Ellipse 
// or 
Ellipse (Ellipse.Standard AsElement)
// or 
AsElement |> Ellipse.Standard |> Ellipse 
// or 
Ellipse.Standard <| AsElement |> Ellipse // Note the backward pipe operator.
// or 
Ellipse.Ring |> Ellipse // No construction modifier for this shape. 
/// etc.
```

(As you might have noticed, these are just different ways to assign field values to DUs as you might normally do.)

You can choose whichever method suits your purposes/preferences.

Ready-made values for all possibilities are also available via the `Shape.Ellipse` **module**,
e.g. `Shape.Ellipse.standardAsElement`.

## The Polygon Type

The `Polygon` **type** defines a discriminated union used to specify a polygon shape.

Polygon shapes are, generally, those which are based on radial vertices which are evenly spaced.

The cases are:

| Case Name                 | Modifier Field Type   | Description                                                           |
| ------------------------- | --------------------- | --------------------------------------------------------------------- | 
| **Regular**               | None                  | A regular polygon                                                     |
| **ShuffledVertices**      | None                  | A polygon made from the shuffled vertices of a regular polygon        |
| **RandomVertices**        | None                  | A polygon made from random vertex positions                           |
| **RandomQuadrilateral**   | None                  | A four-sided polygon with vertices randomly placed                    |

There are various ways to specify a polygon shape and some of those are as follows:

```fsharp 
Polygon.Regular |> Shape.Polygon 
// or 
Shape.Polygon Regular 
/// etc.
```

(As you might have noticed, these are just different ways to assign field values to DUs as you might normally do.)

You can choose whichever method suits your purposes/preferences.

Ready-made values for all possibilities are also available via the `Shape.Polygon` **module**,
e.g. `Shape.Polygon.regular`.

> **Note:** It's possible, but unlikely, that a random quadrilateral will look like it's not there because the offsets
generated make the sides overlap. In thses rare cases just generate the design again if necessary.

## The Radial Type

The `Radial` **type** defines a discriminated union used to specify a radial shape.

Radial shapes are those which are based on radial vertices which are evenly spaced.

The cases are:

| Case Name             | Modifier Field Type   | Description                                                           |
| --------------------- | --------------------- | --------------------------------------------------------------------- | 
| **Star**              | None                  | A pointed star                                                        |
| **DoubleStar**        | None                  | A large star combined with a smaller star                             |
| **Flower**            | None                  | A shape with rounded 'petals'                                         |
| **Spikey**            | None                  | A shape made from spikes                                              |
| **Blob**              | None                  | An amorphous shape with randomly drawn curves                         |
| **Squiggle**          | None                  | A wildly-amorphous shape with randomly drawn curves                   |

There are various ways to specify a radial shape and some of those are as follows:

```fsharp 
Radial.Star |> Shape.Polygon 
// or 
Shape.Radial Star 
/// etc.
```

(As you might have noticed, these are just different ways to assign field values to DUs as you might normally do.)

You can choose whichever method suits your purposes/preferences.

Ready-made values for all possibilities are also available via the `Shape.Radial` **module**,
e.g. `Shape.Radial.doubleStar`.

> **Note:** The starting vertex of these shapes is always at, or aligned to, the top-centre (before rotation).
Also, the `Blob` and `Squiggle` shapes can sometime produce some very strange results. Try generating the design again until
you get something you like.

## The Quadripartite Type

The `Quadripartite` **type** defines a discriminated union used to specify a quadripartite shape.

Quadripartite shapes are those which have four parts.

The cases are:

| Case Name             | Modifier Field Type   | Description                                                               |
| --------------------- | --------------------- | ------------------------------------------------------------------------- | 
| **Quaternate**        | None                  | A symmetrical shape made from four 'pointy leaves'                        |
| **Quatrefoil**        | None                  | A symmetrical shape made from four 'overlapping circles'                  |
| **Plus**              | None                  | A shape which looks like a plus sign, or a vertically-aligned cross       |

There are various ways to specify a quadripartite shape and some of those are as follows:

```fsharp 
Quadripartite.Plus |> Shape.Quadripartite 
// or 
Shape.Quadripartite Quadripartite.Plus 
/// etc.
```

(As you might have noticed, these are just different ways to assign field values to DUs as you might normally do.)

You can choose whichever method suits your purposes/preferences.

Ready-made values for all possibilities are also available via the `Shape.Quadripartite` **module**,
e.g. `Shape.Quadripartite.quaternate`.

## The Item Type

The `Item` **type** defines a discriminated union used to specify an item shape.

Item shapes are those which look like an item which you could see or pick up.

The cases are:

| Case Name             | Modifier Field Type   | Description                   |
| --------------------- | --------------------- | ----------------------------- | 
| **Heart**             | None                  | A heart                       |
| **Egg**               | None                  | An egg                        |
| **Gemstone**          | None                  | A gemstone                    |
| **Cloud**             | None                  | A cartoon cloud               |

There are various ways to specify an item shape and some of those are as follows:

```fsharp 
Item.Heart |> Shape.Item 
// or 
Shape.Item Item.Heart 
/// etc.
```

(As you might have noticed, these are just different ways to assign field values to DUs as you might normally do.)

You can choose whichever method suits your purposes/preferences.

Ready-made values for all possibilities are also available via the `Shape.Item` **module**,
e.g. `Shape.Item.gemstone`.

## The Creature Type

The `Creature` **type** defines a discriminated union used to specify a creature shape.

Creature shapes are those which look like a animal or other creature.

The cases are:

| Case Name             | Modifier Field Type   | Description                   |
| --------------------- | --------------------- | ----------------------------- | 
| **Alien**             | None                  | An alien's head               |
| **Ghost**             | None                  | A spooky ghost                |

There are various ways to specify an item shape and some of those are as follows:

```fsharp 
Creature.Alien |> Shape.Creature 
// or 
Shape.Creature Alien 
/// etc.
```

(As you might have noticed, these are just different ways to assign field values to DUs as you might normally do.)

You can choose whichever method suits your purposes/preferences.

Ready-made values for all possibilities are also available via the `Shape.Creature` **module**,
e.g. `Shape.Creature.ghost`.

## The Binary Type

The `Binary` **type** defines a discriminated union used to specify a binary shape.

Binary shapes are those which are of a binary nature, e.g. on/off, yes/no, right/wrong, etc.

The cases are:

| Case Name             | Modifier Field Type   | Description                   |
| --------------------- | --------------------- | ----------------------------- | 
| **Correct**           | None                  | A tick mark                   |
| **Incorrect**         | None                  | A cross mark                  |

There are various ways to specify a creature shape and some of those are as follows:

```fsharp 
Binary.Correct |> Shape.Binary 
// or 
Shape.Binary Correct 
/// etc.
```

(As you might have noticed, these are just different ways to assign field values to DUs as you might normally do.)

You can choose whichever method suits your purposes/preferences.

Ready-made values for all possibilities are also available via the `Shape.Binary` **module**,
e.g. `Shape.Binary.incorrect`.

## The CardSuit Type

The `CardSuit` **type** defines a discriminated union used to specify a card suit shape.

Card suit shapes are those which you would see on a standard set of playing cards.

The cases are:

| Case Name             | Modifier Field Type   | Description                   |
| --------------------- | --------------------- | ----------------------------- | 
| **Spades**            | None                  | The spades suit               |
| **Clubs**             | None                  | The clubs suit                |
| **Hearts**            | None                  | The hearts suit               |
| **Diamonds**          | None                  | The diamonds suit             |
| **Random**            | None                  | A randomly-chosen suit        |

There are various ways to specify a card suit shape and some of those are as follows:

```fsharp 
CardSuit.Spades |> Shape.CardSuit 
// or 
Shape.CardSuit Spades 
/// etc.
```

(As you might have noticed, these are just different ways to assign field values to DUs as you might normally do.)

You can choose whichever method suits your purposes/preferences.

Ready-made values for all possibilities are also available via the `Shape.CardSuit` **module**,
e.g. `Shape.CardSuit.hearts`.

> **Note:** When a random suit is chosen, the generated fill colour will be overridden with the standard
suit colour (e.g. Clubs = Black, Hearts = Red, etc.).

## The ChessPiece Type

The `ChessPiece` **type** defines a discriminated union used to specify a chess piece shape.

Chess piece shapes are those which look like a standard chess piece.

The cases are:

| Case Name             | Modifier Field Type   | Description                       |
| --------------------- | --------------------- | --------------------------------- | 
| **Pawn**              | None                  | A pawn                            |
| **Knight**            | None                  | A knight                          |
| **Bishop**            | None                  | A bishop                          |
| **Rook**              | None                  | A rook                            |
| **Queen**             | None                  | A queen                           |
| **King**              | None                  | A king                            |
| **Random**            | None                  | A randomly-chosen chess piece     |

There are various ways to specify a chess piece shape and some of those are as follows:

```fsharp 
ChessPiece.Pawn |> Shape.ChessPiece
// or 
Shape.ChessPiece Pawn
/// etc.
```

(As you might have noticed, these are just different ways to assign field values to DUs as you might normally do.)

You can choose whichever method suits your purposes/preferences.

Ready-made values for all possibilities are also available via the `Shape.ChessPiece` **module**,
e.g. `Shape.ChessPiece.rook`.

> **Note:** These chess piece shapes are sized so that they look right in the chess board pattern so, for example,
a pawn with a height of 100 will look smaller than a queen with a height of 100.

## The Linear Type

The `Linear` **type** defines a discriminated union used to specify a linear shape.

Linear shapes are those which are made from one or more straight lines and which have no fill.

The cases are:

| Case Name             | Modifier Field Type                                   | Description                                                           |
| --------------------- | ----------------------------------------------------- | --------------------------------------------------------------------- | 
| **Plus**              | None                                                  | Two lines in the form of a plus sign                                  |
| **Cross**             | None                                                  | Two lines in the form of a cross or multiplication sign               |
| **Horizontal**        | [ShapeConstruction](#the-shape-construction-type)     | A single horizontal line                                              |
| **Vertical**          | [ShapeConstruction](#the-shape-construction-type)     | A single vertical line                                                |

There are various ways to specify a linear shape and some of those are as follows:

```fsharp 
ShapeConstruction.AsElement |> Linear.Horizontal |> Shape.Linear 
// or 
Linear (Linear.Horizontal AsElement)
// or 
AsElement |> Linear.Horizontal |> Linear 
// or 
Linear.Horizontal <| AsElement |> Linear // Note the backward pipe operator.
// or 
Linear.Plus |> Linear // No construction modifier for this shape. 
/// etc.
```

(As you might have noticed, these are just different ways to assign field values to DUs as you might normally do.)

You can choose whichever method suits your purposes/preferences.

Ready-made values for all possibilities are also available via the `Shape.Linear` **module**,
e.g. `Shape.Linear.cross`.

## Discriminated Union Identity Values

Functions are available for converting to and from POCO types and DU cases **for the Shape type only**.
See the [overview documentation](000-Overview.md "Package overview") for more information about these.

The default shape case is the standard rectangle as an element.

## Exception-free Processing

Exception-free processing versions - FailSafe, Option, and Result - of some functions are available.
See the [overview documentation](000-Overview.md "Package overview") for more information about these.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.