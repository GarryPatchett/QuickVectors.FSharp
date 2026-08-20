# QuickVectors.FSharp 

This is the public repository for the QuickVectors.FSharp packages.

Together these packages allow you to quickly create procedurally-generated vector designs like those shown below, often with very little code.

![Mixed Examples Image](/images/Mixed-Examples.png "Mixed Examples")

## Contents

- [Overview](#overview)
- [Learning](#learning)
- [Questions and Reporting Issues](#questions-and-reporting-issues)
- [Usage](#usage)

## Overview

This QuickVectors.FSharp project contains four packages:

| Package                           | What It's For | Documentation | Package |
| --------------------------------- | ------------- | ------------- | ------- |
| **QuickVectors.Core.FSharp**      | Contains shared types and functionalities | [Core docs](docs/QuickVectors.Core.FSharp/000-Overview.md "Core package documentation") | [Core package](https://www.nuget.org/packages/QuickVectors.Core.FSharp "Core package") |
| **QuickVectors.Elements.FSharp**  | Contains types and functionality normally only used internally | N/A | [Elements package](https://www.nuget.org/packages/QuickVectors.Elements.FSharp "Elements package") |
| **QuickVectors.Patterns.FSharp**  | Create designs from patterns of shapes | [Patterns docs](docs/QuickVectors.Patterns.FSharp/000-Overview.md "Patterns package documentation") | [Patterns package](https://www.nuget.org/packages/QuickVectors.Patterns.FSharp "Patterns package") |
| **QuickVectors.Export.FSharp**    | Export designs (currently only to SVG) | [Export docs](docs/QuickVectors.Export.FSharp/000-Overview.md "Export package documentation") | [Export package](https://www.nuget.org/packages/QuickVectors.Export.FSharp "Export package") |

You are not expected to install the first two packages manually but should install the `Patterns` and `Export` packages instead
which will install everything that is necessary.

Once you have installed the `Patterns` and `Export` packages you can quickly generate patterns and export them to SVG documents.

The documentation for the `Core` package [here](docs/QuickVectors.Core.FSharp/000-Overview.md "Core package documentation") contains very useful general information.

The documentation for the `Patterns` package [here](docs/QuickVectors.Patterns.FSharp/000-Overview.md "Patterns package documentation") can be referred to when creating patterns.

The documentation for the `Export` package [here](docs/QuickVectors.Export.FSharp/000-Overview.md "Export package documentation") tells you how to export designs.

There is no user documentation for the `Elements` package as you would not normally use the contents manually. (The contents of this package might eventually become unavailable to developers.)

Various types and modules are provided in the packages and the documentation for such can be found in the
documentation for the relevant package.

The documentation files for each package have a numerical prefix and are ordered in such
a way that it would be beneficial to the reader if they read them in ascending order of this numerical prefix,
but you can dip in to whichever part of the documentation you want to read at any time.

There is no code in this repository as **the software is not open source**. You can install and use the packages pretty
much anywhere you like but the code is **NOT** yours to view, modify, or make derivatives of.
See the "licence.md" file for each package to get more information.

## Learning

The packages in this project contain a lot of types and modues and trying to understand them all before trying
to do anything with them would be a difficult task.

Because of this it is recommended that you read the [short tutorial](TUTORIAL.md "Project tutorial") (in the "TUTORIAL.md" file) first so that you
can get used to how to use some of the various functionalities in a step-by-step fashion.

There's nothing particularly complicated in these packages but the shear amount of 'stuff' to learn can
be daunting so learning things bit-by-bit should make for a more comfortable process.

## Questions and Reporting Issues

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.

> **Note:** I don't visit GitHub regularly so it may take some time for you to get a response.

## Usage

The types and functions in these packages have been designed to be used only with F#.

However, they may also be usable with C# but this has not been tested, so use them with C# at your own risk.