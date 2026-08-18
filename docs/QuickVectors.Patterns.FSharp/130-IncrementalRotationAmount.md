# QuickVectors.Patterns.FSharp

# Incremental Rotation Amount

This type lets you specify the incremental rotation amount to be generated in a Centric pattern.

- The [Incremental Rotation Amount Type](#the-incremental-rotation-amount-type)
    - [Limits](#limits)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Incremental Rotation Amount Type 

The `IncrementalRotationAmount` **type** defines the incremental rotation amount to be used in a Centric pattern.

### Limits

Some values are provided to give the limits of a incremental rotation amount, and these are:

- `minimum` : Returns the minimum incremental rotation amount - the lowest value that can be set;
- `maximum` : Returns the maximum incremental rotation amount - the highest value that can be set.

For example, `IncrementalRotationAmount.minimum` will return the minimum possible incremental rotation amount.

These values can be useful in interactive environments where you need to set the limits for a control.

### Construction

An incremental rotation amount can be created via the `fromFloat` function.

The value will be clamped to the range `minimum` to `maximum` (inclusive).

When a incremental rotation amount is printed to the screen the output will be `IncrementalRotation(n)` where `n` is the incremental rotation amount.
For example, an incremental rotation amount defined as 5.5 with `IncrementalRotation.fromFloat 5.5` will be printed as `IncrementalRotation(5.5)`.

### Deconstruction

The internal incremental rotation amount can be obtained via the `toFloat` function.

### Variations

An incremental rotation amount, once constructed, cannot be modified. If you need to use a different value then just create a new incremental rotation amount.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.