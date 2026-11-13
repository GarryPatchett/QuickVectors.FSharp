# QuickVectors.Export.Svg.FSharp

# Svg Export Settings

These types let you define how the design will be exported to an SVG.

- The [Xml Encoding Type](#the-xml-encoding-type)
- The [Svg Version Type](#the-svg-version-type)
- The [Svg Export Element Identification Policy Type](#the-svg-export-element-identification-policy-type)
- The [Svg Export Transform Format Type](#the-export-transform-format-type)
- The [Svg Export Colour Format Type](#the-export-colour-format-type)
- The [Svg Export Invisibility Policy Type](#the-export-invisibility-policy-type)
- The [Svg Export Opacity Policy Type](#the-svg-export-opacity-policy-type)
- The [Svg Export Opacity Format Type](#the-svg-export-opacity-format-type)
- The [Svg Export Default Attribute Policy Type](#the-svg-export-default-attribute-policy-type)
- The [Svg Export Grouping Policy Type](#the-svg-export-grouping-policy-type)
- The [Svg Export Settings Type](#the-svg-export-settings-type)
- The [Svg Export Settings Module](#the-svg-export-settings-module)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
    - [Ready-made Settings](#ready-made-settings)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

> **Note:** It is likely that some of these settings will change, or be renamed, or be replaced, over time
so it is recommended that you check the release notes as appropriate.

## The Xml Encoding Type

The `XmlEncoding` **type** defines a discriminated union used to specify the XML encoding.

There is currently only one case:

| Case Name                                     | Description                                                               |
| --------------------------------------------- | ------------------------------------------------------------------------- | 
| **Utf8Encoding**                              | Use Utf8 encoding                                                         |

To specify this encoding simply supply its name, such as `XmlEncoding.Utf8Encoding`.

This type has been created to allow for possible future expansion but that might never happen,
so just use the single case as provided.

## The Svg Version Type

The `SvgVersion` **type** defines a discriminated union used to specify the SVG version.

There is currently only one case:

| Case Name                                     | Description                                                               |
| --------------------------------------------- | ------------------------------------------------------------------------- | 
| **OnePointOne**                               | SVG version 1.1                                                           |

To specify this version simply supply its name, such as `SvgVersion.OnePointOne`.

This type has been created to allow for possible future expansion but that might never happen,
so just use the single case as provided.

## The Svg Export Element Identification Policy Type

The `SvgExportElementIdentificationPolicy` **type** defines a discriminated union used to specify whether/how element identification will be expressed upon export.

The cases are:

| Case Name                                     | Description                                                               |
| --------------------------------------------- | ------------------------------------------------------------------------- | 
| **OmitIdentification**                        | Do not identify elements                                                  |
| **UseDesignShapeAsClassIdentification**       | Identify elements by their shape in the design                            |

To specify a format simply supply its name, such as `SvgExportElementIdentificationPolicy.OmitIdentification`.

When identification is omitted, the elements will not be identified by either class or id.

When the design shape is used for identification, the type of the shape created in the design will be used as the class, e.g. `Shape.Rectangle` will be identified as *class="rectangle"*.

## The Svg Export Transform Format Type

The `SvgExportTransformFormat` **type** defines a discriminated union used to specify how transformations will be expressed upon export.

The cases are:

| Case Name                 | Description                                                               |
| ------------------------- | ------------------------------------------------------------------------- | 
| **VerboseTransform**      | Express each transformation in full                                       |
| **MatrixTransform**       | Express all the transformations as a single matrix transform              |

To specify a format simply supply its name, such as `SvgExportTransformFormat.VerboseTransform`.

An example of a verbose transform is: `transform="translate(50 50) rotate(15.266 0 0) scale(83.253 83.253)"`

An example of a matrix transform is: `transform="matrix(78.9929 14.892 -14.892 78.9929 50 50)"`

## The Svg Export Colour Format Type

The `SvgExportColourFormat` **type** defines a discriminated union used to specify how colours will be expressed upon export.

The cases are:

| Case Name                 | Description                                                               |
| ------------------------- | ------------------------------------------------------------------------- | 
| **ExportColoursAsRgb**    | Express each colour as an RGB colour with decimal components              |
| **ExportColoursAsHex**    | Express each colour as a single hex string containing all components      |

To specify a format simply supply its name, such as `SvgExportColourFormat.ExportColoursAsRgb`.

An example of a decimal colour is: `fill="rgb(255,23,182)"`

An example of a hex colour string is: `fill="#7BFF00"`

## The Svg Export Invisibility Policy Type

The `SvgExportInvisibilityPolicy` **type** defines a discriminated union used to specify whether invisible elements will be expressed upon export.

The cases are:

| Case Name                     | Description                                                           |
| ----------------------------- | --------------------------------------------------------------------- | 
| **ExportInvisibleElements**   | Export all elements even if they will be invisible                    |
| **OmitInvisibleElements**     | Only export the elements which will be visible                        |

To specify a policy simply supply its name, such as `SvgExportInvisibilityPolicy.ExportInvisibleElements`.

An invisible element is one which has no colour as both its fill and stroke colour or both the
fill and stroke colours have a minimum (0%) opacity.

## The Svg Export Opacity Policy Type

The `SvgExportOpacityPolicy` **type** defines a discriminated union used to specify *when* opacities will be expressed upon export.

The cases are:

| Case Name                                     | Description                                                               |
| --------------------------------------------- | ------------------------------------------------------------------------- | 
| **AlwaysExpressOpacity**                      | Opacities will always be expressed                                        |
| **OnlyExpressOpacityWhenNotFullyOpaque**      | Opacities will only be expressed when they are not fully-opaque           |

To specify a policy simply supply its name, such as `SvgExportOpacityPolicy.AlwaysExpressOpacity`.

If your design contains no transparency - all colours are fully-opaque - then it's probably
best to use `OnlyExpressOpacityWhenNotFullyOpaque` so that the SVG text is shorter.

## The Svg Export Opacity Format Type

The `SvgExportOpacityFormat` **type** defines a discriminated union used to specify *how* opacities will be expressed upon export.

The cases are:

| Case Name                     | Description                                                                                                   |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------- | 
| **OpacitiesAsPercentages**    | The opacity will be expressed as a percentage between 0% (no opacity, transparent) and 100% (fully-opaque)    |
| **OpacitiesAsDecimals**       | The opacity will be expressed as a number between 0.0 (no opacity, transparent) and 1.0 (fully-opaque)        |

To specify a format simply supply its name, such as `SvgExportOpacityFormat.OpacitiesAsPercentages`.

An example of a percentage fill opacity is: `fill-opacity="50%"`

An example of a decimal stroke opacity is: `stroke-opacity="0.5"`

## The Svg Export Default Attribute Policy Type

The `SvgExportDefaultAttributePolicy` **type** defines a discriminated union used to specify whether default attribute values will be expressed upon export.

The cases are:

| Case Name                                     | Description                                                               |
| --------------------------------------------- | ------------------------------------------------------------------------- | 
| **AlwaysExpressDefaultAttributes** **1*       | Default attributes will always be expressed                               |
| **PreferNoDefaultAttributes**                 | Default attributes will not be expressed where possible                   |

- **1* : The generally recommended policy.

To specify a policy simply supply its name, such as `SvgExportDefaultAttributePolicy.AlwaysExpressDefaultAttributes`.

If an attibute value is the default value - e.g. Miter for *line-join* in a path - then this policy specifies
whether it will be expressed in the SVG or not.

> **Note:** This policy does not apply to some attributes such as *stroke-width* or *color*
(in these cases it is because the default stroke width is 1px but this package doesn't use units of measure,
and the default colour depends on the rendering user agent, e.g. browser, etc.).

## The Svg Export Grouping Policy Type

The `SvgExportGroupingPolicy` **type** defines a discriminated union used to specify whether/how related elements will be grouped upon export.

The cases are:

| Case Name                    | Modifier   | Description                                                               |
| ---------------------------- | ---------- | ------------------------------------------------------------------------- | 
| **NoGroupedElements**        | N/A        | Related elements will NOT be grouped                                      |
| **GroupRelatedElements**     | int **2*   | Related elements WILL be grouped                                          |

- **2* : This value is not validated; large values will look strange in the exported SVG (best to use 1 or 2, but it's your choice).

To specify a policy, supply either:
- `SvgExportGroupingPolicy.NoGroupedElements`, or;
- `SvgExportGroupingPolicy.GroupRelatedElements (IndentSpaces = X)` where `X` is the number of spaces to indent the elements in the group by, or;
- `SvgExportGroupingPolicy.GroupRelatedElements X` where `X` is the number of spaces to indent the elements in the group by.

> **Notes:**
>
> 3. Any frame(s) or background(s) added post-generation will not be grouped.
>
> 4. The design itself is not grouped.
>
> 5. The groups themselves will not have any identification class or id, regardless of the element identification policy choice.
>
> 6. Grouping of related elements only applies to some designs, e.g. the multi-element Tessellators in a Tessellation pattern.

## The Svg Export Settings Type

The `SvgExportSettings` **type** defines a record used to specify the SVG export settings.

The fields are:

| Field Name                    | Required Type                     |
| ----------------------------- | --------------------------------- | 
| **XmlEncoding**               | XmlEncoding                       |
| **SvgVersion**                | SvgVersion                        |
| **TransformFormat**           | SvgExportTransformFormat          |
| **ColourFormat**              | SvgExportColourFormat             |
| **InvisibilityPolicy**        | SvgExportInvisibilityPolicy       |
| **OpacityPolicy**             | SvgExportOpacityPolicy            |
| **OpacityFormat**             | SvgExportOpacityFormat            |
| **DefaultAttributePolicy**    | SvgExportDefaultAttributePolicy   |
| **GroupingPolicy**            | SvgExportGroupingPolicy           |

An example of a settings record is as follows:

```fsharp 
let settings =
    { XmlEncoding = XmlEncoding.Utf8Encoding 
      SvgVersion = SvgVersion.OnePointOne 
      ColourFormat = SvgExportColourFormat.ExportColoursAsRgb
      TransformFormat = SvgExportTransformFormat.VerboseTransform
      InvisibilityPolicy = SvgExportInvisibilityPolicy.ExportInvisibleElements 
      OpacityPolicy = SvgExportOpacityPolicy.OnlyExpressOpacityWhenNotFullyOpaque 
      OpacityFormat = SvgExportOpacityFormat.OpacitiesAsPercentages 
      DefaultAttributePolicy = SvgDefaultAttributePolicy.AlwaysExpressDefaultAttributes 
      GroupingPolicy = SvgExportGroupingPolicy.GroupRelatedElements (IndentSpaces = 2) }
```

The settings in the code above are those which define the standard settings as mentioned below.

## The Svg Export Settings Module

### Construction

There are no construction functions, just create a record as shown above.

### Deconstruction

There are no deconstruction functions for this type.

### Variations 

There are no functions for varying the values of this type; if you need to change the settings then you
can change the field values as you would with any other record.

### Ready-made Settings

The `SvgExportSettings` **module** defines some values which contain ready-made export settings.

These values are:

- `standard` : Basic settings which are generally useful;
- `compact` : Settings which express the design in a (fairly) compact fashion.

You can use a settings value by specifying the module name and value, e.g. `SvgExportSettings.standard`.

It is recommended that you use the standard settings, simply for convenience, unless you have specific requirements.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.