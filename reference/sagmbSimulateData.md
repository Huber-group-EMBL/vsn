# Simulate data and assess vsn's parameter estimation

Functions to validate and assess the performance of vsn through
simulation of data.

## Usage

``` r
sagmbSimulateData(n=8064, d=2, de=0, up=0.5, nrstrata=1,  miss=0, log2scale=FALSE)
sagmbAssess(h1, sim)
```

## Arguments

- n:

  Numeric. Number of probes (rows).

- d:

  Numeric. Number of arrays (columns).

- de:

  Numeric. Fraction of differentially expressed genes.

- up:

  Numeric. Fraction of up-regulated genes among the differentially
  expressed genes.

- nrstrata:

  Numeric. Number of probe strata.

- miss:

  Numeric. Fraction of data points that is randomly sampled and set to
  `NA`.

- log2scale:

  Logical. If `TRUE`, glog on base 2 is used, if `FALSE`, (the default),
  then base e.

- h1:

  Matrix. Calibrated and transformed data, according, e.g., to vsn

- sim:

  List. The output of a previous call to `sagmbSimulateData`, see Value

## Value

For `sagmbSimulateData`, a list with four components: `hy`, an `n x d`
matrix with the true (=simulated) calibrated, transformed data; `y`, an
`n x d` matrix with the simulated uncalibrated raw data - this is
intended to be fed into
[`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md);
`is.de`, a logical vector of length `n`, specifying which probes are
simulated to be differentially expressed. `strata`, a factor of length
`n`.

For `sagmbSimulateData`, a number: the root mean squared difference
between true and estimated transformed data.

## Details

Please see the vignette.

## References

Wolfgang Huber, Anja von Heydebreck, Holger Sueltmann, Annemarie
Poustka, and Martin Vingron (2003) "Parameter estimation for the
calibration and variance stabilization of microarray data", Statistical
Applications in Genetics and Molecular Biology: Vol. 2: No. 1, Article
3. http://www.bepress.com/sagmb/vol2/iss1/art3

## Author

Wolfgang Huber

## Examples

``` r
  sim <- sagmbSimulateData(nrstrata = 4)
  ny  <- vsn2(sim$y, strata = sim$strata)
  res <- sagmbAssess(exprs(ny), sim)
  res
#> [1] 0.04680428
```
