# QuickVectors.Patterns.FSharp

# Number Of Shapes

This type lets you specify the number of shapes to be generated in a pattern.

- The [Number Of Shapes Type](#the-number-of-shapes-type)
    - [Limits](#limits)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Number Of Shapes Type 

The `NumberOfShapes` **type** defines the number of shapes to be generated in some patterns.

### Limits

Some values are provided to give the limits of a number of shapes, and these are:

- `minimum` : Returns the minimum number of shapes - the lowest value that can be set;
- `maximum` : Returns the maximum number of shapes - the highest value that can be set.

For example, `NumberOfShapes.minimum` will return the minimum possible number of shapes.

These values can be useful in interactive environments where you need to set the limits for a control.

### Construction

A number of shapes can be created via the `fromInt` function.

The value will be clamped to the range `minimum` to `maximum` (inclusive).

When a number of shapes is printed to the screen the output will be `Shapes(n)` where `n` is the number of shapes.
For example, a number of shapes defined as 200 with `NumberOfShapes.fromInt 200` will be printed as `Shapes(200)`.

### Deconstruction

The internal number of shapes can be obtained via the `toInt` function.

### Variations

A number of shapes, once constructed, cannot be modified. If you need to use a different value then just create a new number of shapes.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.