# QuickVectors.FSharp 

This is the public repository for the QuickVectors.FSharp packages.

## Contents

- [Overview](#overview)
- [Learning](#learning)
- [Questions and Reporting Issues](#questions-and-reporting-issues)
- [Usage](#usage)

## Overview

This QuickVectors.FSharp project contains four packages:

| Package                           | What It's For                                                     |
| --------------------------------- | ----------------------------------------------------------------- |
| **QuickVectors.Core.FSharp**      | Contains shared types and functionalities                         |
| **QuickVectors.Elements.FSharp**  | Contains types and functionality normally only used internally    |
| **QuickVectors.Patterns.FSharp**  | Create designs from patterns of shapes                            |
| **QuickVectors.Export.FSharp**    | Export designs (currently only to SVG)                            |

You are not expected to install the first three packages manually but should install the `Export` package instead
which will install all of the packages together at the same time.

Once you have installed the `Export` package you can quickly generate patterns and export them to SVG documents.

The documentation for the `Core` package will be very useful when creating patterns.

The documentation for the `Patterns` package can be referred to when creating designs from patterns.

There is no user documentation for the `Elements` package as you would not normally use the contents manually.

The documentation for the `Export` package tells you how to export designs.

Various types and modules are provided and the documentation for such can be found in the
documentation for the relevant package.

The documentation files for each package have a numerical prefix and are ordered in such
a way that it would be beneficial to the reader if they read them in ascending order of this numerical prefix,
but you can dip in to whichever part of the documentation you want to read at any time.

There is no code in this repository as the software is not open source. You can install and use the packages pretty
much anywhere you like but the code is **NOT** yours to view, modify, or make derivatives of.
See the "licence.md" file for each package for more information.

## Learning

The packages in this project contain a lot of types and modues and trying to understand them all before trying
to do anything with them would be a difficult task.

Because of this it is recommended that you read the short tutorial (in the TUTORIAL.md file) first so that you
can get used to how to use some of the various functionalities in a step-by-step fashion.

There's nothing particularly complicated in these packages but the shear amount of 'stuff' to learn can
be daunting so learning things bit-by-bit should make for a more comfortable process.

## Questions and Reporting Issues

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp)* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.

> **Note:** I don't visit GitHub regularly so it may take some time for you to get a response.

## Usage

The types and functions in these packages have been designed to be used only with F#.

However, they may also be usable with C# but this has not been tested, so use them with C# at your own risk.
