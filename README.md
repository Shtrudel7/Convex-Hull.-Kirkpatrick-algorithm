# Convex Hull — Kirkpatrick–Seidel Algorithm

![Wolfram Language](https://img.shields.io/badge/Language-Wolfram%20Language-DD1100?logo=wolfram&logoColor=white)
![Computational Geometry](https://img.shields.io/badge/Field-Computational%20Geometry-2467A9)

An educational implementation of the **Kirkpatrick–Seidel algorithm** for computing the convex hull of a finite set of points in the plane using **Wolfram Mathematica**.

The implementation demonstrates the *marriage-before-conquest* approach: identify a bridge crossing a vertical median line, discard points that cannot contribute to the hull, and recursively connect the relevant vertices.

## Overview

For a set of planar points $P$, its convex hull is the smallest convex set containing all points in $P$:

$$\operatorname{conv}(P)=\left\{\sum_{i=1}^{n}\lambda_i p_i:\lambda_i\ge 0,\ \sum_{i=1}^{n}\lambda_i=1\right\}. $$

The original Kirkpatrick–Seidel algorithm has an **output-sensitive** worst-case bound of $O(n\log h)$, with $n$ input points and $h$ hull vertices. **This bound describes the theoretical algorithm, not a verified performance guarantee of the supplied Mathematica implementation.**

## Implementation

The notebook contains these routines:

| Function | Role |
| --- | --- |
| `QuickSelect` | Selection of an order statistic / pivot |
| `Bridge` | Find a candidate upper-hull bridge across a vertical line |
| `ConnectPoints` | Recursive connection of hull vertices |
| `UpperHull` | Construct the upper chain |
| `LowerHull` | Construct the lower chain via reflection |
| `Convexhull` | Combine the upper and lower hull chains |
| `Main` | Read points, measure elapsed time and draw a plot |

## Repository structure

```text
.
├── README.md
├── .gitignore
├── data/
│   ├── problem1.txt          # 20 points reconstructed from saved notebook output
│   └── problem2.txt          # same example data; original second dataset unavailable
├── notebooks/
│   ├── KirkpatrickSeidel.nb  # portable paths, primary notebook
│   └── original.nb           # unmodified uploaded notebook
└── docs/
    └── algorithm.md         # algorithm overview and limitations
```

## Getting started

1. Install **Wolfram Mathematica** (the original notebook was saved in Mathematica 14.1).
2. Open `notebooks/KirkpatrickSeidel.nb`.
3. Evaluate the notebook from top to bottom. Its first cell sets the working directory to the notebook's location.
4. The `Main[]` call imports `../data/problem1.txt`, computes a hull, prints the number of hull vertices and elapsed time, and draws the result.

The input file is whitespace-separated, with the first line holding a point count, followed by one `x y` coordinate pair per line:

```text
4
0 0
1 0
1 1
0 1
```

**Important:** `Main[]` explicitly removes the first imported row with `Delete[..., 1]`. Retain the header line when replacing the dataset. The notebook also references `problem2.txt` in an exploratory cell, though `Main[]` uses `problem1.txt`.

## Verification and limitations

- The notebook has **not been executed or benchmarked** in a Wolfram kernel in this packaging environment.
- Degenerate geometries, numerical tolerance behavior, and the claimed asymptotic complexity of this implementation have **not been independently verified**.
- Some original plotting parameters, including a fixed `PlotRange`, may clip points when using other datasets.
- `data/problem1.txt` was recovered from a saved output cell; `problem2.txt` is a copy for convenience, **not the original second dataset**.
- For an independent correctness check, compare the set of hull vertices against Mathematica's `ConvexHullMesh[points]` / `MeshCoordinates` after accounting for ordering and collinear points.

## Reference

D. G. Kirkpatrick and R. Seidel, [*The Ultimate Planar Convex Hull Algorithm?*](https://doi.org/10.1137/0215021), **SIAM Journal on Computing**, 15(1), 287–299 (1986).

## Author

[Sultan — Shtrudel7](https://github.com/Shtrudel7)
