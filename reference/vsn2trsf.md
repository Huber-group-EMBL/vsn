# Apply the vsn transformation to data

Apply the vsn transformation to data.

## Usage

``` r
# S4 method for class 'vsn'
predict(object, newdata, strata=object@strata, log2scale=TRUE, useDataInFit=FALSE)
```

## Arguments

- object:

  An object of class
  [`vsn`](https://huber-group-embl.github.io/vsn/reference/class.vsn.md)
  that contains transformation parameters and strata information,
  typically this is the result of a previous call to `vsn2`.

- newdata:

  Object of class `ExpressionSet`,
  [`NChannelSet`](https://rdrr.io/pkg/Biobase/man/class.NChannelSet.html),
  [`AffyBatch`](https://rdrr.io/pkg/affy/man/AffyBatch-class.html) (from
  the `affy` package), `RGList` (from the `limma` package), `matrix` or
  `numeric`, with the data to which the fit is to be applied to.

- strata:

  Optional, a `factor` or `integer` that aligns with the rows of
  `newdata`; see the `strata` argument of
  [`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md).

- log2scale:

  If `TRUE`, the data are returned on the glog scale to base 2, and an
  overall offset c is added (see *Value* section of the
  [`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md)
  manual page). If `FALSE`, the data are returned on the glog scale to
  base e, and no offset is added.

- useDataInFit:

  If `TRUE`, then no transformation is attempted and the data stored in
  `object` is transferred appropriately into resulting object, which
  otherwise preserves the class and metadata of `newdata`. This option
  exists to increase performance in constructs like


             fit = vsn2(x, ...)
             nx = predict(fit, newdata=x)
        

  and is used, for example, in the
  [`justvsn`](https://huber-group-embl.github.io/vsn/reference/justvsn.md)
  function.

## Value

An object typically of the same class as `newdata`. There are two
exceptions: if `newdata` is an `RGList`, the return value is an
[`NChannelSet`](https://rdrr.io/pkg/Biobase/man/class.NChannelSet.html),
and if `newdata` is numeric, the return value is a `matrix` with 1
column.

## Author

Wolfgang Huber

## Examples

``` r
data("kidney")

## nb: for random subsampling, the 'subsample' argument of vsn
##   provides an easier way to do this
fit = vsn2(kidney[sample(nrow(kidney), 500), ])
tn = predict(fit, newdata=exprs(kidney))
```
