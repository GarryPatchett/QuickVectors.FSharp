# QuickVectors.Core.FSharp

# Luminosity

Luminosities can be used to create colours in an 8-bit RGB colour space.

- The [Luminosity Type](#the-luminosity-type)
- The [Luminosity Module](#the-luminosity-module)
    - [Construction Functions](#construction-functions) with [code examples](#construction-and-deconstruction-code-examples)
    - [Deconstruction Functions](#deconstruction-functions) with [code examples](#construction-and-deconstruction-code-examples)
    - [Variation Functions](#variation-functions) with [code examples](#variation-code-examples)
    - [Ready-made Values](#ready-made-values)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

> See the `QuickData.Core.FSharp` documentation for more information about the Normal type.

## The Luminosity Type

The `Luminosity` **type** defines a colour component in an 8-bit RGB colour space.

Valid colour component luminosity values are integers within the range 0 to 255 (inclusive),
with 0 being the lowest value (least luminous, darkest) and 255 being the highest value (most luminous, lightest).

The type provides various operators/properties for manipulating/querying luminosities, which are:

- `+` : Add two luminosities together (equivalent to the `add` function);
- `-` : Subtract one luminosity from another luminosity (equivalent to the `subtract` function);
- `*` : Multiply two luminosities (equivalent to the `multiplyBy` and `scale` functions);
- `/` : Divide one luminosity by another luminosity (equivalent to the `divideBy` function);
- `Value` : Returns the decimal value of the luminosity as a byte (equivalent to the `toByte` function);
- `ValueString` : Returns a string version of the decimal value of the luminosity (equivalent to the `toPaddedString` function).

When you print a luminosity value to the screen it will be formatted as 'Lxxx' where 'L' is the prefix
for **L**uminosity and 'xxx' is a three digit value (zero padded) containing the decimal value of the luminosity, e.g. L012
is a luminosity with the value of 12.

> **Notes:**
>
> 1. Luminosity values perform 'wrap-around' when used with arithmetic functions so, for example, adding L020 to L250 will return L014.
>
> 2. Dividing any luminosity by `Luminosity.minimum` (or any zero luminosity, e.g. L000) will return a value of `Luminosity.maximum` (or L255).

## The Luminosity Module

The `Luminosity` **module** provides various functions for creating and manipulating luminosities.

### Construction Functions 

The construction functions provided are:

- `fromByte` : Create a luminosity from a byte value;
- `fromInt` : Create a luminosity from an int value - the value will be clamped to the range of 0 to 255 (inclusive);
- `fromNormal` : Create a luminosity from a Normal;
- `random` : Create a random luminosity using the provided random number generator.

### Deconstruction Functions 

The deconstruction functions provided are:

- `toByte` : Returns the value of a luminosity as a byte;
- `toInt` : Returns the value of a luminosity as an int;
- `toNormal` : Returns the value of a luminosity as a Normal;
- `toString` : Returns the value of the luminosity as a decimal string (one, two, or three characters, depending on value);
- `toPaddedString` : Returns the value of the luminosity as a decimal string (zero-padded, always three characters);
- `toHexString` : Returns the value of the luminosity as a hex string (zero-padded, always two characters).

#### Construction and Deconstruction Code Examples

```fsharp 
// Construction.

let lumTen = Luminosity.fromByte 10uy // -> L010
let lumFifty = Luminosity.fromInt 50 // -> L050
let lumHalf = Luminosity.fromNormal Normal.oneHalf // -> L127
let lumRand = Luminosity.random System.Random.Shared // -> e.g. L057

// Deconstruction.

let ten = lumTen |> Luminosity.toInt // -> 10
let fifty = lumFifty |> Luminosity.toByte // -> 50uy 
let half = lumHalf |> Luminosity.toNormal // -> N0.4980392157
let padded = lumRand |> Luminosity.toPaddedString // -> "058"
let hex = lumRand |> Luminosity.toHexString // -> "39"
```

> **Note:** The result of converting a luminosity from or to a Normal may not, as in the example above,
be an exact conversion because conversion from one range (0 to 255) to another (0.0 to 1.0) is not always
exact. The result should be close enough in most cases to not be a big problem in practice if used only within this package.

### Variation Functions 

The variation functions provided are:

- `add` : Add two luminosities together (equivalent to the `+` operator);
- `subtract` : Subtract one luminosity from another luminosity (equivalent to the `-` operator);
- `multiplyBy` : Multiply two luminosities (equivalent to the `*` operator and `scale` function);
- `scale` : This is equivalent to the `multiplyBy` function;
- `divideBy` : Divide one luminosity by another luminosity (equivalent to the `/` operator);
- `invert` : Returns the inversion of the original luminosity;
- `darker` : Returns a darker version of the original luminosity (value does not 'wrap-around');
- `lighter` : Returns a lighter of the original luminosity (value does not 'wrap-around').

#### Variation Code Examples

```fsharp 
// Non-wrapping examples.

let forty = Luminosity.fromByte 40uy // -> L040 
let thirty = Luminosity.fromByte 30uy // -> L030 

let added = forty |> Luminosity.add thirty // -> L070
let subtracted = forty |> Luminosity.subtract thirty // -> L010
let inverted = forty |> Luminosity.invert // -> L215

let darker = Luminosity.oneHalf |> Luminosity.darker Luminosity.oneQuarter // -> L064
let lighter = Luminosity.oneHalf |> Luminosity.lighter Luminosity.oneQuarter // -> L190

// Wrapping examples. 

let twenty = Luminosity.fromByte 20uy // -> L020 
let twoFifty = Luminosity.fromInt 250 // -> L250

let subtractedWrapped = twenty |> Luminosity.subtract twoFifty // -> L026
let addedWrapped = twoFifty |> Luminosity.add twenty // -> L014
let multipliedBy = twoFifty |> Luminosity.multiplyBy twenty // -> L136
```

### Ready-made Values

The `Luminosity` **module** also provides various ready-made values which make it easy to specify some often-used luminosities.

> **Note:** Some of these values are only approximate to what their names suggest because of the nature of the range
of possible values, i.e. one-quarter of 255 is really 63.75 but that value cannot be held in an integer.

These values are:

#### Basics

- `minimum` = L000 ; the lowest possible value;
- `maximum` = L255 ; the highest possible value.

#### Fractional Values

- `oneTenth` = L025 ; one-tenth of the maximum;
- `oneFifth` = L051 ; one-fifth of the maximum;
- `oneQuarter` = L063 ; one-quarter of the maximum;
- `oneThird` = L085 ; one-third of the maximum;
- `twoFifths` = L102 ; two-fifths of the maximum;
- `oneHalf` = L127 ; half of the maximum;
- `threeFifths` = L153 ; three-fifths of the maximum;
- `twoThirds` = L170 ; two-thirds of the maximum;
- `threeQuarters` = L191 ; three-quarters of the maximum;
- `fourFifths` = L204 ; four-fifths of the maximum.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp)* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.
