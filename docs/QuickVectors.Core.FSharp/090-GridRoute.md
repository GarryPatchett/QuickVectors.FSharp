# QuickVectors.FSharp

# Grid Route

The ways in which cells in a grid can be visited.

- The [Grid Route Type](#the-grid-route-type)
    - [Processing](#processing)
    - [Code Examples](#code-examples)
- [Discriminated Union Identity Values](#discriminated-union-identity-values)
- [Exception-free Processing](#exception-free-processing)
- [Issues, Questions, and Suggestions](#issues-questions-and-suggestions)

## The Grid Route Type

The `GridRoute` **type** defines a discriminated union used to specify how cells in a grid are visited.

The cases are (in alphabetical order):

| Case Name             | Start         | Transition                                                                    |
| --------------------- | ------------- | ----------------------------------------------------------------------------- |
| **Cascade** **1*      | Top-left      | Left to right; down; left to right; down; left to right; etc.                 |
| **CascadeReversed**   | Bottom-right  | Right to left; up; right to left; up; right to left; etc.                     |
| **Diagonal**          | Top-left      | Diagonal 'stripes' to bottom-right                                            |
| **DiagonalReversed**  | Bottom-right  | Diagonal 'stripes' to top-left                                                |
| **Flow**              | Top-left      | Left to right; down; right to left; down; left to right; etc.                 |
| **FlowReversed**      | Bottom-right  | Right to left; up; left to right; up; right to left; etc.                     |
| **Random**            | Anywhere      | Random order but all cells are visited and each is only visited once          |
| **SpiralIn**          | Top-left      | Top row left to right; Right side downwards; bottom row right to left; etc.   |
| **SpiralOut**         | Centre        | Reverse of SpiralIn                                                           |

- **1* : The default case.

To specify a grid route simply supply its name, such as `GridRoute.Cascade`.

You can see visual examples of the grid routes [here](images/GridRoute-Examples.png "Visual roll call of the available grid routes").

### Processing

A grid route can be used to create a sequence of cell coordinates in a grid of a specified size.

This can be achieved via the function:

- `fromGridSize` : Returns a new sequence of cell coordinates in the grid according to the specified route.

A random number generator is required even if the route chosen has no randomness.

You would normally not need to use this functionality manually but it's there if you need it.

### Code Examples

```fsharp 
let gridSize = GridSize.fromColumnsAndRows 5 3 

let rng = System.Random 9629 // Randomly-chosen seed.
 
let cascade = 
    GridRoute.Cascade 
    |> GridRoute.fromGridSize rng gridSize 
    // -> seq { (0, 0); (1, 0); (2, 0); (3, 0); (4, 0); (0, 1);
    //          (1, 1); (2, 1); (3, 1); (4, 1); (0, 2); (1, 2);
    //          (2, 2); (3, 2); (4, 2) }

let spiralIn = 
    GridRoute.SpiralIn 
    |> GridRoute.fromGridSize rng gridSize 
    // -> seq { (0, 0); (1, 0); (2, 0); (3, 0); (4, 0); (4, 1);
    //          (4, 2); (3, 2); (2, 2); (1, 2); (0, 2); (0, 1); 
    //          (1, 1); (2, 1); (3, 1) }
```

## Discriminated Union Identity Values

Functions are available for converting to and from POCO types and DU cases.
See the [overview documentation](000-Overview.md "Package overview") for more information about these.

## Exception-free Processing

Exception-free processing versions - FailSafe, Option, and Result - of some functions are available.
See the [overview documentation](000-Overview.md "Package overview") for more information about these.

## Issues, Questions, and Suggestions

You can visit the *[QuickVectors.FSharp](https://github.com/GarryPatchett/QuickVectors.FSharp "Home page for the QuickVectors project")* GitHub repository to report issues, 
ask questions, or make suggestions. You can also read about the changes across different versions in the release notes there.