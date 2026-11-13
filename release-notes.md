# QuickVectors.FSharp Release Notes

> **Notes:**
> 
> 1. Changes to the project documentation can be made
as necessary at any time, but they will not normally be noted in these release
notes unless those changes are particularly significant.
>
> 2. Any changes to the Intellisense documentation will be made
as necessary with new releases, but they will not normally be noted in these release
notes unless those changes are significant.
>
> 3. If any package is updated then all of the packages will be updated to the new version number,
whether thay have changed or not. This, hopefully, helps to avoid confusion by having the same version
number across all of the packages in the project at any one time.
>
> 4. Any items deprecated in the current version will remain until at least the next version but they
will usually be removed from the version after that. (E.g. A item deprecated in 0.3.2 will be in 0.3.3 but
not in 0.3.4.)

## Overview

- [0.3.2](#032--) -
    - New chess board pattern;
    - New shapes - Ghost, Cloud, Card Suits, Chess Pieces, etc.;
    - Added limited colour opacity capabilities;
    - Added ability to specify corner type;
    - New colour schemes and standard palettes;
    - Added way to include background(s);
    - New way to include frames;
    - Some related elements can be grouped;
    - Re-written compile/export processing;
    - New Template module;
    - New ready-made patterns;
    - ...and more.
- [0.3.1](#031--) - Abandoned release.
- [0.3.0](#030--) - Initial release.

## 0.3.2 - 

(QuickVectors.FSharp 0.3.1 was not released because of problems with QuickData.FSharp 0.3.1, thus the 'jump' to 0.3.2.)

### General

- Changed some code to use functions from QuickData.FSharp 0.3.2 rather than internal code.

### Core Package 

- **VERY IMPORTANT:** Changed `Shape` **type**:
    - The way in which you specify shapes has changed considerably from that in 0.3.0. This change was necessary to
        accommodate new shapes in a more organised way than previously. Extra types have been added to
        allow for this new organisation.

        Rather than specifying, for example, `Shape.RectanglePath` in 0.3.0 you can now specify the same shape in
        a number of ways, e.g. `Rectangle (Rectangle.Standard AsPath)`, or `Shape.Rectangle.standardAsPath`.

        See the documentation for the `Shape` type for more information and examples.

    - Added new shapes:
        - Items - `Gemstone`, `Cloud`;
        - Creatures - `Alien`, `Ghost`;
        - Binary - `Correct`,`Incorrect`;
        - Card Suits - `Spades`, `Clubs`, `Hearts`, `Diamonds`, and `Random`;
        - Chess Pieces - `Pawn`, `Knight`, `Bishop`, `Rook`, `Queen`, `King`, and `Random`.
    
        The new shapes can be seen in the relevant sample (see other documentation).

- Added `StrokeCornerPolicy` **type** and **module** to specify, in a stroke definition, how line/path sements are joined.

- Added `OpacityPercentage` **type** and **module**:
    - New type and module necessary for handling opacities (transparency).

- Added `Opacity` **type** and **module**:
    - New type and module necessary for handling opacities (transparency).

- Changed `Colour` **type** and **module**:
    - Added new field to `Colour` for Opacity;
    - Added new functions to handle extracting the opacity from a colour;
    - Added new ready-made colours:
        - `midRed`, `midGreen`, `midBlue` : mid-range colours;
        - `darkRed`, `darkGreen`, `darkBlue` : dark colours.

    Opacity specification/variation is currently only possible via design generation;
    at present you can **only** manually create colours which are fully-opaque.

- Added new `ColourScheme` cases:
    - `GreyscaleLinearBounceSingleHigh` : Like linear bounce but only one high value is generated;
    - `GreyscaleLinearBounceShort` : Like linear bounce single high but the sequence ends before the final low value;
    - `RandomColourBetween` : Generate colours by choosing their components from the component ranges of the specified colours.

- Added some new palettes to `StandardPalette.FiveShades` and `StandardPalette.SevenShades` for
    lighter shades of grey.

### Elements Package 

Extensive re-write with many changes, but since no-one should be using the things in here
(as mentioned in the project README.md file), other than the `Sample` **module** and the
new `Template` **module** (as mentioned in the Export Package release notes below),
that shouldn't be a problem.

### Patterns Package 

- Added `ChessBoard` **type** and **module**, and other related types/modules, to create different chess board position patterns.

Some pattern fields and functions - those for frames - are deprecated; see the documentation for each pattern for more information.

- Changed `ShapeGrid` **module**:
    - Added `withBackground` function;
    - Added `withBoundaryFrame` function;
    - Added `withExtentsFrame` function.
- Changed `Scatter` **module**:
    - Added `withBackground` function;
    - Added `withBoundaryFrame` function.
- Changed `Tessellation` **module**:
    - Added `withBackground` function;
    - Added `withBoundaryFrame` function.
- Changed `Centric` **module**:
    - Added `withBackground` function;
    - Added `withBoundaryFrame` function.
    - Added `withExtentsFrame` function.
- Changed `Pane` **module**:
    - Added `withBackground` function;
    - Added `withBoundaryFrame` function.

    The `withBackground` functions allow a coloured background to be added to the design after generation.
    
    The `withBoundaryFrame` function is the new way to add a boundary frame.
   
    The `withExtentsFrame` function is the new way to add an extents frame (where applicable).

- Changed `StrokeDefinition` **type** and **module**:
    - Added `CornerPolicy` field to specify how line/path segements are joined;
    - Added `withCornerPolicy` function to change the corner policy.

- Some elements in some designs can be grouped upon export (see Export package documentation).

- Changed expected parameters for some `Sample.RollCall` functions.

- Added some new ready-made patterns:
    - `ShapeGrid.cardSharp`
    - `Scatter.alienAttack`
    - `Scatter.cloudySkies`

- Changed the `Scatter.confetti` ready-made pattern to make it look more interesting.

### Export Package 

Extensive re-write of the SVG generation functionality but usage should remain as
before except for the items mentioned below.

The generated SVG code will be slightly different but it will, hopefully, be better than it was in previous versions.
For example, when there is no stroke, no stroke attributes will be expressed other than *stroke="none"*.

- Added `XmlEncoding` **type**:
    - New type to specify how the XML will be encoded (currently only one case).
- Added `SvgVersion` **type**:
    - New type to specify the version of the SVG that will be generated (currently only one case).
- Added `SvgExportElementIdentificationPolicy` **type**:
    - New type to specify whether/how element identification will be expressed.
- Added `SvgExportOpacityPolicy` **type**:
    - New type to specify *when* opacities will be expressed.
- Added `SvgExportOpacityFormat` **type**:
    - New type to specify *how* opacities will be expressed.
- Added `SvgExportDefaultAttributePolicy` **type**:
    - New type to specify whether default attributes should be expressed.
- Added `SvgExportGroupingPolicy` **type**:
    - New type to specify whether/how relatd elements will be grouped.
- Changed `SvgExportSettings` **type** and **module**:
    - Added fields for the types listed above;
    - Added `compact` ready-made settings for smaller SVG output.

- Added `Template` **module** which provides templates for creating collective designs (only one at the moment).

- Changed the `Linear.Plus` (was `LinePlus`) and `Linear.Cross` (was `LineCross`) shapes to each express as a single *path* element rather than two *line* elements.

- Changed the `Svg.compile` function which now creates an `SvgDocument` type instead of strings.
This new type holds all of the information necessary to create the SVG file. (As with previous versions, it is recommended
that you do not manually alter the information in this type but you can do so at your own risk.)

## 0.3.1 - 

- Was never released due to problems with QuickData.FSharp 0.3.1.

## 0.3.0 - 

- Initial release. Started at version 0.3.0 to make the version numbers equal across
both the QuickData.FSharp and QuickVectors.FSharp projects.