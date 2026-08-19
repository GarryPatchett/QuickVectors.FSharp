# QuickVectors.Export.Svg.FSharp

# Svg Export Settings

These types let you define how the design will be exported to an SVG.

- The [Svg Export Transform Format Type](#the-export-transform-format-type)
- The [Svg Export Colour Format Type](#the-export-colour-format-type)
- The [Svg Export Invisibility Policy Type](#the-export-invisibility-policy-type)
- The [Svg Export Settings Type and Module](#the-svg-export-settings-type)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

> **Note:** It is likely that some of these settings will change, or be renamed, or be replaced over time so it is
recommended that you check the release notes as appropriate.

## The Svg Export Transform Format Type

The `SvgExportTransformFormat` **type** defines a discriminated union used to specify how transformations will be expressed upon export.

The cases are:

| Case Name                 | Description                                                               |
| ------------------------- | ------------------------------------------------------------------------- | 
| **VerboseTransform**      | Express each transformation in full                                       |
| **MatrixTransform**       | Express all the transformations as a single matrix transform              |

To specify a setting simply supply its name, such as `SvgExportTransformFormat.VerboseTransform`.

An example of a verbose transform is: `transform="translate(50 50) rotate(15.266 0 0) scale(83.253 83.253)"`

An example of a matrix transform is: `transform="matrix(78.9929 14.892 -14.892 78.9929 50 50)"`

## The Svg Export Colour Format Type

The `SvgExportColourFormat` **type** defines a discriminated union used to specify how colours will be expressed upon export.

The cases are:

| Case Name                 | Description                                                               |
| ------------------------- | ------------------------------------------------------------------------- | 
| **ExportColoursAsRgb**    | Express each colour as an RGB colour with decimal components              |
| **ExportColoursAsHex**    | Express each colour as a single hex string containing all components      |

To specify a value modification simply supply its name, such as `SvgExportColourFormat.ExportColoursAsRgb`.

An example of a decimal colour is: `fill="rgb(255,23,182)"`

An example of a hex colour string is: `fill="#7BFF00"`

## The Svg Export Invisibility Policy Type

The `SvgExportInvisibilityPolicy` **type** defines a discriminated union used to specify whether invisible elements will be expressed upon export.

The cases are:

| Case Name                     | Description                                                           |
| ----------------------------- | --------------------------------------------------------------------- | 
| **ExportInvisibleElements**   | Export all elements even if they will be invisible                    |
| **OmitInvisibleElements**     | Only export the elements which will be visible                        |

To specify a setting simply supply its name, such as `SvgExportInvisibilityPolicy.ExportInvisibleElements`.

An invisible element is one which has `Colour.noColour` as both its fill and stroke colour.

## The Svg Export Settings Type

The `SvgExportSettings` **type** defines a record used to specify the SVG export settings.

The fields are:

| Field Name                | Required Type                     |
| ------------------------- | --------------------------------- | 
| **TransformFormat**       | SvgExportTransformFormat          |
| **ColourFormat**          | SvgExportColourFormat             |
| **InvisibilityPolicy**    | SvgExportInvisibilityPolicy       |

An example of a settings record is as follows:

```fsharp 
let settings =
    { ColourFormat = SvgExportColourFormat.ExportColoursAsRgb
      TransformFormat = SvgExportTransformFormat.VerboseTransform
      InvisibilityPolicy = SvgExportInvisibilityPolicy.ExportInvisibleElements }
```

The settings in the code above are those which define the standard settings as mentioned below.

## The Svg Export Settings Module

The `SvgExportSettings` **module** defines a single value which contains the standard export settings.

You can use this by specifying `SvgExportSettings.standard`.

It is recommended that you use these standard settings, simply for convenience, unless you need to use different settings.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.