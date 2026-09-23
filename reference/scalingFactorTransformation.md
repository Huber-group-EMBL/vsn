# The transformation that is applied to the scaling parameter of the vsn model

The transformation that is applied to the scaling parameter of the vsn
model

## Usage

``` r
scalingFactorTransformation(b)
```

## Arguments

- b:

  Real vector.

## Value

A real vector of same length as b, with transformation `f` applied (see
vignette *Likelihood Calculations for vsn*).

## Author

Wolfgang Huber

## Examples

``` r
b  = seq(-3, 2, length=20)
fb = scalingFactorTransformation(b)
if(interactive())
  plot(b, fb, type="b", pch=16)
```
