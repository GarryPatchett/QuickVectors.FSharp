# QuickVectors.Patterns.FSharp

# Jiggle Percentage

This type lets you specify an amount of jiggle.

- The [Jiggle Percentage Type](#the-jiggle-percentage-type)
    - [Limits](#limits)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Jiggle Percentage Type

The `JigglePercentage` **type** defines a jiggle percentage. Jiggle Percentages are only appropriate for the Pane patterns.

The value is used to determine the maximum distance by which a vertex in the pane can vary from its 'natural' position.

The 'natural' positions of the vertices are calculated as if they were on a grid and the jiggle distances are chosen at random up to the specified amount.

### Limits

Some values are provided to give the limits of a jiggle percentage, and these are:

- `minimum` : Returns the minimum value of a jiggle percentage - the lowest value that can be set;
- `maximum` : Returns the maximum value of a jiggle percentage - the highest value that can be set.

For example, `JigglePercentage.minimum` will return the minimum possible value for a jiggle percentage.

These values can be useful in interactive environments where you need to set the limits for a control.

### Construction

A jiggle percentage can be created via the `JigglePercentage.fromFloat` function.

The value will be clamped to the range `minimum` to `maximum` (inclusive).

When a jiggle percentage is printed to the screen the output will be `Jiggle(l)%` where `l` is the percentage.
For example, a jiggle percentage defined as 20.0 with `JigglePercentage.fromFloat 20.0` will be printed as `Jiggle(20)%`.

### Deconstruction

The internal value of a jiggle percentage can be obtained via the `toFloat` function.

### Variations

Jiggle Percentages, once constructed, cannot be modified. If you need to use a different value then just create a new jiggle percentage.

### Ready-made Jiggle Percentages

Various ready-made jiggle percentages are available, and these are:

- `none` : No jiggle at all; vertices will retain their 'natural' positions;
- `less` : A small amount of jiggle (quarter of the maximum);
- `moderate` : A moderate amount of jiggle (half of the maximum);
- `more` : A large amount of jiggle (three-quarters of the maximum);
- `most` : The largest amount of jiggle (maximum). 

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.