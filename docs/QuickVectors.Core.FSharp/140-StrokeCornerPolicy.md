# QuickVectors.Core.FSharp

# Stroke Corner Policy

Defines how the corners between segemnts of a line/path are joined

- The [Corner Policy Type](#the-stroke-corner-policy-type)
- [Discriminated Union Identity Values](#discriminated-union-identity-values)
- [Exception-free Processing](#exception-free-processing)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Stroke Corner Policy Type

The `StrokeCornerPolicy` **type** defines a discriminated union used to specify how the corners between segemnts of a line/path are joined

The cases are:

| Case Name                     | Line/Path is Joined With                      |
| ----------------------------- | --------------------------------------------- |
| **ArcsCorners**               | An arcs corner **1*                           |
| **BeveledCorners**            | A flat beveled corner                         |
| **MiteredCorners** **2*       | A sharp mitered corner (sometimes) **3*       |
| **ClippedMiterCorners**       | A sharp mitered corner (sometimes) **1* **3*  |
| **RoundCorners**              | A round corner                                |

- **1* : These might not be drawn properly by certain user agents (browsers, etc.) when exported.
- **2* : The default case.
- **3* : When exporting, the default miter limit will be used and this can cause a different result
under different circumstances.

To specify a corner policy simply supply its name, such as `StrokeCornerPolicy.RoundCorners`.

Some shapes will look better with a certain corner policy so it's best to experiment to see which is more
to your taste depending on your circumstances. (You can use the `Sample.RollCall.shapes` function in the Export
package to generate samples of the shapes with different corner policies to see which works best for you.)

Some shapes which are drawn with paths - e.g. the cards suits - override your choice of policy because they
look best using a particular policy. All of the Pane pattern shapes currenty override the corner policy.

The ready-made stroke definitions use `StrokeCornerPolicy.RoundCorners` by default as that looks nice for most shapes.

See [here](https://developer.mozilla.org/en-US/docs/Web/SVG/Reference/Attribute/stroke-linejoin) for more information about
line joins in SVG files.

## Discriminated Union Identity Values

Functions are available for converting to and from POCO types and DU cases.
See the [overview documentation](000-Overview.md "Package overview") for more inpolicyation about these.

## Exception-free Processing

Exception-free processing versions - FailSafe, Option, and Result - of some functions are available.
See the [overview documentation](000-Overview.md "Package overview") for more inpolicyation about these.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.