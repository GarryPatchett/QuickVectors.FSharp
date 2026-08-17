# QuickVectors.Core.FSharp

# Colour

Colours in an 8-bit RGB colour space which can be used in designs and patterns.

- The [Colour Type](#the-colour-type)
- The [Colour Module](#the-colour-module)
    - [Construction Functions](#construction-functions) with [code examples](#construction-and-deconstruction-code-examples)
    - [Deconstruction Functions](#deconstruction-functions) with [code examples](#construction-and-deconstruction-code-examples)
    - [Variation Functions](#variation-functions) with [code examples](#variation-code-examples)
    - [Ready-made Values](#ready-made-values)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

> **Note:** The words ***colour*** and ***grey*** in this package use the **British** spelling.

## The Colour Type

The `Colour` **type** defines a single-case discriminated union which specifies a colour in an 8-bit RGB colour space.

The colour type has three fields:

- `Red` : The red component of the colour;
- `Green` : The green component of the colour;
- `Blue` : The blue component of the colour.

Each of these fields is a [Luminosity](030-Luminosity.md "The Luminosity type and module").

All combinations of luminosities are valid.

You can construct a colour by simply supplying the luminosities as required or you can use one of the convenience functions
provided by the `Colour` **module** (see below).

The type provides one property for obtaining information from a colour, which is:

- `AsDisplayString`
    : Returns a string which describes the colour in a succinct way (see below).

When you print a colour value to the screen it will be formatted as follows:

- `Black` : Black;
- `White` : White;
- `Grey(lum)` : Greyscale where *lum* is the decimal luminosity (of each component);
- `Rgb(red,green,blue)` : Full Colour where *red*, *green*, and *blue* are the decimal luminosity component values.

> **Note:** There is currently no provision for colour transparency in this package; all colours are fully-opaque.

## The Colour Module

The `Colour` **module** provides various functions for creating and manipulating colours.

### Construction Functions 

The construction convenience functions provided are:

- `fromSingleByte` : Create a colour from a single byte value;
- `fromBytes` : Create a colour from three byte values;
- `fromByteTuple` : Create a colour from a tuple containing three byte values;
- `fromSingleLuminosity` : Create a colour from a single luminosity;
- `fromLuminosities` : Create a colour from three luminosities;
- `fromLuminosityTuple` : Create a colour from a tuple containing three luminosities;
- `fromSingleInt` : Create a colour from a single int value;
- `fromInts` : Create a colour from three int values;
- `fromIntTuple` : Create a colour from a tuple containing three int values;
- `fromHexString` : Create a colour from a string containing hexadecimal characters.

The `fromHexString` function processes the string as follows:

1. If the string starts with "0x", or "#", then this prefix is ignored.
2. All non-hexadecimal characters are ignored. The characters 'a' to 'f', 'A' to 'F', and '0' to '9' (all inclusive) are the only valid characters.
3. The remaining characters are then interpreted as follows:
    - "A" - interpreted as "AAAAAA";
    - "AB" - interpreted as "ABABAB";
    - "ABC" - interpreted as "AABBCC";
    - "ABCDEF" - accepted as is.
4. Only the first six characters, after interpretation, are considered.
5. After interpretation, the first two characters are the red component, 
the second two characters are the green component, and the last two characters are the blue component.
6. If the string contains no valid characters after interpretation, or the number of characters is not as expected, then an exception is raised.

> **Note:** If there is an error while generating a colour via the functionalities elsewhere in this package then
an invalid colour will be created. This colour looks like a 'hot pink' and, as such, is usually easily noticed. If
you see this colour then please report it describing the circumstances in which it was generated.

### Deconstruction Functions 

The deconstruction functions provided are:

- `toByteTuple` : Returns a new tuple containing three bytes which correspond to
                    the red, green, and blue components of the colour in that order;
- `toLuminosityTuple` : Returns a new tuple containing three luminosities which correspond to
                    the red, green, and blue components of the colour in that order;
- `toIntTuple` : Returns a new tuple containing three ints which correspond to
                    the red, green, and blue components of the colour in that order;
- `toHexString` : Returns a string containing the red, green, and blue components of the
                    colour, each as a two-character hexadecimal value, in that order.

### Construction and Deconstruction Code Examples

```fsharp 
// Construction.

let manualConstruction = 
        Colour(Red = Luminosity.oneHalf,
               Green = Luminosity.oneFifth, 
               Blue = Luminosity.twoThirds)
        // -> Rgb(127,51,170)

let fromBytes = Colour.fromBytes 50uy 100uy 150uy // -> Rgb(50,100,150)

let fromSingleInt = Colour.fromSingleInt 32 // -> Grey(32)

let fromLuminosityTuple = 
    Colour.fromLuminosityTuple 
        (Luminosity.oneFifth, Luminosity.oneHalf, Luminosity.fourFifths)
        // -> Rgb(51,127,204)

let fromHexString = Colour.fromHexString "B1A5ED" // -> Rgb(177,165,237)

let invalidColour = Colour.fromHexString "WRONG" // -> Raises System.Exception

// Deconstruction.

let toLuminosityTuple = 
    fromBytes 
    |> Colour.toLuminosityTuple 
    // -> (L050, L100, L150)

let toByteTuple = 
    fromSingleInt 
    |> Colour.toByteTuple
    // -> (32uy, 32uy, 32uy)

let toIntTuple = 
    fromLuminosityTuple 
    |> Colour.toIntTuple 
    // -> (51, 127, 204)

let toHexString = 
    fromBytes
    |> Colour.toHexString 
    // -> "326496"
```

### Variation Functions 

The variation functions provided are:

- `invert` : Returns a new colour where each component has been inverted;
- `rev` : Returns a new colour with the components reversed;
- `shiftToRed` : Returns a new colour where the components have been shifted to the left, in the direction of red;
- `shiftToBlue` : Returns a new colour where the components have been shifted to the right, in the direction of blue.
- `darker` : Returns a new colour where the components have been made darker than those in the original;
- `lighter` : Returns a new colour where the components have been made lighter than those in the original.

> **Note:** Some of the above functions will, depending upon the original colour, simply return the original
colour when the function cannot have any effect. For example, reversing the components of a greyscale colour
will have no effect because they all have the same value.

### Variation Code Examples

```fsharp 
let original = Colour.fromBytes 50uy 100uy 150uy // -> Rgb(50,100,150)

let inverted = 
    original 
    |> Colour.invert 
    // -> Rgb(205,155,105)

let reversed = 
    original 
    |> Colour.rev 
    // -> Rgb(150,100,50)

let shiftedToRed = 
    original 
    |> Colour.shiftToRed 
    // -> Rgb(100,150,50)

let shiftedToBlue = 
    original 
    |> Colour.shiftToBlue 
    // -> Rgb(150,50,100)

let darker = 
    original
    |> Colour.darker (Luminosity.fromByte 10uy)
    // -> Rgb(40,90,140)

let lighter = 
    original
    |> Colour.lighter (Luminosity.fromByte 10uy)
    // -> Rgb(60,110,160)
```

### Ready-made Values

The `Colour` **module** also provides various ready-made values which make it easy to specify some often-used colours.

These values are:

#### Basics

- `black` = Black ; all luminosities are Luminosity.minimum (e.g. 0);
- `white` = White ; all luminosities are Luminosity.maximum (e.g. 255).

#### Greyscale

These are values for grey colours where the component values are equal.

- `oneTenthGrey` = Grey(25) ; one-tenth of the maximum;
- `oneFifthGrey` = Grey(51) ; one-fifth of the maximum;
- `oneQuarterGrey` = Grey(63) ; one-quarter of the maximum;
- `oneThirdGrey` = Grey(85) ; one-third of the maximum;
- `twoFifthsGrey` = Grey(102) ; two-fifths of the maximum;
- `oneHalfGrey` = Grey(127) ; one-half of the maximum;
- `threeFifthsGrey` = Grey(153) ; three-fifths of the maximum;
- `twoThirdsGrey` = Grey(170) ; two-thirds of the maximum.
- `threeQuartersGrey` = Grey(191) ; three-quarters of the maximum;
- `fourFifthsGrey` = Grey(204) ; four-fifths of the maximum.

#### Bright Colours

- `brightRed` = Rgb(255,0,0) ; A colour where the red component value is at the maximum and the others are at the minimum;
- `brightGreen` = Rgb(0,255,0) ; A colour where the green component value is at the maximum and the others are at the minimum;
- `brightBlue` = Rgb(0,0,255) ; A colour where the blue component value is at the maximum and the others are at the minimum.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.