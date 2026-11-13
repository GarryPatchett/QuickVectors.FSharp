# QuickVectors.Patterns.FSharp

# Opacity 

This type lets you specify an opacity.

- The [Opacity Type](#the-opacity-type)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

> **IMPORTANT:** This type, and the functionalities in this module, are for reference only at the moment.
While you can generate colours which do not have full opacity you cannot, as yet, create your own
colour which is not fully-opaque. This is expected to change in a later version.
You can create an Opacity but you cannot, as yet, apply it to anything manually.

## The Opacity Percentage Type

The `Opacity` **type** defines a discriminated union for opacities to be used when generating colours.

The cases are:

| Case Name                | Description                                                |
| ------------------------ | ---------------------------------------------------------- |
| **FullyTransparent**     | A fully-transparent opacity (0% opaque)                    |
| **FullyOpaque**          | A fully-opaque opacity (100% opaque, no transparency)      |
| **PartialOpacity**       | Any other value of opacity                                 |

When you print an opacity to the screen it will be formatted as 'O(N)' where 'N' is the opacity value as
a Normal, or 'O(Opaque)' for the FullyOpaque case, or 'O(Transparent)' for the FullyTransparent case.

### Construction Functions 

The construction functions provided are:

- `fromFloat` : Create an opacity from a float in the range of 0.0 to 1.0 (inclusive);
- `fromNormal` : Create an opacity from a Normal;
- `fromPercentage` : Create an opacity from an opacity percentage.

### Deconstruction Functions 

The deconstruction functions provided are:

- `toFloat` : Returns the value of an opacity as a float;
- `toNormal` : Returns the value of an opacity as a Normal;
- `toPercentage` : Returns the value of an opacity as an opacity percentage;
- `toPercentageFloat` : Returns the percentage value of an opacity as a float.

### Variations

Opacities, once constructed, cannot be modified. If you need to use a different value then just create a new opacity.

### Ready-made Opacities

Various ready-made opacities are available, and these are:

- `fullyTransparent` = 0% opacity : Fully-transparent;
- `oneQuarter` = 25% opacity : Mostly transparent;
- `oneHalf` = 50% opacity : Half-transparent;
- `threeQuarters` = 75% opacity : Mostly opaque;
- `fullyOpaque` = 100% opacity : Fully-opaque.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.