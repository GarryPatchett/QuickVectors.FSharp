# QuickVectors.Patterns.FSharp

# Reordering and Modification

These types let you change the order and value of the elements generated via a profile.

They are used in various Definition types.

- The [Sequence Reordering Type](#the-sequence-reordering-type)
- The [Value Modification Type](#the-value-modification-type)
- The [Colour Reordering Type](#the-colour-reordering-type)
- The [Colour Modification Type](#the-colour-modification-type)
- [Discriminated Union Identity Values](#discriminated-union-identity-values)
- [Exception-free Processing](#exception-free-processing)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Sequence Reordering Type

The `SequenceReordering` **type** defines a discriminated union used to specify how the sequence of generated values can be reordered.

The cases are:

| Case Name                 | Description                                                               |
| ------------------------- | ------------------------------------------------------------------------- | 
| **ReversedSequence**      | The sequence will be reversed                                             |
| **SortAscending**         | The values in the sequence will be sorted by value in ascending order     |
| **SortDescending**        | The values in the sequence will be sorted by value in descending order    |

To specify a reordering simply supply its name, such as `SequenceOrdering.ReversedSequence`.

## The Value Modification Type

The `ValueModification` **type** defines a discriminated union used to specify how the values in a generated sequence can be further modified.

The cases are:

| Case Name                 | Description                                                               |
| ------------------------- | ------------------------------------------------------------------------- | 
| **InvertValues**          | Each value in the sequence will be inverted                               |

To specify a value modification simply supply its name, such as `ValueModification.InvertValues`.

## The Colour Reordering Type

The `ColourReordering` **type** defines a discriminated union used to specify how the sequence of colours can be reordered.

The cases are:

| Case Name                         | Description                                                                                   |
| --------------------------------- | --------------------------------------------------------------------------------------------- | 
| **ReversedSequence**              | The sequence will be reversed                                                                 |
| **SortedByAscendingLuminosity**   | The colours in the sequence will be sorted by the sum of the luminosities                     |
| **SortedByDescendingLuminosity**  | The colours in the sequence will be sorted by the sum of the luminosities in descending order |

To specify a reordering simply supply its name, such as `ColourReordering.ReversedSequence`.

## The Colour Modification Type

The `ColourModification` **type** defines a discriminated union used to specify how the colours in a generated sequence can be further modified.

The cases are:

| Case Name                 | Description                                                               |
| ------------------------- | ------------------------------------------------------------------------- | 
| **InvertColours**         | Each colour in the sequence will be inverted                              |
| **ReverseComponents**     | Each colour in the sequence will have its components reversed             |
| **ShiftComponentsToRed**  | Each colour in the sequence will have its components shifted to the red   |
| **ShiftComponentsToBlue** | Each colour in the sequence will have its components shifted to the blue  |

To specify a value modification simply supply its name, such as `ColourModification.InvertColour`.

## Discriminated Union Identity Values

Functions are available for converting to and from POCO types and DU cases. 
See the [overview documentation](000-Overview.md "Package overview") for more information about these.

For the types described above there is no `defaultCase` value.

## Exception-free Processing

Exception-free processing versions - Option and Result - of some functions are available. 
See the [overview documentation](000-Overview.md "Package overview") for more information about these.

For the types described above there is no `FailSafe.fromInt` function and it is recommended
that you use the `Option.fromInt` function instead.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.