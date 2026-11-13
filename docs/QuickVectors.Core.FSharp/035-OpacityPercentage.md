# QuickVectors.Patterns.FSharp

# Opacity Percentage

This type lets you specify an amount of opacity.

- The [Opacity Percentage Type](#the-opacity-percentage-type)
    - [Limits](#limits)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

> **IMPORTANT:** This type, and the functionalities in this module, are for reference only at the moment.
While you can generate colours which do not have full opacity you cannot, as yet, create your own
colour which is not fully-opaque. This is expected to change in a later version.
You can create an Opacity Percentage but you cannot, as yet, apply it to anything other than an Opacity but an
Opacity cannot be applied to anything manually.

## The Opacity Percentage Type

The `OpacityPercentage` **type** defines a opacity percentage for a colour.

An opacity percentage of 100% is fully-opaque (no transparency). An opacity percentage of 0% is fully-transparent.

### Limits

Some values are provided to give the limits of a opacity percentage, and these are:

- `minimum` : Returns the minimum value of a opacity percentage - the lowest value that can be set;
- `maximum` : Returns the maximum value of a opacity percentage - the highest value that can be set.

For example, `OpacityPercentage.minimum` will return the minimum possible value for a opacity percentage.

These values can be useful in interactive environments where you need to set the limits for a control.

### Construction

A opacity percentage can be created via the `OpacityPercentage.fromFloat` function.

The value will be clamped to the range `minimum` to `maximum` (inclusive).

When a opacity percentage is printed to the screen the output will be `O(p)%` where `p` is the percentage.
For example, a opacity percentage defined as 20.0 with `OpacityPercentage.fromFloat 20.0` will be printed as `O(20)%`.

### Deconstruction

The internal value of a opacity percentage can be obtained via the `toFloat` function.

### Variations

Opacity Percentages, once constructed, cannot be modified. If you need to use a different value then just create a new opacity percentage.

### Ready-made Opacity Percentages

Various ready-made opacity percentages are available, and these are:

- `fullyTransparent` = 0% opacity : Fully-transparent;
- `oneQuarter` = 25% opacity : Mostly transparent;
- `oneHalf` = 50% opacity : Half-transparent;
- `threeQuarters` = 75% opacity : Mostly opaque;
- `fullyOpaque` = 100% opacity : Fully-opaque.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.