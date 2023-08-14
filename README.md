---
output: github_document
---

# CoastlineFD

The goal of CoastlineFD is to calculate the fractal dimension of coastline by boxes method and Dividers method.

## Installation

You can install the development version of CoastlineFD like so:

``` r
devtools::github_install("redworld123/CoastlineFD")
```

## Example

This is a basic example which shows you how to solve a common problem:

``` r
library(CoastlineFD)
FD(
  "../density/D",
  "../density/B",
  "../fishnet",
  "FD1985_2022.xlsx",
  c(1985:2022),
  c(30, 60, 75, 150, 300, 600, 900, 1000, 1050, 1100, 1150, 1200, 1500, 1800),
  0.95,
  TRUE
)
```

What is special about using `README.Rmd` instead of just `README.md`? You can include R chunks like so
