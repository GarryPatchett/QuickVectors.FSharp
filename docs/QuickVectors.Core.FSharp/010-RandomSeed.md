# QuickVectors.Core.FSharp

# Random Seed

This type lets you define a seed value which will be used to create random number generators.

- The [Random Seed Module](#the-random-seed-module)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Random Seed Module 

The `RandomSeed` **module** lets you define a random seed.

You can use a specific random seed to generate patterns which follow the same process or use
a randomly generated seed to create patterns which can look very different.

### Construction

A random seed can be created via either of these functions:

- `fromInt` : Creates a new random seed from the value specified;
- `generate()` : Generates a new randomly-chosen random seed.

The value specified will be clamped to the range of zero to just under the maximum possible value of an int (this is for internal processing reasons).

When a random seed is printed to the screen the output will be `Random(S)` where `S` is the seed value.

### Deconstruction

The internal value of a random seed can be obtained via the `toInt` function.

This can be useful if you want to store the seed value for use later.

### Variations

Random seeds, once constructed, cannot be modified. If you need to use a different value then just create a new seed.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp)* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.
