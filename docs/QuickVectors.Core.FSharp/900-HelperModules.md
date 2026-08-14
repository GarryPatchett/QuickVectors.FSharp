# QuickVectors.Core.FSharp

# Helper Modules

Some modules exist which provide some helper functions which might be useful.

- The [Byte Helpers Module](#the-byte-helpers-module) with [code examples](#byte-helpers-code-examples)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Byte Helpers Module

The `ByteHelpers` module provides these functions for manipulating byte values:

- `asShortString` : Returns the value of the byte as a decimal string (one, two, or three characters, depending on value).
                    (The string will not have the "uy" suffix which is normally added when printing the value via printf and its variants);
- `asPaddedString` : Returns the value of the byte as a decimal string (zero-padded, always three characters).
                    (The string will not have the "uy" suffix which is normally added when printing the value via printf and its variants);
- `asHexString` : Returns the value of the byte as a hex string (zero-padded, always two characters);
- `invert` : Returns the inversion of the original byte, e.g. result = 255uy - original;
- `fromInt` : Returns a byte from an int value - the value will be clamped to the range of 0 to 255 (inclusive).

### Byte Helpers Code Examples

```fsharp 
let ten = 10uy |> ByteHelpers.asShortString // -> "10"
let twenty = 20uy |> ByteHelpers.asPaddedString // -> "020"
let thirty = 30uy |> ByteHelpers.asHexString // -> "1E"
let inverted = 100uy |> ByteHelpers.invert // 155uy
let tooLow = -5 |> ByteHelpers.fromInt // -> 0uy
let tooHigh = 300 |> ByteHelpers.fromInt // -> 255uy
let justRight = 150 |> ByteHelpers.fromInt // -> 150uy
```

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp)* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.
