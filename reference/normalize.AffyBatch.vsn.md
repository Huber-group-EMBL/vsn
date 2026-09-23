# Wrapper for vsn to be used as a normalization method with expresso

Wrapper for
[`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md) to be
used as a normalization method with the expresso function of the package
affy. The expresso function is deprecated, consider using
[`justvsn`](https://huber-group-embl.github.io/vsn/reference/justvsn.md)
instead. The normalize.AffyBatch.vsn can still be useful on its own, as
it provides some additional control of the normalization process
(fitting on subsets, alternate transform parameters).

## Usage

``` r
normalize.AffyBatch.vsn(
     abatch,
     reference,
     strata = NULL,
     subsample = if (nrow(exprs(abatch))>30000L) 30000L else 0L,
     subset,
     log2scale = TRUE,
     log2asymp=FALSE,
     ...)
```

## Arguments

- abatch:

  An object of type
  [`AffyBatch`](https://rdrr.io/pkg/affy/man/AffyBatch-class.html).

- reference:

  Optional, a 'vsn' object from a previous fit. If this argument is
  specified, the data in 'x' are normalized "towards" an existing set of
  reference arrays whose parameters are stored in the object
  'reference'. If this argument is not specified, then the data in 'x'
  are normalized "among themselves". See
  [`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md) for
  details.

- strata:

  The 'strata' functionality is not supported, the parameter is ignored.

- subsample:

  Is passed on to
  [`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md).

- subset:

  This allows the specification of a subset of expression measurements
  to be used for the vsn fit. The transformation with the parameters of
  this fit is then, however, applied to the whole dataset. This is
  useful for excluding expression measurements that are known to be
  differentially expressed or control probes that may not match the vsn
  model, thus avoiding that they influence the normalization process.
  This operates at the level of probesets, not probes. Both 'subset' and
  'subsample' can be used together.

- log2scale:

  If TRUE, this will perform a global affine transform on the data to
  put them on a similar scale as the original non-transformed data. Many
  users prefer this. Fold-change estimates are not affected by this
  transform. In some situations, however, it may be helpful to turn this
  off, e.g., when comparing independently normalized subsets of the
  data.

- log2asymp:

  If TRUE, this will perform a global affine transform on the data to
  make the generalized log (asinh) transform be asymptotically identical
  to a log base 2 transform. Some people find this helpful. Only **one**
  of 'log2scale' or 'log2asymp' can be set to TRUE. Fold-change
  estimates are not affected by this transform.

- ...:

  Further parameters for
  [`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md).

## Details

Please refer to the *Details* and *References* sections of the man page
for [`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md)
for more details about this method.

**Important note**: after calling
[`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md), the
function `normalize.AffyBatch.vsn` **exponentiates** the data (base 2).
This is done in order to make the behavior of this function similar to
the other normalization methods in affy. That packages uses the
convention of taking the logarithm to base in subsequent analysis steps
(e.g. in [`medpolish`](https://rdrr.io/r/stats/medpolish.html)).

## Value

An object of class
[`AffyBatch`](https://rdrr.io/pkg/affy/man/AffyBatch-class.html). The
`vsn` object returned, which can be used as `reference` for subsequent
fits, is provided by `description(abatch)@preprocessing$vsnReference`.

## Author

D. P. Kreil <http://bioinf.boku.ac.at/>, Wolfgang Huber

## See also

[`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md)

## Examples

``` r
## Please see vignette.
```
