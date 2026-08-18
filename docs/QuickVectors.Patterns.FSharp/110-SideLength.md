# QuickVectors.Patterns.FSharp

# Side Length

This type lets you define the length of a side of a tessellator.

- The [Side Length Type](#the-side-length-type)
    - [Limits](#limits)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Side Length Type

The `SideLength` **type** defines a side length. Side lengths are only appropriate for the Tessellation patterns.

### Limits

Some values are provided to give the limits of a side length, and these are:

- `minimum` : Returns the minimum value of a side length - the lowest value that can be set;
- `maximum` : Returns the maximum value of a side length - the highest value that can be set.

For example, `SideLength.minimum` will return the minimum possible value for a side length.

These values can be useful in interactive environments where you need to set the limits for a control.

### Construction

A side length can be created via the `SideLength.fromFloat` function.

The value will be clamped to the range `minimum` to `maximum` (inclusive).

When a side length is printed to the screen the output will be `SideLength(l)` where `l` is the length.
For example, a side length defined as 50.0 with `SideLength.fromFloat 50.0` will be printed as `SideLength(50)`.

> **Note:** Not all of the edges of all of the tessellators will be of the side length. You can see visual examples of the tessellators [here](../QuickVectors.Core.FSharp/images/Tessellator-Examples.png "Visual roll call of the available tessellators").

### Deconstruction

The internal value of a side length can be obtained via the `toFloat` function.

### Variations

Side lengths, once constructed, cannot be modified. If you need to use a different value then just create a new side length.

### Ready-made Side Lengths

Various ready-made side lengths are available, and these are:

- `twentyFive` : A side length of 25.0;
- `fifty` : A side length of 50.0;
- `seventyFive` : A side length of 75.0;
- `oneHundred` : A side length of 100.0.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.