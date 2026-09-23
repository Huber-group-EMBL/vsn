# Intensity data for one cDNA slide with two adjacent tissue samples from a nephrectomy (kidney)

Intensity data for one cDNA slide with two adjacent tissue samples from
a nephrectomy (kidney)

## Usage

``` r
data(kidney)
```

## Format

`kidney` is an `ExpressionSet` containing the data from one cDNA chip.
The 8704x2 matrix `exprs(kidney)` contains the spot intensities for the
red (635 nm) and green color channels (532 nm) respectively. For each
spot, a background estimate from a surrounding region was subtracted.

## Details

The chip was produced in 2001 by Holger Sueltmann at the Division of
Molecular Genome Analysis at the German Cancer Research Center in
Heidelberg.

## References

Huber W, Boer JM, von Heydebreck A, Gunawan B, Vingron M, Fuzesi L,
Poustka A, Sueltmann H. Transcription profiling of renal cell carcinoma.
Verh Dtsch Ges Pathol. 2002;86:153-64. PMID: 12647365

## Examples

``` r
 data("kidney")
 plot(exprs(kidney), pch = ".", log = "xy")
#> Warning: 591 x values <= 0 omitted from logarithmic plot
#> Warning: 603 y values <= 0 omitted from logarithmic plot
 abline(a = 0, b = 1, col = "blue")  
```
