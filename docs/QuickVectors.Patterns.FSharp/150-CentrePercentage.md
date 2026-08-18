# QuickVectors.Patterns.FSharp

# Centre Percentage

This type lets you specify where the centre of a design will be for the PaneBlade pane form of Pane patterns.

- The [Centre Percentage Type](#the-centre-percentage-type)
    - [Limits](#limits)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Centre Percentage Type

The `CentrePercentage` **type** defines a centre percentage. Centre Percentages are only appropriate for the PaneBlade pane form of Pane patterns.

The value is used to determine the position of the centre of the design relative to the width/height of the boundary.

For example, a horizontal centre of 25% will put the centre of the design at 25% of the boundary width (quarter of the way from the **left**).
Similarly, a vertical centre of 25% will put the centre of the design at 25% of the boundary height (quarter of the way from the **top**).

### Limits

Some values are provided to give the limits of a centre percentage, and these are:

- `minimum` : Returns the minimum value of a centre percentage - the lowest value that can be set;
- `maximum` : Returns the maximum value of a centre percentage - the highest value that can be set.

For example, `CentrePercentage.minimum` will return the minimum possible value for a centre percentage.

These values can be useful in interactive environments where you need to set the limits for a control.

### Construction

A centre percentage can be created via the `CentrePercentage.fromFloat` function.

The value will be clamped to the range `minimum` to `maximum` (inclusive).

When a centre percentage is printed to the screen the output will be `Centre(p)%` where `p` is the percentage.
For example, a centre percentage defined as 40.0 with `CentrePercentage.fromFloat 40.0` will be printed as `Centre(40)%`.

### Deconstruction

The internal value of a centre percentage can be obtained via the `toFloat` function.

### Variations

Centre Percentages, once constructed, cannot be modified. If you need to use a different value then just create a new centre percentage.

### Ready-made Centre Percentages

Various ready-made centre percentages are available, and these are:

- `least` : The centre will be as far as it can be to the left/top;
- `oneQuarter` : The centre will be a quarter of the way from left/top;
- `middle` : The centre will be in the middle;
- `threeQuarters` : The centre will be a quarter of the way from right/bottom;
- `most` : The centre will be as far as it can be to the right/bottom. 

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.