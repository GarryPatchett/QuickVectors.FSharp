# QuickVectors.Patterns.FSharp

# Number Of Centrics

This type lets you specify the number of centrics to be generated in a Centric pattern.

- The [Number Of Centrics Type](#the-number-of-centrics-type)
    - [Limits](#limits)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Number Of Centrics Type 

The `NumberOfCentrics` **type** defines the number of centrics to be generated a Centric pattern.

### Limits

Some values are provided to give the limits of a number of centrics, and these are:

- `minimum` : Returns the minimum number of centrics - the lowest value that can be set;
- `maximum` : Returns the maximum number of centrics - the highest value that can be set.

For example, `NumberOfCentrics.minimum` will return the minimum possible number of centrics.

These values can be useful in interactive environments where you need to set the limits for a control.

### Construction

A number of centrics can be created via the `fromInt` function.

The value will be clamped to the range `minimum` to `maximum` (inclusive).

When a number of centrics is printed to the screen the output will be `Centrics(n)` where `n` is the number of centrics.
For example, a number of centrics defined as 30 with `NumberOfCentrics.fromInt 30` will be printed as `Centrics(30)`.

### Deconstruction

The internal number of centrics can be obtained via the `toInt` function.

### Variations

A number of centrics, once constructed, cannot be modified. If you need to use a different value then just create a new number of centrics.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.