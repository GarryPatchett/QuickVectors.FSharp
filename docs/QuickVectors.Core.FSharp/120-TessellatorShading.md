# QuickVectors.Core.FSharp

# Tessellator Shading Policy

Defines a tessellator shading policy which can be used with a tessellator.

- The [Tessellator Shading Policy Type](#the-tessellator-shading-policy-type)
- [Discriminated Union Identity Values](#discriminated-union-identity-values)
- [Exception-free Processing](#exception-free-processing)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Tessellator Shading Policy Type

The `TessellatorShadingPolicy` **type** defines a discriminated union used to specify the tessellator shading policies.

The cases are:

| Case Name                     | Description                                                           |
| ----------------------------- | --------------------------------------------------------------------- | 
| **ApplyShading**              | Shading will be applied                                               |
| **ReplaceColour**             | The colours will be replaced by the tessellator shading               |

When a tessellator is comprised of only one shape, no shading is applicable.

When a tessellator is comprised of more than one shape, the more shapes there are the more shading will be applied.

For example, the Isocubes tessellator is comprised of three quadrilaterals. The 'top' of the cube will not be shaded, the
left-hand 'side' will be shaded a little bit, and the right-hand 'side' will be shaded more. In this instance it
gives the impression that the cubes are '3D' with lighting coming from the top-left.

This is easier to understand when it's seen in practice than it is to describe it.

To specify a tessellator shading policy simply supply its name, such as `TessellatorShadingPolicy.ApplyShading`.

## Discriminated Union Identity Values

Functions are available for converting to and from POCO types and DU cases.
See the Overview documentation for more information about these.

For the type described above there is no `defaultCase` value.

## Exception-free Processing

Exception-free processing versions - Option and Result - of some functions are available.
See the Overview documentation for more information about these.

For the type described above there is no `FailSafe.fromInt` function and it is recommended
that you use the `Option.fromInt` function instead.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp)* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.
