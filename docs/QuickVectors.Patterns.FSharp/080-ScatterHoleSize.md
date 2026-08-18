# QuickVectors.Patterns.FSharp

# Scatter Hole size

This type lets you specify the hole size in a scatter pattern.

- The [Scatter Hole Size Type](#the-scatter-hole-size-type)
    - [Limits](#limits)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Scatter Hole Size Type 

The `ScatterHoleSize` **type** defines the hole size in a scatter pattern.

### Limits

Some values are provided to give the limits of a scatter hole size, and these are:

- `minimum` : Returns the minimum scatter hole size - the lowest value that can be set;
- `maximum` : Returns the maximum scatter hole size - the highest value that can be set.

For example, `ScatterHoleSize.minimum` will return the minimum possible scatter hole size.

These values can be useful in interactive environments where you need to set the limits for a control.

### Construction

A scatter hole size can be created via the `fromFloat` function.

The value is a percentage and will be clamped to the range `minimum` to `maximum` (inclusive).

When a scatter hole size is printed to the screen the output will be `HoleSize(s)%` where `s` is the scatter hole size.
For example, a scatter hole size defined as 25.0% with `ScatterHoleSize.fromFloat 25.0` will be printed as `HoleSize(25)%`.

### Deconstruction

The internal scatter hole size can be obtained via the `toFloat` function.

### Variations

A scatter hole size, once constructed, cannot be modified. If you need to use a different value then just create a new scatter hole size.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.