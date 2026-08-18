# QuickVectors.Patterns.FSharp

# Boundary Dimension

This type lets you specify a dimension of a boundary.

- The [Boundary Dimension Size Type](#the-boundary-dimension-size-type)
    - [Limits](#limits)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Boundary Dimension Type 

The `BoundaryDimension` **type** defines a dimension of a boundary.

### Limits

Some values are provided to give the limits of a boundary dimension, and these are:

- `minimum` : Returns the minimum boundary dimension - the lowest value that can be set;
- `maximum` : Returns the maximum boundary dimension - the highest value that can be set.

For example, `BoundaryDimension.minimum` will return the minimum possible boundary dimension.

These values can be useful in interactive environments where you need to set the limits for a control.

### Construction

A boundary dimension can be created via the `fromFloat` function.

The value is a percentage and will be clamped to the range `minimum` to `maximum` (inclusive).

When a boundary dimension is printed to the screen the output will be `BoundaryDim(s)` where `s` is the boundary dimension.
For example, a boundary dimension defined as 400.0 with `BoundaryDimension.fromFloat 400.0` will be printed as `BoundaryDim(400.0)`.

### Deconstruction

The internal boundary dimension can be obtained via the `toFloat` function.

### Variations

A boundary dimension, once constructed, cannot be modified. If you need to use a different value then just create a new boundary dimension.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.