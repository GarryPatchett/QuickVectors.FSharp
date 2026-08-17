# QuickVectors.Core.FSharp

# Range

Used to define a range of values.

- The [Range Type](#the-range-type)
- The [Range Module](#the-range-module)
    - [Construction Functions](#construction-functions) with [code examples](#construction-and-deconstruction-code-examples)
    - [Deconstruction Functions](#deconstruction-functions) with [code examples](#construction-and-deconstruction-code-examples)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Range Type

The `Range` **type** defines a discriminated union with cases for single-value and double-value ranges.

Ranges can be created of any type which is comparable, although it's probably best to use the basic types such as int, float, etc.

A range which was defined with two distinct values will be a double-value range and a range which was defined
with only one unique value will be a single-value range. It is usual to define a double-value range but that's
not always necessary, or possible.

The type provides various properties, which are:

- `Low` : Returns the low value of the range (equivalent to the `lowValue` function);
- `High` : Returns the high value of the range (equivalent to the `highValue` function);
- `AsDisplayString` : Returns a string representation of the range.

When you print a range to the screen it will be formatted as:
- a single-value range of 'Range(V)' where 'V' is the single value;
- a double-value range of 'Range(L,H)' where 'L' is the low value and 'H' is the high value.

For example, Range(10,50) is a range of int between 10 and 50 inclusive.

## The Range Module

The `Range` **module** provides various functions for creating and manipulating ranges.

### Construction Functions 

The construction functions provided are:

- `fromSingleValue` : Creates a new range from a single value;
- `fromValues` : Creates a new range from two values.

### Deconstruction Functions 

The deconstruction functions provided are:

- `lowValue` : Returns the low value of range (equivalent to the `Low` property);
- `highValue` : Returns the high value of range (equivalent to the `High` property).

#### Construction and Deconstruction Code Examples

```fsharp 
// Construction.

let fromTwoInts = Range.fromValues 10 50 // -> R(10,50)
let fromSingleInt = Range.fromSingleValue 25 // -> R(25)
let fromTwoFloats = Range.fromValues 20.5 60.2 // -> R(20.5,60.2)
let fromSingleFloat = Range.fromSingleValue 55.5 // -> R(55.5)

// Properties.

let singleIntLowProperty = fromSingleInt.Low // -> 25
let twoFloatsHighProperty = fromTwoFloats.High // -> 60.2
let twoFloatsString = fromTwoFloats.AsDisplayString // -> "R(20.5,60.2)"

// Deconstruction.

let singleIntLowValue = fromSingleInt |> Range.lowValue // -> 25
let twoFloatsHighValue = fromTwoFloats |> Range.highValue // -> 60.2
```

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.