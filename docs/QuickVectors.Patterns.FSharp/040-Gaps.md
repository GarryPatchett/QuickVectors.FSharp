# QuickVectors.Patterns.FSharp

# Gaps

These types let you change the sizes of gaps in a grid-based pattern.

They are:
- `ColumnGap`
    : The size of a gap between columns;
- `RowGap`
    : The size of a gap between rows.

They are used in various Definition types.

Since they are similar they are documented together; what applies to one applies to the other. 

- [Shared Functionality](#shared-functionality)
    - [Limits](#limits)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## Shared Functionality

### Limits

Some values are provided to give the limits of a gap size, and these are:

- `minimum` : Returns the minimum value of a gap size - the lowest value that can be set;
- `maximum` : Returns the maximum value of a gap size - the highest value that can be set.

For example, `ColumnGap.minimum` will return the minimum possible value for a column gap size.

These values can be useful in interactive environments where you need to set the limits for a control.

### Construction

A gap size can be created via the `fromFloat` function, e.g. `ColumnGap.fromFloat` or `RowGap.fromFloat`.

The value will be clamped to the range `minimum` to `maximum` (inclusive).

When a gap is printed to the screen the output will be either `ColumnGap(s)` (for a column gap) or
`RowGap(s)` (for a row gap) where `s` is the size. For example, a column gap defined as 16.0 with 
`ColumnGap.fromFloat 16.0` will be printed as `ColumnGap(16)`.

### Deconstruction

The internal value of a gap size can be obtained via the `toFloat` function.

### Variations

Gaps, once constructed, cannot be modified. If you need to use a different value then just create a new gap.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.