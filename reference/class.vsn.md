# Class to contain result of a vsn fit

Class to contain result of a vsn fit

## Creating Objects

`new("vsn")` `vsn2(x)` with `x` being an `ExpressionSet`.

## Slots

- `coefficients`::

  A 3D array of size (number of strata) x (number of columns of the data
  matrix) x 2. It contains the fitted normalization parameters (see
  vignette).

- `strata`::

  A factor of length 0 or n. If its length is n, then its levels
  correspond to different normalization strata (see vignette).

- `mu`::

  A numeric vector of length n with the fitted parameters
  \\\hat{\mu}\_k\\, for \\k=1,...,n\\.

- `sigsq`::

  A numeric scalar, \\\hat{\sigma}^2\\.

- `hx`::

  A numeric matrix with 0 or n rows. If the number of rows is n, then
  `hx` contains the transformed data matrix.

- `lbfgsb`::

  An integer scalar containing the return code from the L-BFGS-B
  optimizer.

- `hoffset`::

  Numeric scalar, the overall offset \\c\\- see manual page of
  [`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md).

- `calib`::

  Character of length 1, see manual page of
  [`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md).

## Methods

- `[`:

  Subset

- `dim`:

  Get dimensions of data matrix.

- `nrow`:

  Get number of rows of data matrix.

- `ncol`:

  Get number of columns of data matrix.

- `show`:

  Print a summary of the object

- `exprs`:

  Accessor to slot `hx`.

- `coef`, `coefficients`:

  Accessors to slot `coefficients`.

## Author

Wolfgang Huber

## See also

[`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md)

## Examples

``` r
  data("kidney")
  v = vsn2(kidney)
  show(v)
#> vsn object for 8704 features and 2 samples.
#> sigsq=0.005
#> hx: 8704 x 2 matrix.
  dim(v)
#> [1] 8704    2
  v[1:10, ]
#> vsn object for 10 features and 2 samples.
#> sigsq=0.005
#> hx: 10 x 2 matrix.
```
