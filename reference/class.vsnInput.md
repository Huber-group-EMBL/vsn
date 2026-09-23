# Class to contain input data and parameters for vsn functions

Class to contain input data and parameters for vsn functions

## Creating Objects

`new("vsnInput")`

## Slots

- `x`::

  A numeric matrix with the input data.

- `reference`::

  An object of
  [`vsn`](https://huber-group-embl.github.io/vsn/reference/class.vsn.md),
  typically this would have been obtained from a previous fit to a set
  of reference arrays (data).

- `strata`::

  A factor of length 0 or n. If its length is n, then its levels
  correspond to different normalization strata (see
  [`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md)).

- `ordered`::

  Logical scalar; are the rows reordered so that the strata are
  contiguous.

- `lts.quantile`::

  Numeric scalar,
  see[`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md).

- `subsample`::

  Integer scalar,
  see[`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md).

- `verbose`::

  Logical scalar,
  see[`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md).

- `calib`:

  Character of length 1, see manual page of
  [`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md).

- `pstart`::

  A 3D array of size (number of strata) x (number of columns of the data
  matrix) x 2. It contains the start parameters.

- `optimpar`::

  List with parameters for the numerical optimiser `L-BFGS-B`; see the
  manual page of
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

## Author

Wolfgang Huber

## See also

[`vsn2`](https://huber-group-embl.github.io/vsn/reference/vsn2.md)
