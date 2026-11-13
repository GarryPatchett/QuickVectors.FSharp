# QuickVectors.Patterns.FSharp

# Backgrounds

A design can have one or more backgrounds, each of which covers the extents of the design.

- [General Information](#general-information)
- The [Background Strategy Type](#the-background-strategy-type)
- The [Strategies Explained](#the-strategies-explained)
    - [SpecificColour](#specificcolour)
    - [LightestColour](#lightestcolour)
    - [HighestLuminositiesColour](#highestluminositiescolour)
    - [AverageColour](#averagecolour)
    - [AverageGrey](#averagegrey)
    - [LowestLuminositiesColour](#lowestluminositiescolour)
    - [DarkestColour](#darkestcolour)
- [Ready-made Background Strategies](#ready-made-background-strategies)
- [Discriminated Union Identity Values](#discriminated-union-identity-values)
- [Exception-free Processing](#exception-free-processing)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## General Information

The background is a rectangular path, covering the extents of the design, filled with the provided/calculated
colour but with no stroke.

It can often be useful when some generated shapes, in some patterns, by their nature, show
a tiny gap at their aligned edges (e.g. because of on-screen antialiasing). Adding a background can help
to remove the visible 'gaps' between the shapes by making them 'blend' together.

For example, in the image below, the (simulated with a gradient) grey background on the left can be contrasted with
the white background (default in some file viewers) on the right. The gaps between the shapes are far less
visible on the left with the grey background than they are on the right with no background (or a white one).

![Background Examples Image](images/Background-Examples.png "Background Examples")

It's best to experiment with different backgrounds to see which is best in each case.

Backgrounds are drawn below the design - as the first element(s) in the exported file - in the order in
which they are added in your code.

While multiple backgrounds are possible, only the last one which was added will be seen because prior
backgrounds will be drawn underneath (before) the last one.

## The Background Strategy Type

The `BackgroundStrategy` **type** defines a discriminated union for strategies that can be used to choose a background colour.

The cases are:

| Case Name                         | Modifier                                                                          | What Will Be Used For The Background Colour?                          |
| --------------------------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| **SpecificColour**                | [Colour](../QuickVectors.Core.FSharp/040-Colour.md "The Colour type and module")  | The specified colour.                                                 |
| **LightestColour**                | None                                                                              | The lightest colour in the design.                                    |
| **HighestLuminositiesColour**     | None                                                                              | A colour with the highest luminosities of the colours in the design.  |
| **AverageColour**                 | None                                                                              | A colour with the average luminosities of the colours in the design.  |
| **AverageGrey**                   | None                                                                              | A grey with the average luminosities of the colours in the design.    |
| **LowestLuminositiesColour**      | None                                                                              | A colour with the lowest luminosities of the colours in the design.   |
| **DarkestColour**                 | None                                                                              | The darkest colour in the design.                                     |

To specify a background strategy simply supply its name, such as `BackgroundStrategy.DarkestColour`, with the modifier if necessary.

## The Strategies Explained

In the following explanations, lightest and darkest refer to the luminosity values (actual component values) rather
than the overall luminance (how bright it looks) of the colour.

The background colour is calculated from the **fill** colours of the shapes in the design, unless a specific
colour has been specified. The stroke colours are always ignored.

### SpecificColour

The background colour will be that which is specified.

### LightestColour

The background colour will be the same as the colour in the design which has the lightest combined luminosities.
The luminosities of the components of each colour are added together and the colour with the highest total is used.

If no elements of the design have a fill colour then the background will be coloured white.

### HighestLuminositiesColour

The background colour will have the highest components of all the colours of the design.
The red components are extracted and the highest value is used as the red component of the background colour. Same for the green and blue components.

If no elements of the design have a fill colour then the background will be coloured white.

### AverageColour

The components of each kind of all colours are averaged and these values are used as the luminosities of a colour.

E.g. Get the average of the red component values and use that as the new red component value, and same for green and blue.

If no elements of the design have a fill colour then the background will be coloured one-half grey.

### AverageGrey

The components of all colours are averaged and this value is used as the luminosity of a greyscale colour.

If no elements of the design have a fill colour then the background will be coloured one-half grey.

### LowestLuminositiesColour

The background colour will have the lowest components of all the colours of the design.
The red components are extracted and the lowest value is used as the red component of the background colour. Same for the green and blue components.

If no elements of the design have a fill colour then the background will be coloured black.

### DarkestColour

The background colour will be the same as the colour in the design which has the darkest combined luminosities.
The luminosities of the components of each colour are added together and the colour with the lowest total is used.

If no elements of the design have a fill colour then the background will be coloured black.

## Ready-made Background Strategies

The `BackgroundStrategy` **module** defines various ready-made background strategies, and these are:

A background which is coloured...

- `white` : ...white;
- `oneHalfGrey` : ...one-half grey;
- `darkRed` : ...dark red;
- `darkGreen` : ...dark green;
- `darkBlue` : ...dark blue;
- `black` : ...black.

To use one simply specify the module name and value name, e.g. `BackgroundStrategy.black`.

(The above values are just `SpecificColour` strategies with a chosen colour, nothing more than that.)

## Discriminated Union Identity Values

Because backgrounds are added after the generation of the design, no functions are available for converting to and from POCO types and DU cases. 

## Exception-free Processing

No functions have exception-free versions.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.