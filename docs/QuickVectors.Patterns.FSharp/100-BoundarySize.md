# QuickVectors.Patterns.FSharp

# Boundary size

This type lets you specify the size of a boundary of some patterns.

- The [Boundary Size Type](#the-boundary-size-type)
    - [Limits](#limits)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
    - [Code Examples](#code-examples)
    - [Ready-made Boundary Sizes](#ready-made-boundary-sizes)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Boundary Size Type 

The `BoundarySize` **type** defines the size of a boundary of a pattern.

### Construction

A boundary size can be created via various functions:

- `fromSingleFloat` : The boundary size will be created with **both** the width and height equal to the value provided;
- `fromFloats` : The boundary size will be created with the width and height equal to the values provided;
- `fromSingleDimension` : The boundary size will be created with **both** the width and height equal to the dimension provided;
- `fromDimensions` : The boundary size will be created with the width and height equal to the dimensions provided.

When one or more floats are provided the values will be clamped to the `minimum` and `maximum` (inclusive) of
the [BoundaryDimension](090-BoundaryDimension.md "The BoundaryDimension type and module") type.

When one or more dimensions are provided then those values will be used directly.

When a boundary size is printed to the screen the output will be `Boundary(w,h)` where `w` is the boundary width
and `h` is the boundary height. For example, a boundary size defined as a width of 500.0 and a height of 800.0
with `BoundarySize.fromFloats 500.0 800.0` will be printed as `Boundary(500.0,800.0)`.

> **Note:** When a pattern needs a boundary size the origin of the pattern will always be
at 0,0 which is at the top-left with positive horizontal values going right and positive vertical values going downwards,
and the shapes will usually be within the boundary (some shapes - e.g. Squiggle - might extend beyond this and the stroke of some shapes may also, in some circumstances, extend beyond the boundary).

### Deconstruction

The deconstruction functions are:

- `width` : Returns the width of the boundary size;
- `height` : Returns the height of the boundary size.

### Variations

There are no functions for varying the values of the fields but you can, since all field values are type-checked and valid,
change the values in the same way as you would with any F# record.  
For example: `let newRecord = { oldRecord with FieldName = newValue }`.

### Code Examples

```fsharp 
let byFloats = 
    BoundarySize.fromFloats 500.0 800.0 
    // -> Boundary(500.0,800.0)

let width = BoundaryDimension.fromFloat 700.0 // -> BoundaryDim(700.0)
let height = BoundaryDimension.fromFloat 400.0 // -> BoundaryDim(400.0)

let byDimensions = 
    BoundarySize.fromDimensions width height 
    // -> Boundary(700.0,400.0)
```

### Ready-made Boundary Sizes

Various ready-made boundary sizes are available, and these are:

- `minimum` : A boundary with the minimum size;
- `thousandByThousand` : A boundary of 1000x1000 (a good default to use if you don't have specific needs);
- `twoThousandByTwoThousand` : A boundary of 2000x2000;
- `fullHighDefinition` : A boundary with the size of Full HD (landscape);
- `quadHighDefinition` : A boundary with the size of Quad HD (landscape);
- `ultraHighDefinition` : A boundary with the size of Ultra HD (landscape);
- `maximum` : A boundary with the maximum size.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.