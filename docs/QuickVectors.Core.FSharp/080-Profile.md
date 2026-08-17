# QuickVectors.FSharp

# Profile

A profile determines the 'shape' of a sequence of values.

- The [Profile Type](#the-profile-type)
- The [Profile Module](#the-profile-module)
    - [Generation Functions](#generation-functions) with [code examples](#generation-code-examples)
- [Discriminated Union Identity Values](#discriminated-union-identity-values)
- [Exception-free Processing](#exception-free-processing)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

> See the `QuickData.Core.FSharp` [documentation](https://www.nuget.org/packages/QuickData.Core.FSharp "QuickData.Core.FSharp package documentation") for more information about the Normal type.
>
> See the `QuickData.Numbers.FSharp` [documentation](https://www.nuget.org/packages/QuickData.Numbers.FSharp "QuickData.Numbers.FSharp package documentation") for more information about Normal sequences.

## The Profile Type

The `Profile` **type** defines a discriminated union for profiles to be used when generating a sequence of values.

Each profile creates a sequence of values with a different 'shape'.

Profiles are used in many areas such as shape size generation, geometry modification, rotation, etc.
Because of this it is recommended that you take the time to understand what each sequence produces (most of them are fairly self-explanatory).

The cases are:

| Case Name **1*           | Normal.Seq Sequence **2*                         |
| ------------------------ | ------------------------------------------------ |
| **Random** **3*          | random                                           |
| **LowValue**             | repeatedMinimum                                  |
| **OneThird**             | repeatedOneThird                                 |
| **OneHalf**              | repeatedOneHalf                                  |
| **TwoThirds**            | repeatedTwoThirds                                |
| **HighValue**            | repeatedMaximum                                  |
| **Linear**               | byEquation NormalEquation.Linear                 |
| **LinearBounce**         | linearBounce                                     |
| **Alternating**          | alternatingMinimumMaximum                        |
| **QuarterPipe**          | byEquation NormalEquation.QuarterPipe            |
| **HockeyStick**          | byEquation NormalEquation.HockeyStick            |
| **SkiSlope**             | byEquation NormalEquation.SkiSlope               |
| **Bump**                 | byEquation NormalEquation.Bump                   |
| **SineWave**             | byEquation NormalEquation.SineWave               |
| **CosineWave**           | byEquation NormalEquation.CosineWave             |
| **BellMediumMiddle**     | bell BellShape.Medium BellPosition.Middle        |
| **EaseSineIn**           | byEquation NormalEquation.EaseSineIn             |
| **EaseSineOut**          | byEquation NormalEquation.EaseSineOut            |
| **EaseSineInOut**        | byEquation NormalEquation.EaseSineInOut          |
| **EaseCubicIn**          | byEquation NormalEquation.EaseCubicIn            |
| **EaseCubicOut**         | byEquation NormalEquation.EaseCubicOut           |
| **EaseCubicInOut**       | byEquation NormalEquation.EaseCubicInOut         |
| **EaseBounceIn**         | byEquation NormalEquation.EaseBounceIn           |
| **EaseBounceOut**        | byEquation NormalEquation.EaseBounceOut          |
| **EaseBounceInOut**      | byEquation NormalEquation.EaseBounceInOut        |

- **1* : The name of the DU case, e.g. `Profile.Linear`.
- **2* : The `Normal.Seq` functionality which is used to generate the values. See the relevant `QuickData.Numbers.FSharp` documentation for more information.
- **3* : The default case.

To specify a profile simply supply its name, such as `Profile.Linear`.

You can see visual examples of the profiles [here](images/Profile-Examples.png "Visual roll call of the available profiles").

## The Profile Module

The `Profile` **module** provides functions for use with profiles.

### Generation Functions 

The generation functions provided are:

- `generateNormals` : Generate a sequence of Normals which conform to the 'shape' of the profile.

#### Generation Code Examples

```fsharp 
let rng = System.Random 4981 // Randomly-chosen seed.

let linearUp = 
    Profile.LinearUp 
    |> Profile.generateNormals rng 20 
    // -> seq { N0.0; N0.05263157895; N0.1052631579; N0.1578947368; N0.2105263158;
    //          N0.2631578947; N0.3157894737; N0.3684210526; N0.4210526316; N0.4736842105;
    //          N0.5263157895; N0.5789473684; N0.6315789474; N0.6842105263; N0.7368421053;
    //          N0.7894736842; N0.8421052632; N0.8947368421; N0.9473684211; N1.0}

let sineWave = 
    Profile.SineWave 
    |> Profile.generateNormals rng 20 
    // -> seq { N0.5; N0.6623497346; N0.8071063563; N0.9185832391; N0.984700133;
    //          N0.9982922465; N0.9578866633; N0.8678619553; N0.7379736965; N0.5822972951;
    //          N0.4177027049; N0.2620263035; N0.1321380447; N0.04211333667;
    //          N0.001707753497; N0.01529986703; N0.08141676087; N0.1928936437;
    //          N0.3376502654; N0.5}
```

## Discriminated Union Identity Values

Functions are available for converting to and from POCO types and DU cases.
See the [overview documentation](000-Overview.md "Package overview") for more information about these.

## Exception-free Processing

Exception-free processing versions - FailSafe, Option, and Result - of some functions are available.
See the [overview documentation](000-Overview.md "Package overview") for more information about these.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.