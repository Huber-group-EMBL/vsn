# vsn

vsn

## Details

The main function of the package is
[`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md).
Interesting for its applications are also `predict` and the wrapper
function
[`justvsn`](https://huber-group-embl.github.io/vsn/reference/justvsn.md).

[`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md) can
be applied to objects of class `ExpressionSet`,
[`NChannelSet`](https://rdrr.io/pkg/Biobase/man/class.NChannelSet.html),
[`AffyBatch`](https://rdrr.io/pkg/affy/man/AffyBatch-class.html) (from
the `affy` package) and `RGList` (from the `limma` package), `matrix`
and `vector`. It returns an object of class
[`vsn`](https://huber-group-embl.github.io/vsn/reference/class.vsn.md),
which contains the results of fitting the `vsn` model to the data.

The most common use case is that you will want to construct a new data
object with the vsn-normalized data whose class is the same as that of
the input data and which preserves the metadata. This can be achieved by


        fit = vsn2(x, ...)
        nx = predict(fit, newdata=x)
      

To simplify this, there exists also a simple wrapper
[`justvsn`](https://huber-group-embl.github.io/vsn/reference/justvsn.md).

## Author

Wolfgang Huber
