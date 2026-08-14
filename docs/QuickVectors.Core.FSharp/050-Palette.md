# QuickVectors.Core.FSharp

# Palette

A selection of colours in an 8-bit RGB colour space which can be used in designs and patterns.

- The [Palette Type](#the-palette-type)
- The [Palette Module](#the-palette-module)
    - [Construction Functions](#construction-functions) with [code examples](#construction-and-deconstruction-code-examples)
    - [Deconstruction Functions](#deconstruction-functions) with [code examples](#construction-and-deconstruction-code-examples)
    - [Variation Functions](#variation-functions) with [code examples](#variation-code-examples)
    - [Ready-made Palettes](#ready-made-palettes) in the StandardPalette module
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

> **Note:** The words ***colour*** and ***grey*** in this package use the **British** spelling.

## The Palette Type

The `Palette` **type** defines a palette containing colours in an 8-bit RGB colour space.

A palette can be defined via an array of colours or an array of weighted colours.

## The Palette Module

The `Palette` **module** provides various functions for creating and manipulating palettes.

### Construction Functions 

The construction functions provided are:

- `fromColours` : Create a palette from an array of colours, all with the same weight;
- `fromWeightedColours` : Create a palette from an array of colours and weights (specified with tuples).

> **Note:** The maximum number of colours in a palette is defined by the `Palette.maximumNumberOfColours` value; any colours in the source array after that many are ignored.

### Colour Weights

When weights are specified, they refer to the amount of each colour that the palette contains.

For example, given the following array of colours and weights:

`[| (Colour.black, 1) ; (Colour.oneHalfGrey, 2) ; (Colour.white, 3) |]`

- Colour.black is given the weight of 1;
- Colour.oneHalfGrey is given the weight of 2;
- Colour.white is given the weight of 3.

There is twice the amount of Colour.oneHalfGrey than there is of Colour.black, and there is three times the amount of Colour.white than there is of Colour.black, and one and a half times the amount of Colour.white than there is of Colour.oneHalfGrey.

The more of a particular colour there is in a palette the more often that colour will be chosen when generating colours from a Colour Scheme (see related documentation) which uses that palette.

If all of the colours in a palette have the same weight then they are all just as likely to be chosen.

> **Note:** Weights are clamped to the range of 1 to 20 (inclusive) so that no one colour can be 'overly-present'.

### Deconstruction Functions 

The deconstruction functions provided are:

- `numberOfColours` : Returns the number of colours in the palatte;
- `colours` : Returns an array containing the colours in the palette;
- `weights` : Returns an array containing the colour weights in the palette.

### Construction and Deconstruction Code Examples

```fsharp 
let fromColours = 
    [|  Colour.black 
        Colour.white |]
    |> Palette.fromColours 

let fromWeightedColours = 
    [|  Colour.oneThirdGrey, 1 
        Colour.twoThirdsGrey, 2 
        Colour.white, 3 |]
    |> Palette.fromWeightedColours 

let numberOfColours = 
    fromWeightedColours 
    |> Palette.numberOfColours 
    // -> 3 

let weights = 
    fromWeightedColours 
    |> Palette.weights 
    // -> [| 1 ; 2 ; 3 |]
```

### Variation Functions 

The variation functions provided are:

- `rev` : Creates a new palette where the colours and weights of the original are in reverse order;
- `lighter` : Creates a new palette where the colours of the original are lighter;
- `darker` : Creates a new palette where the colours of the original are darker.

### Variation Code Examples

```fsharp 
let fromWeightedColours = 
    [|  Colour.oneThirdGrey, 1 
        Colour.twoThirdsGrey, 2 
        Colour.white, 3 |]
    |> Palette.fromWeightedColours 

let reversedWeights = 
    fromWeightedColours 
    |> Palette.rev 
    |> Palette.weights
    // -> [| 3 ; 2 ; 1 |]
```

### Ready-made Palettes

The `StandardPalette` **module** provides dozens of ready-made palettes.

These palettes are split into various sub-modules, which are:

| Module Name               | Description                                                               |
| ------------------------- | ------------------------------------------------------------------------- | 
| **Basic**                 | Basic colour combinations                                                 |
| **FiveShades**            | Five shades of a colour or grey **1*                                      |
| **SevenShades**           | Seven shades of a colour or grey **1*                                     |
| **Shades**                | Various shades of similar/complementary colours                           |
| **MultiColour**           | Different colours which go nicely together                                |
| **Vista**                 | Colours which can be useful when creating a sunset, sunrise, or vista     |
| **Flags**                 | (Approximate) colours which form some national/organisational flags       |

- **1* : The luminosities of the shades are between 80uy and 235uy (inclusive).

Some examples are:

- `StandardPalette.Basic.blackAndWhite` : Just black and white;
- `StandardPalette.SevenShades.redDarkToLight` : Seven shades of red;
- `StandardPalette.Shades.halloween` : For Hallow'een;
- `StandardPalette.MultiColour.forestBerries` : Think of 1970's bathrooms and wallpaper;
- `StandardPalette.Vista.desert` : A desert sunset;
- `StandardPalette.Flags.PrideRainbow` : The colours of the Pride rainbow flag.

Try experimenting with different palettes in various designs to see which you like best in certain situations.

If you want to make a slightly different version of a standard palette, or any other palette, then that's possible.
The code below shows an example of making a slightly darker version of an existing one.

```fsharp 
let originalPalette = StandardPalette.Shades.warmInside 

let originalColours = originalPalette |> Palette.colours 
let originalWeights = originalPalette |> Palette.weights

let darkening = Luminosity.fromByte 10uy 
let darkerColours = originalColours |> Array.map (Colour.darker darkening)

let newPalette = 
    (darkerColours, originalWeights)
    ||> Array.zip 
    |> Palette.fromWeightedColours 
```

(In the case above you could also use the `Palette.darker` function.)

Or you can make your own palette from a sequence of values, such as:

```fsharp 
// Create a linear sequence of eight Normals. 
Normal.Seq.byEquation NormalEquation.Linear 8 
// Denormalise the values to the range of 100.0 to 200.0. 
|> Normal.Seq.denormalise (DenormalisationRange.fromFloats 100.0 200.0)
// Convert each denormalised float to a byte.
|> Seq.map byte 
// Create a colour (e.g. shade of red) from each luminosity value. 
|> Seq.map (fun luminosity -> Colour.fromBytes luminosity 0uy 0uy)
// Create an array from the sequence. 
|> Seq.toArray 
// Create a palette from the array. 
|> Palette.fromColours 
// -> { NumberOfColours = 8
//      Colours =
//         [| Rgb(100,0,0); Rgb(114,0,0); Rgb(128,0,0); Rgb(142,0,0);
//            Rgb(157,0,0); Rgb(171,0,0); Rgb(185,0,0); Rgb(200,0,0) |]
//      Weights = [| 1; 1; 1; 1; 1; 1; 1; 1 |]
//      ExpandedColourIndices = [| 0; 1; 2; 3; 4; 5; 6; 7 |] }
```

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp)* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.
