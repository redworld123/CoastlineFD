# CoastlineFD

Fractal Dimensions of Coastline

# Installation

```R
install.packages("CoastlineFD")
devtools::install_github("CoastlineFD")
```
# Example

- BoxesFD
- DividersFD
- Fishnet
- Results
- *.R

```R
library("CoastlineFD")

FD(
  "./DividersFD",
  "./BoxesFD",
  "./Fishnet",
  "./FD.xlsx",
  c(1985:2022),
  c(30, 60, 75, 90, 150, 200, 300, 400, 500, 
    600, 700, 800, 900, 1000, 1050, 1100, 1150,
    1200, 1300, 1400, 1500, 1650, 1800, 2500, 3000,
    3500, 4500, 6000, 7500, 9000),
  0.99,
  TRUE,
  TRUE
)
```
