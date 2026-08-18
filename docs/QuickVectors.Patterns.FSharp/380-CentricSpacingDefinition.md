# QuickVectors.Patterns.FSharp

# Centric Spacing Definition

This type lets you define how centrics will be spaced.

- The [Centric Spacing Definition Type](#the-centric-spacing-definition-type)
    - [Cases](#cases)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
    - [Ready-made Centric Spacing Definitions](#ready-made-centric-spacing-definitions)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Centric Spacing Definition Type

The `CentricSpacingDefinition` **type** defines a discriminated union which is used to specify how centrics will be spaced.

### Cases 

The cases of the centric spacing definition are as follows:

| Case Name                 | Modifier                  | Description                                                               |
| ------------------------- | ------------------------- | ------------------------------------------------------------------------- |
| **RegularSpacing**        | KeepDistancesEqual (bool) **1*   | All centrics will be equally spaced                                       |
| **ProfiledSpacing**       | Profile ([Profile](../QuickVectors.Core.FSharp/080-Profile.md "The Profile type and module"))                  | The centrics will spaced according to the specified profile               |

- **1* : `KeepDistancesEqual` only comes into effect when the boundary dimensions are not equal.

Below are examples of centric spacing definitions:

```fsharp 
let regular = RegularSpacing(KeepDistancesEqual = true)
// -> RegularSpacing true

let profiled = ProfiledSpacing(Profile = Profile.Linear)
// -> ProfiledSpacing Linear
```

### Construction

There are no construction functions, just create a case as shown above.

### Deconstruction

There are no deconstruction functions for the type itself but you can deconstruct each field with the
deconstruction function appropriate for the type of that field.

### Variations 

There are no functions for varying the values of the type; if you need a new definition then just create a different one.

## Ready-made Centric Spacing Definitions

The ready-made centric spacing definitions available are:

- `regular` : Regular spacing, keeping distances equal;
- `linear` : Linear profiled spacing;
- `random` : Random spacing.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.