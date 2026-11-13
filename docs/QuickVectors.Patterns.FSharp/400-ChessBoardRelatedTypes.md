# QuickVectors.Patterns.FSharp

# Chess Board Related Types

These types let you define a chess board pattern.

- The [Chess Board Arrangement Type](#the-chess-board-arrangement-type)
- The [Chess Board Arrangement Module](#the-chess-board-arrangement-module)
    - [Construction](#construction) with [code examples](#chess-board-arrangement-creation-code-examples)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
- The [Chess Board Sizing Types](#the-chess-board-sizing-types) with [code examples](#chess-board-sizing-creation-code-examples)
- The [Chess Board Colour Way Type](#the-chess-board-colour-way-type)
- The [Chess Piece Colour Way Type](#the-chess-piece-colour-way-type)
- The [Chess Board Annotation Policy Type](#the-chess-board-annotation-policy-type)
- [Discriminated Union Identity Values](#discriminated-union-identity-values)
- [Exception-free Processing](#exception-free-processing)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Chess Board Arrangement Type

The `ChessBoardArrangement` **type** is a record which defines the arrangement of pieces on a chess board.

The fields are:

| Field Name                | Description                                                               |
| ------------------------- | ------------------------------------------------------------------------- | 
| **OriginalInput**         | The input which was provided to create the arrangement **1*               |
| **Pieces**                | A sequence containing the arrangement of pieces on the board              |

- **1*: For a randomly generated arrangement this string will state that the arrangement is random
and how many pieces there are.

## The Chess Board Arrangement Module

The `ChessBoardArrangement` **module** provides functionalities for working with chess board arrangements.

### Construction

You can only create an arrangement via the construction functions:

- `fromFen`: Creates an arrangement from a string which contains Forsyth–Edwards Notation;

    This function only looks at the part of the input string which preceeds the first space, the rest is ignored.

    See [here](https://en.wikipedia.org/wiki/Forsyth%E2%80%93Edwards_Notation) for information about Forsyth–Edwards Notation.

    The only validation performed is to check that the provided notation is correct; there is no validation for the 
    'right' number of pieces, or valid positions, or anything sophisticated like that.

    This function will raise an exception if it cannot understand the notation as provided but the information in
    the exception should help with figuring out what is wrong.

- `random`: Creates a new random chess board arrangement.

    A random arrangement will always contain one white king, one black king, and at least one other random piece
    (up to the number of pieces requested).

    This functionality is provided as a curiosity only as it is not guaranteed that the
    arrangement will be a valid board position (and they usually aren't). However, some randomly-generated boards
    might be of some limited use for training/puzzle positions.

    The pieces which are randomly chosen don't contain more than the number of each piece which a normal game would
    start with. For example, there may be up to two black knights but there won't be more than that.
    (You can think of it as randomly placing the two kings and then drawing pieces out of a bag and randomly placing
    each in turn with no thought about where they are being placed.)

### Chess Board Arrangement Creation Code Examples

```fsharp 
// Create from notation.
//
// The "w KQkq - 0 1" part is ignored as it has no relevance to the arrangment of pieces.
let startingPosition = 
    ChessBoardArrangement.fromFen "rnbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1" 

// Create random arrangement.
//
// Any Random can be used.
// In this case, the arrangement will consist of 16 pieces, two of which will be the kings.
// You cannot specify more the 32 pieces as that's how many pieces there are in a normal game.
let randomArrangement = 
    ChessBoardArrangement.random System.Random.Shared 16 
```

### Deconstruction

There is no provision to deconstruct an arrangement.

### Variations 

There is no provision to modify/vary an arrangement, to make a different one you need to make a new one.

## The Chess Board Sizing Types

Three chess board sizing types are provided which allow you to define the size of a chess board.

The `ChessSquareSize` **type** defines value which will be used to size the board by the size of the squares.

The `ChessBoardSize` **type** defines value which will be used to size the squares by the size of the board.

The `ChessBoardSizing` **type** defines a discriminated union which is either a `ChessSquareSize` or a `ChessBoardSize`.

You can define a `ChessBoardSizing` value manually but it is more convenient to use one of the provided convenience functions:

- `squareSize`: Creates a sizing which is defined by the size of each square;
- `boardSize`: Creates a sizing which is defined by the size of the board.

### Chess Board Sizing Creation Code Examples

```fsharp 
// The squares will each be 100x100. 
// The board will therefore be 800x800. 
let bySquareSize = ChessBoardSizing.squareSize 100.0 

// The board will be 1600x1600. 
// The squares will therefore each be 200x200. 
let byBoardSize = ChessBoardSizing.boardSize 1600.0 
```

The squares, and therefore the board, will always be square in shape - and of the size provided or calculated - but the board size will always be slightly smaller that the extents of the generated design. This allows you to re-generate the design with external annotations added or removed without needing to resize the exported file if used elsewhere.

## The Chess Board Colour Way Type

The `ChessBoardColourWay` **type** defines a discriminated union used to specify the colouring of the squares on a chess board.

The cases are:

| Case Name                         |
| --------------------------------- |
| **WhiteAndBlack**                 |
| **WhiteAndLightGrey**             |
| **WhiteAndMidGrey**               |
| **WhiteAndDarkGrey**              |
| **LightGreyAndDarkGrey**          |
| **LightGreyAndMidBlue**           |
| **LightPinkAndDarkPink**          |
| **CreamAndLightBrown**            |
| **LightOrangeAndDarkBrown**       |
| **LightBlueAndDarkBlue**          |
| **LightYellowAndMidGreen**        |

The first colour in the name is the colour of the white squares and the second colour, after "And", is the colour of the black squares.

To specify a chess board colour way simply supply its name, such as `ChessBoardColourWay.WhiteAndDarkGrey`.

These colour ways seem to cover most of the modern example boards that I have seen.

## The Chess Piece Colour Way Type

The `ChessPieceColourWay` **type** defines a discriminated union used to specify the colouring of the chess pieces.

The cases are:

| Case Name                             | Description                                                           |
| ------------------------------------- | --------------------------------------------------------------------- |
| **FilledOnly**                        | All pieces are filled but have no outline                             | 
| **OutlinedOnly**                      | All pieces have an outline but no fill                                |
| **FilledAndOppositeOutline**          | All pieces are filled and have an outline of the opposite colour      |
| **FilledAndWhiteWithBlackOutline**    | All pieces are filled and the white pieces have a black outline       |
| **FilledAndBlackWithWhiteOutline**    | All pieces are filled and the black pieces have a white outline       |

The pieces are coloured according to their type: white pieces are coloured white; black pieces are coloured black.

To specify a chess piece colour way simply supply its name, such as `ChessPieceColourWay.FilledAndOppositeOutline`.

These colour ways seem to cover most of the modern examples that I have seen.

## The Chess Board Annotation Policy Type

The `ChessBoardAnnotationPolicy` **type** defines a discriminated union used to specify whether/how the chess board is annotated.

The cases are:

| Case Name                             | Description                                                                                   |
| ------------------------------------- | --------------------------------------------------------------------------------------------- | 
| **NoAnnotation**                      | No annotations will be generated                                                              |
| **ExteriorLeftAndBottom**             | Ranks will be annotated on the left and files will be annotated at the bottom                 |
| **ExteriorLeftAndTop**                | Ranks will be annotated on the left and files will be annotated at the top                    |
| **ExteriorRightAndBottom**            | Ranks will be annotated on the right and files will be annotated at the bottom                |
| **ExteriorAllSides**                  | Ranks will be annotated on both sides and files will be annotated at the top and bottom       |
| **InteriorAllSquaresCentredBig**      | Each square will have its position annotated by large text in the centre of the square        |
| **InteriorAllSquaresTopLeft**         | Each square will have its position annotated by small text at its top left                    |

To specify a chess board annotation policy simply supply its name, such as `ChessBoardAnnotationPolicy.ExteriorLeftAndBottom`.

These annotation policies seem to cover most of the modern example boards that I have seen.

> **Note:** When exporting the design to SVG, some user agents (e.g. browsers, vector design applications) do not interpret the
SVG `dominant-baseline` text attribute properly, or at all, so the result might not look as it should. In these cases you may need
to manually manipulate the generated output yourself. (Most modern browsers do handle this property correctly so you can use them to
see what the design should look like.)

## Discriminated Union Identity Values

Functions are available for converting to and from POCO types and DU cases for some of the above types. 
See the [overview documentation](000-Overview.md "Package overview") for more information about these.

For the types described above there may not be a `defaultCase` value.

## Exception-free Processing

Exception-free processing versions - Option and Result - of some functions are available for some of the above types. 
See the [overview documentation](000-Overview.md "Package overview") for more information about these.

For the types described above there may not be a `FailSafe.fromInt` function and it is recommended
that you use the `Option.fromInt` function instead.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.