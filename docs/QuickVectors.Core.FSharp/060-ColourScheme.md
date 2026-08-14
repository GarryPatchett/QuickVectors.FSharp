# QuickVectors.Core.FSharp

# Colour Scheme

Provides a way to generate sequences of colours.

- The [Colour Scheme Type](#the-colour-scheme-type)
    - [Repeated Schemes](#repeated-schemes)
    - [Alternating Schemes](#alternating-schemes)
    - [Cycled Schemes](#cycled-schemes)
    - [Random Schemes](#random-schemes)
    - [Tombola Schemes](#tombola-schemes)
    - [Palette Schemes](#palette-schemes)
    - [Greyscale Schemes](#greyscale-schemes)
    - [Colour Schemes](#colour-schemes)
    - [Special Schemes](#special-schemes)
- The [Colour Scheme Module](#the-colour-scheme-module)
    - [Generation Functions](#generation-functions) with [code examples](#code-examples)
- [Self-Build Code Example](#self-build-code-example)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

> **Note:** The words ***colour*** and ***grey*** in this package use the **British** spelling.

## The Colour Scheme Type

The `ColourScheme` **type** defines a discriminated union which can be used to generate a sequence of colours.

The colours generated are options of either `None` (no colour), or `Some <colour>`.
When a colour is mentioned below it is really a `Some <colour>`, for example, Black is really `Some Colour.black`.

There are lots of colour scheme cases to choose from, each giving a different result.
Some schemes are simply 'shortcuts' defined as a way to specify another often-used scheme more
quickly, e.g. `AllBlack` instead of `AllSame Colour.black`.

There are no validation or construction functions for colour schemes as you can only create
a DU case with valid elements; just create the case as you would normally.

If any case requires a list, and that list is empty, then a sequence of invalid colour will
be generated (see documentation elsewhere).

Where there is a choice of full, dark, mid-tones, or light greyscales or colours, the luminosity ranges are:

- **Full** : 0 to 255 (inclusive);
- **Dark** : 0 to 84 (inclusive);
- **Mid-tones** : 85 to 169 (inclusive);
- **Light** : 170 to 255 (inclusive).

### Repeated Schemes

These schemes produce sequences where every element is the same.

- `AllNoColour` : All colours will be None;
- `AllBlack` : All colours will be Black;
- `AllWhite` : All colours will be White;
- `AllSame` : All colours will be that which is specified. 

### Alternating Schemes

These schemes produce sequences where two elements are repeated one after the other.

- `AlternatingBlackAndWhite` : Colours alternate between Black and White;
- `AlternatingBlackAndNoColour` : Colours alternate between Black and None;
- `AlternatingWhiteAndNoColour` : Colours alternate between White and None;
- `AlternatingBetween` : Colours alternate between those specified.

### Cycled Schemes

These schemes produce sequences where elements from a list are repeated in order.

- `CycledFrom` : The colours in the specified list will be cycled: first colour, second colour, etc.

### Random Schemes

These schemes produce sequences where elements are selected at random.

- `RandomBlackOrWhite` : Black and White will be chosen at random;
- `RandomBlackOrNoColour` : Black and None will be chosen at random;
- `RandomWhiteOrNoColour` : White and None will be chosen at random;
- `RandomBlackOrWhiteOrNoColour` : Black, White, and None will be chosen at random;
- `RandomFrom` : Colours will be chosen at random from the specified list.

### Tombola Schemes

These schemes produce sequences where elements are (endlessly) shuffled before being selected.

- `TombolaBlackOrWhite` : Black and White will be shuffled;
- `TombolaBlackOrNoColour` : Black and None will be shuffled;
- `TombolaWhiteOrNoColour` : White and None will be shuffled;
- `TombolaBlackOrWhiteOrNoColour` : Black, White, and None will be shuffled;
- `TombolaFrom` : The colours in the specified list will be shuffled before being selected.

### Palette Schemes

These schemes produce sequences of colours which are selected from a palette.

- `RandomFromPalette` : Colours will be chosen at random from the palette;
- `TombolaFromPalette` : The colours in the palette will be repeatedly shuffled before being chosen in order;
- `CycledFromPalette` : The colours in the palette will be cycled: first colour, second colour, etc.

### Greyscale Schemes

These schemes produce sequences of randomly generated greyscale colours.

- `RandomGreyscaleFull` : All greyscale colours are possible;
- `RandomGreyscaleDark` : Only dark greyscale colours are possible;
- `RandomGreyscaleMidTones` : Only greyscale colours with mid-tones are possible;
- `RandomGreyscaleLight` : Only light greyscale colours are possible;
- `RandomGreyscaleBetween` : A sequence of greyscale colours will be generated where the luminosity for each will be chosen at random between the luminosities of the colours specified.

### Colour Schemes

These schemes produce sequences of randomly generated colours.

- `RandomColourFull` : All colours are possible;
- `RandomColourDark` : Only dark colours are possible;
- `RandomColourMidTones` : Only colours with mid-tones are possible;
- `RandomColourLight` : Only light colours are possible.

### Special Schemes

These schemes produce sequences of colours according to an equation, a gradient, or a function.

- `GreyscaleByEquation` : Greyscale colours will be generated where their luminosities are defined by the given equation;
- `GreyscaleByGradient` : Greyscale colours will be generated where their luminosities are defined by the specified gradient pattern and orientation;
- `GreyscaleLinear` : Greyscale colours will be generated where their luminosities increase in a linear fashion;
- `GreyscaleLinearBounce` : Greyscale colours will be generated where their luminosities increase and then decrease in a linear fashion;
- `GreyscaleBell` : Greyscale colours will be generated where their luminosities increase and decrease to form a 'bell' shape.

## The Colour Scheme Module

The `ColourScheme` **module** provides functions for working with colour schemes.

### Generation Functions 

The generation functions provided are:

- `generateSequence`
    : Creates a sequence of colour as appropriate for the colour scheme.

Colour scheme cases, once defined, cannot be modified; if you want a different one then you will need to create a new one.

When generating a sequence you always need to also specify a random number generator, even if the sequence has no randomisation, and a count to say how many elements you want in the sequence.

### Code Examples

```fsharp 
let rng = System.Random 14791 // Randomly-chosen seed.

let allBlack = 
    ColourScheme.AllBlack
    |> ColourScheme.generateSequence rng 5 
    // -> seq { Some Black; Some Black; Some Black; 
    //          Some Black; Some Black }

let alternatingBlackWhite = 
    ColourScheme.AlternatingBlackAndWhite 
    |> ColourScheme.generateSequence rng 5 
    // -> seq { Some Black; Some White; Some Black; 
    //          Some White; Some Black }

let cycledfrom = 
    [ Colour.black ; Colour.oneThirdGrey ; Colour.twoThirdsGrey ; Colour.white ]
    |> ColourScheme.CycledFrom 
    |> ColourScheme.generateSequence rng 7
    // -> seq { Some Black; Some Grey(85); Some Grey(170); 
    //          Some White; Some Black }

let randomBlackNone = 
    ColourScheme.RandomBlackOrNoColour 
    |> ColourScheme.generateSequence rng 7
    // -> e.g. seq { None; None; Some Black; None; Some Black; 
    //               Some Black; Some Black }

let randomFromPalette = 
    StandardPalette.Retro.warmInside
    |> ColourScheme.RandomFromPalette 
    |> ColourScheme.generateSequence rng 8 
    // -> e.g. seq { Some Rgb(105,77,67); Some Rgb(105,77,67); 
    //               Some Rgb(211,124,108); Some Rgb(240,119,49); 
    //               Some Rgb(249,175,65); Some Rgb(114,114,82); 
    //               Some Rgb(211,124,108); Some Rgb(240,119,49) }

let byEquation = 
    NormalEquation.QuarterPipe 
    |> ColourScheme.GreyscaleByEquation 
    |> ColourScheme.generateSequence rng 11 
    // -> seq { Some Black; Some Grey(1); Some Grey(5); Some Grey(11); 
    //          Some Grey(21); Some Grey(34); Some Grey(50); Some Grey(72); 
    //          Some Grey(102); Some Grey(143); Some White }

let linearBounce = 
    ColourScheme.GreyscaleLinearBounce 
    |> ColourScheme.generateSequence rng 11 
    // -> seq { Some Black; Some Grey(51); Some Grey(102); 
    //          Some Grey(153); Some Grey(204); Some White; 
    //          Some Grey(204); Some Grey(153); Some Grey(102); 
    //          Some Grey(51); Some Black }
```

## Self-Build Code Example

Alternatively you can build your own sequence of colours from other sequences.

In the code below:
1. a sequence of red luminosities is built from a HockeyStick equation;
2. a sequence of green luminosities is built from a SineWave equation;
3. a sequence of blue luminosities is built from a *reversed* QuarterPipe equation;
4. the luminosities are zipped together (to make tuples) and then colours are created from them.

> **Notes** 
>
> - 1. The lengths of the value sequences should be the same, otherwise the length of the sequence
of colours will be the same as the length of the shortest value sequence.
>
> - 2. The colours generated in this way are not colour options which would otherwise be generated
via the `generateSequence` function. A simple `colours |> Seq.map Some` would rectify this, if necessary.

```fsharp 
let count = 20 

let reds = 
    Normal.Seq.byEquation NormalEquation.HockeyStick count 
    |> Seq.map Luminosity.fromNormal 

let greens = 
    Normal.Seq.byEquation NormalEquation.SineWave count 
    |> Seq.map Luminosity.fromNormal 

let blues = 
    Normal.Seq.byEquation NormalEquation.QuarterPipe count 
    |> Seq.rev 
    |> Seq.map Luminosity.fromNormal 

let colours = 
    (reds, greens, blues)
    |||> Seq.zip3
    |> Seq.map Colour.fromLuminosityTuple 
    // -> seq { Rgb(0,127,255); Rgb(0,168,173); Rgb(3,205,141); 
    //          Rgb(7,234,117); Rgb(13,251,98); Rgb(21,254,82); 
    //          Rgb(30,244,69); Rgb(41,221,57); etc. }
```

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp)* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.
