# QuickVectors.Patterns.FSharp

# Frames

A design can have one or more frames generated around it which can make it easier to align it with other things.

- The [Frame Stroke Width Type](#the-frame-stroke-width-type)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
- The [Frame Definition Type](#the-frame-definition-type)
    - [Ready-made Frame Definitions](#ready-made-frame-definitions)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

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

A frame is simply a non-filled rectangle with a stroke of the colour and width specified.

You define a frame definition by supplying a colour and a frame stroke width, such as:

```fsharp 
let frameDefinition = 
    {   FrameDefinition.Colour = Colour.brightRed 
        StrokeWidth = FrameStrokeWidth.fromFloat 1.0 }
```

While some of the 'footprint' of the frame stroke might be outside of the boundary/extent of the
pattern - half could be inside and half outside - the centre of the stroke itself is centred
on that boundary/extent.

### Ready-made Frame Definitions

Two ready-made frame definitions are available:

- `FrameDefinition.boundaryFrame` : Has a blue-ish stroke with a stroke width of 4.0;
- `FrameDefinition.extentsFrame` : Has a purple-ish stroke with a stroke width of 4.0.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.