# QuickVectors.FSharp

# Grid Size

This type lets you define the size of a grid, where appropriate.

- The [Grid Size Type](#the-grid-size-type)
    - [Construction](#construction)
    - [Deconstruction](#deconstruction)
    - [Variations](#variations)
    - [Code Examples](#code-examples)
    - [Ready-made Grid Sizes](#ready-made-grid-sizes)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Grid Size Type

The `GridSize` **type** defines the size of a grid which is used by some patterns.

### Limits

Some values are provided to give the limits of a grid size, and these are:

- `minimum` : Returns the minimum number of columns/rows - the lowest value that can be set;
- `maximum` : Returns the maximum number of columns/rows - the highest value that can be set.

For example, `GridSize.minimum` will return the minimum possible number of columns/rows.

These values can be useful in interactive environments where you need to set the limits for a control.

### Construction

The construction functions are:

- `fromColumnsAndRows` : Creates a grid size with the specified number of columns and rows;
- `fromRowsAndColumns` : Creates a grid size with the specified number of rows and columns.

Make sure that you get the number of columns and rows in the correct order for the function being used.
(The functions do the same thing but you have the option of which way round you prefer to supply the dimensions.)

The values for each of the columns and rows are clamped to the range `minimum` to `maximum`.

When a grid size is printed to the screen the output will be `Grid(xC/yR)`, where `x` is the number
of columns and `y` is the number of rows.

The type member `AsDisplayString` is available to get the short display string - as mentioned above - for a grid size.

### Deconstruction

The deconstruction functions are:

- `numberOfColumns` : Returns the number of columns for the grid size;
- `numberOfRows` : Returns the number of rows for the grid size;
- `numberOfCells` : Returns the total number of cells for the grid size (columns multipled by rows).

### Variations

A grid size, once constructed, cannot be modified. If you need to use different values then just create a new grid size.

### Code Examples

```fsharp 
let sixByFour = GridSize.fromColumnsAndRows 6 4 // -> Grid(6C/4R)

let columns = sixByFour |> GridSize.numberOfColumns // -> 6

let rows = sixByFour |> GridSize.numberOfRows // -> 4

let cells = sixByFour |> GridSize.numberOfCells // -> 24
```

### Ready-made Grid Sizes

Various ready-made grid sizes are available, and these are:

- `threeByThree` : Three columns and three rows;
- `fiveByFive` : Five columns and five rows;
- `eightByEight` : Eight columns and eight rows (like a chess board);
- `tenByTen` : Ten columns and ten rows;
- `twelveByOne` : Twelve columns and one row;
- `twelveByTwelve` : Twelve columns and twelve rows.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.