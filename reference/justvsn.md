# Wrapper functions for vsn

`justvsn` is equivalent to calling


      fit = vsn2(x, ...)
      nx = predict(fit, newdata=x, useDataInFit = TRUE)

`vsnrma` is a wrapper around
[`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md) and
[`rma`](https://rdrr.io/pkg/affy/man/rma.html).

## Usage

``` r
justvsn(x, ...)
vsnrma(x, ...)
```

## Arguments

- x:

  For `justvsn`, any kind of object for which
  [`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md)
  methods exist. For `vsnrma`, an
  [`AffyBatch`](https://rdrr.io/pkg/affy/man/AffyBatch-class.html).

- ...:

  Further arguments that get passed on to
  [`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md).

## Details

`vsnrma` does probe-wise background correction and between-array
normalization by calling
[`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md) on
the perfect match (PM) values only. Probeset summaries are calculated
with the medianpolish algorithm of
[`rma`](https://rdrr.io/pkg/affy/man/rma.html).

## Value

`justvsn` returns the vsn-normalised intensities in an object generally
of the same class as its first argument (see the man page of `predict`
for details). It preserves the metadata.

`vsnrma` returns an `ExpressionSet`.

## See also

[`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md)

## Author

Wolfgang Huber

## Examples

``` r
##--------------------------------------------------
## use "vsn2" to produce a "vsn" object
##--------------------------------------------------
data("kidney")
fit = vsn2(kidney)
nkid = predict(fit, newdata=kidney)

##--------------------------------------------------
## justvsn on ExpressionSet
##--------------------------------------------------
nkid2 = justvsn(kidney)
stopifnot(identical(exprs(nkid), exprs(nkid2)))

##--------------------------------------------------
## justvsn on RGList
##--------------------------------------------------
rg = new("RGList", list(R=exprs(kidney)[,1,drop=FALSE], G=exprs(kidney)[,2,drop=FALSE]))
erge = justvsn(rg)
```
