# Fit the vsn model

`vsn2` fits the vsn model to the data in `x` and returns a
[`vsn`](https://huber-group-embl.github.io/vsn/reference/class.vsn.md)
object with the fit parameters and the transformed data matrix. The data
are, typically, feature intensity readings from a microarray, but this
function may also be useful for other kinds of intensity data that obey
an additive-multiplicative error model. To obtain an object of the same
class as `x`, containing the normalised data and the same metdata as
`x`, use


        fit = vsn2(x, ...)
        nx = predict(fit, newdata=x)
      

or the wrapper
[`justvsn`](https://huber-group-embl.github.io/vsn/reference/justvsn.md).
Please see the vignette *Introduction to vsn*.

## Usage

``` r
vsnMatrix(x,
          reference,
          strata,
          lts.quantile = 0.9,
          subsample    = 0L,
          verbose      = interactive(),
          returnData   = TRUE,
          calib        = "affine",
          pstart,
          minDataPointsPerStratum = 42L,
          optimpar     = list(),
          defaultpar   = list(factr=5e7, pgtol=2e-4, maxit=60000L,
                              trace=0L, cvg.niter=7L, cvg.eps=0))

# S4 method for class 'ExpressionSet'
vsn2(x, reference, strata, ...)

# S4 method for class 'AffyBatch'
vsn2(x, reference, strata, subsample, ...)

# S4 method for class 'NChannelSet'
vsn2(x, reference, strata, backgroundsubtract=FALSE,
       foreground=c("R","G"), background=c("Rb", "Gb"), ...)

# S4 method for class 'RGList'
vsn2(x, reference, strata, ...)
```

## Arguments

- x:

  An object containing the data to which the model is fitted.

- reference:

  Optional, a
  [`vsn`](https://huber-group-embl.github.io/vsn/reference/class.vsn.md)
  object from a previous fit. If this argument is specified, the data in
  `x` are normalized "towards" an existing set of reference arrays whose
  parameters are stored in the object `reference`. If this argument is
  not specified, then the data in `x` are normalized "among themselves".
  See Details for a more precise explanation.

- strata:

  Optional, a `factor` or `integer` whose length is `nrow(x)`. It can be
  used for stratified normalization (i.e. separate offsets \\a\\ and
  factors \\b\\ for each level of `strata`). If missing, all rows of `x`
  are assumed to come from one stratum. If `strata` is an integer, its
  values must cover the range \\1,\ldots,n\\, where \\n\\ is the number
  of strata.

- lts.quantile:

  Numeric of length 1. The quantile that is used for the resistant least
  trimmed sum of squares regression. Allowed values are between 0.5
  and 1. A value of 1 corresponds to ordinary least sum of squares
  regression.

- subsample:

  Integer of length 1. If its value is greater than 0, the model
  parameters are estimated from a subsample of the data of size
  `subsample` only, yet the fitted transformation is then applied to all
  data. For large datasets, this can substantially reduce the CPU time
  and memory consumption at a negligible loss of precision. Note that
  the `AffyBatch` method of `vsn2` sets a value of `30000` for this
  parameter if it is missing from the function call - which is different
  from the behaviour of the other methods.

- backgroundsubtract:

  Logical of length 1: should local background estimates be subtracted
  before fitting vsn?

- foreground, background:

  Aligned character vectors of the same length, naming the channels of
  `x` that should be used as foreground and background values.

- verbose:

  Logical. If TRUE, some messages are printed.

- returnData:

  Logical. If TRUE, the transformed data are returned in a slot of the
  resulting
  [`vsn`](https://huber-group-embl.github.io/vsn/reference/class.vsn.md)
  object. Setting this option to `FALSE` allows saving memory if the
  data are not needed.

- calib:

  Character of length 1. Allowed values are `affine` and `none`. The
  default, `affine`, corresponds to the behaviour in package versions
  \<= 3.9, and to what is described in references \[1\] and \[2\]. The
  option `none` is an experimental new feature, in which no affine
  calibration is performed and only two global variance stabilisation
  transformation parameters `a` and `b` are fitted. This functionality
  might be useful in conjunction with other calibration methods, such as
  quantile normalisation - see the vignette *Introduction to vsn*.

- pstart:

  Optional, a three-dimensional numeric array that specifies start
  values for the iterative parameter estimation algorithm. If not
  specified, the function tries to guess useful start values. The first
  dimension corresponds to the levels of `strata`, the second dimension
  to the columns of `x` and the third dimension must be 2, corresponding
  to offsets and factors.

- minDataPointsPerStratum:

  The minimum number of data points per stratum. Normally there is no
  need for the user to change this; refer to the vignette for further
  documentation.

- optimpar:

  Optional, a list with parameters for the likelihood optimisation
  algorithm. Default parameters are taken from `defaultpar`. See
  details.

- defaultpar:

  The default parameters for the likelihood optimisation algorithm.
  Values in `optimpar` take precedence over those in `defaultpar`. The
  purpose of this argument is to expose the default values in this
  manual page - it is not intended to be changed, please use `optimpar`
  for that.

- ...:

  Arguments that get passed on to `vsnMatrix`.

## Value

An object of class
[`vsn`](https://huber-group-embl.github.io/vsn/reference/class.vsn.md).

## Note on overall scale and location of the glog transformation

The data are returned on a \\glog\\ scale to base 2. More precisely, the
transformed data are subject to the transformation \\glog_2(f(b)\*x+a) +
c\\, where the function \\glog_2(u) = log_2(u+\sqrt{u\*u+1}) =
asinh(u)/\log(2)\\ is called the generalised logarithm, the offset \\a\\
and the scaling parameter \\b\\ are the fitted model parameters (see
references), and \\f(x)=\exp(x)\\ is a parameter transformation that
allows ensuring positivity of the factor in front of \\x\\ while using
an unconstrained optimisation over \\b\\ \[4\]. The overall offset \\c\\
is computed from the \\b\\'s such that for large \\x\\ the
transformation approximately corresponds to the \\\log_2\\ function.
This is done separately for each stratum, but with the same value across
arrays. More precisely, if the element `b[s,i]` of the array *b* is the
scaling parameter for the `s`-th stratum and the `i`-th array, then
`c[s]` is computed as `log2(2*f(mean(b[,i])))`. The offset *c* is
inconsequential for all differential expression calculations, but many
users like to see the data in a range that they are familiar with.

## Specific behaviour of the different methods

`vsn2` methods exist for `ExpressionSet`,
[`NChannelSet`](https://rdrr.io/pkg/Biobase/man/class.NChannelSet.html),
[`AffyBatch`](https://rdrr.io/pkg/affy/man/AffyBatch-class.html) (from
the `affy` package), `RGList` (from the `limma` package), `matrix` and
`numeric`. If `x` is an
[`NChannelSet`](https://rdrr.io/pkg/Biobase/man/class.NChannelSet.html),
then `vsn2` is applied to the matrix that is obtained by horizontally
concatenating the color channels. Optionally, available background
estimates can be subtracted before. If `x` is an `RGList`, it is
converted into an `NChannelSet` using a copy of Martin Morgan's code for
`RGList` to `NChannelSet` coercion, then the `NChannelSet` method is
called.

## Standalone versus reference normalisation

If the `reference` argument is *not* specified, then the model
parameters \\\mu_k\\ and \\\sigma\\ are fit from the data in `x`. This
is the mode of operation described in \[1\] and that was the only option
in versions 1.X of this package. If `reference` is specified, the model
parameters \\\mu_k\\ and \\\sigma\\ are taken from it. This allows for
'incremental' normalization \[4\].

## Convergence of the iterative likelihood optimisation

`L-BFGS-B` uses three termination criteria:

1.  `(f_k - f_{k+1}) / max(|f_k|, |f_{k+1}|, 1) <= factr * epsmch` where
    `epsmch` is the machine precision.

2.  `|gradient| < pgtol`

3.  `iterations > maxit`

These are set by the elements `factr`, `pgtol` and `maxit` of
`optimpar`. The remaining elements are

- `trace`:

  An integer between 0 and 6, indicating the verbosity level of
  `L-BFGS-B`, higher values create more output.

- `cvg.niter`:

  The number of iterations to be used in the least trimmed sum of
  squares regression.

- `cvg.eps`:

  Numeric. A convergence threshold for the least trimmed sum of squares
  regression.

## See also

[`justvsn`](https://huber-group-embl.github.io/vsn/reference/justvsn.md),
`predict`

## References

\[1\] Variance stabilization applied to microarray data calibration and
to the quantification of differential expression, Wolfgang Huber, Anja
von Heydebreck, Holger Sueltmann, Annemarie Poustka, Martin Vingron;
Bioinformatics (2002) 18 Suppl.1 S96-S104.

\[2\] Parameter estimation for the calibration and variance
stabilization of microarray data, Wolfgang Huber, Anja von Heydebreck,
Holger Sueltmann, Annemarie Poustka, and Martin Vingron; Statistical
Applications in Genetics and Molecular Biology (2003) Vol. 2 No. 1,
Article 3. http://www.bepress.com/sagmb/vol2/iss1/art3.

\[3\] L-BFGS-B: Fortran Subroutines for Large-Scale Bound Constrained
Optimization, C. Zhu, R.H. Byrd, P. Lu and J. Nocedal, Technical Report,
Northwestern University (1996).

\[4\] Package vignette: Likelihood Calculations for vsn

## Author

Wolfgang Huber

## Examples

``` r
data("kidney")

fit = vsn2(kidney)                   ## fit
nkid = predict(fit, newdata=kidney)  ## apply fit

plot(exprs(nkid), pch=".")
abline(a=0, b=1, col="red")
```
