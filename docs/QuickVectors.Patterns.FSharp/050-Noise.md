# QuickVectors.Patterns.FSharp

# Noise

A noise determines how much the values in a sequence can be varied in a (semi-)natural way.

- The [Noise Type](#the-noise-type)
- The [Noise Module](#the-noise-module)
    - [Processing Functions](#processing-functions) with [code examples](#processing-code-examples)
- [Discriminated Union Identity Values](#discriminated-union-identity-values)
- [Exception-free Processing](#exception-free-processing)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

> See the `QuickData.Core.FSharp` [documentation](https://www.nuget.org/packages/QuickData.Core.FSharp "QuickData.Core.FSharp package documentation") for more information about the Normal type.
>
> See the `QuickData.Numbers.FSharp` [documentation](https://www.nuget.org/packages/QuickData.Numbers.FSharp "QuickData.Numbers.FSharp package documentation") for more information about Normal sequences and the NaturalVarianceDegree type.

## The Noise Type

The `Noise` **type** defines a discriminated union for noises to be used when modifying a sequence of generated values.

Each noise applies a modification to a different extent.

The cases are:

| Case Name **1*   | Colour **2*   | NaturalVarianceDegree **3*     | Amount **4* |
| ---------------- | ------------- | ------------------------------ | ----------- |
| Least            | Red           | Lowest                         | +/- 0.035   |
| Less             | Pink          | Low                            | +/- 0.06    |
| Moderate         | White         | Medium                         | +/- 0.17    |
| More             | Blue          | High                           | +/- 0.48    |
| Most             | Violet        | Highest                        | +/- 0.74    |

- **1* : The name of the DU case, e.g. `Noise.Least`.
- **2* : The (roughly) equivalent noise colour, e.g. Moderate is roughly equivalent to white noise.
- **3* : The `NaturalVarianceDegree` equivalent of the noise.
- **4* : The approximate maximum/minimum amount that a value can vary for the noise.

To specify a noise simply supply its name, such as `Noise.Moderate`.

## The Noise Module

The `Noise` **module** provides functions for use with profiles.

### Processing Functions 

The processing functions provided are:

- `apply` : Generate a sequence of noise and apply each element of noise to an element of the original sequence, producing a new sequence.

While you wouldn't normally need to apply noise manually - it's better to do that via a pattern - you can do so if you wish.

#### Processing Code Examples

```fsharp 
let rng = System.Random 4981 // Randomly-chosen seed.

let count = 20 

// The 'originals' sequence is infinite but the output is truncated
//  by applying a finite-length sequence of noise.

let originals = Normal.Seq.repeated Normal.oneHalf 
    // -> seq { 0.5 ; 0.5 ; 0.5 ; 0.5 ; etc. }

let withAppliedNoise = 
    originals
    |> Noise.apply rng Noise.Moderate count 
    |> Normal.Seq.toFloats
    // -> e.g. seq { 0.5530727781; 0.5803393935; 0.5876198862; 
    //               0.522633375;  0.4379422238; 0.4537525399; 
    //               0.5561603738; 0.5958381516; 0.5238833654; 
    //               0.4675686823; 0.5216973191; 0.6038778358; 
    //               0.5884361274; 0.4923751669; 0.4448646161;
    //               0.5035057362; 0.5797035295; 0.5698295569; 
    //               0.4967456268; 0.4584312788 }
```

> **Note:** Because the generated noise values always start at 0.0 it is suggested that you generate
more noise values than you need and then skip the number of extra values to get a more 'natural-looking'
sequence of noise values (this is done automatically when generating noises via a pattern).

## Discriminated Union Identity Values

Functions are available for converting to and from POCO types and DU cases.
See the [overview documentation](000-Overview.md "Package overview") for more information about these.

For the type described above there is no `defaultCase` value.

## Exception-free Processing

Exception-free processing versions - Option and Result - of some functions are available.
See the [overview documentation](000-Overview.md "Package overview") for more information about these.

For the type described above there is no `FailSafe.fromInt` function and it is recommended
that you use the `Option.fromInt` function instead.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.