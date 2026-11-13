# QuickVectors.Patterns.FSharp

# Frames

A design can have one or more frames which delineate certain areas.

- [General Information](#general-information)
- The [Frame Stroke Width Type](#the-frame-stroke-width-type)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
- The [Frame Definition Type](#the-frame-definition-type)
    - [Ready-made Frame Definitions](#ready-made-frame-definitions)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## General Information

The frames are rectangular paths, non-filled with a coloured stroke of a specified width,
which are drawn to delineate a certain area of the design.

The extents frame will cover all of the possibilities for the design, while the boundary can be smaller.

If the boundary for a particular pattern would be the same size as the extents then the pattern cannot
have an extents frame (there is no function to add one for that pattern).

The frames can be useful when you want to align multiple designs in another graphics application.

While some of the 'footprint' of the frame *stroke* might be outside of the boundary/extent of the
pattern - half could be inside and half outside - the centre of the stroke itself is centred
on that boundary/extent.

The frames are drawn on top of the design, after the shapes in the design - last element(s) in
the exported file - in the order in which they are added in your code.

While it's possible to add multiple frames of the same type to a design it's probably not of much
practical use. (If you think of a use then please tell me on the project's GitHub page.)

## The Frame Stroke Width Type

### Limits

Some values are provided to give the limits of a frame stroke width, and these are:

- `minimum` : Returns the minimum value of a frame stroke width - the lowest value that can be set;
- `maximum` : Returns the maximum value of a frame stroke width - the highest value that can be set.

For example, `FrameWidth.minimum` will return the minimum possible value for a frame stroke width.

These values can be useful in interactive environments where you need to set the limits for a control.

### Construction

A frame stroke width can be created via the `fromFloat` function.

The value will be clamped to the range `minimum` to `maximum` (inclusive).

When a frame stroke width is printed to the screen the output will be `FrameStrokeWidth(w)` where `w` is the width.

### Deconstruction

The internal value of a frame stroke width can be obtained via the `toFloat` function.

### Variations

Frame stroke widths, once constructed, cannot be modified. If you need to use a different value then just create a frame stroke width.

## The Frame Definition Type

A frame definition is a record which defines a frame which can be added to a pattern.

You define a frame definition by supplying a colour and a frame stroke width, such as:

```fsharp 
let frameDefinition = 
    {   FrameDefinition.Colour = Colour.brightRed 
        StrokeWidth = FrameStrokeWidth.fromFloat 1.0 }
```

### Ready-made Frame Definitions

Two ready-made frame definitions are available:

- `FrameDefinition.boundaryFrame` : Has a blue-ish stroke with a stroke width of 4.0;
- `FrameDefinition.extentsFrame` : Has a purple-ish stroke with a stroke width of 4.0.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.