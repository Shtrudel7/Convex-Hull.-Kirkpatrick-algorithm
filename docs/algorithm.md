# Kirkpatrick–Seidel: algorithm notes

## Core idea

Unlike algorithms that sort all input points, Kirkpatrick–Seidel constructs the hull using an output-sensitive divide-and-conquer strategy known as **marriage-before-conquest**.

1. Identify the leftmost and rightmost candidate endpoints of the upper chain.
2. Split candidate points by a vertical line through the median x-coordinate.
3. Find an upper bridge: a supporting segment crossing the median line.
4. Filter candidates that cannot lie on the two remaining upper-hull subproblems.
5. Recursively construct both subchains and combine them.
6. Reflect the input across the x-axis to compute the lower chain, then merge chains.

A correct linear-time bridge finder relies on point pairing, slope selection, and safe candidate elimination. The notebook implements a bridge routine and a `QuickSelect` helper; a complete proof of its implementation-level complexity and correctness is outside the present project scope.

## Complexity

The **original algorithm** requires $O(n\log h)$ time and $O(n)$ space, where $h$ is the number of vertices on the final hull. The exact Wolfram notebook code has not been benchmarked or proven to achieve these bounds.

## Suggested tests

- Three non-collinear points; triangular hull.
- Four points of a rectangle, with additional interior points.
- Duplicate input points.
- Points that share the same x-coordinate.
- Collinear point clouds and repeated hull-edge points.
- Points outside $[-1,1]$ to verify plot limits.
- Randomly generated point sets, compared with a trusted hull implementation.

**Note:** some of these cases may reveal bugs; they are regression-test suggestions rather than passed test results.

## Source

Kirkpatrick, D. G., and Seidel, R. (1986). *The Ultimate Planar Convex Hull Algorithm?* SIAM Journal on Computing, 15(1), 287–299. https://doi.org/10.1137/0215021
