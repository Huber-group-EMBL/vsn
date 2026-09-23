# Intensity data for 8 cDNA slides with CLL and DLBL samples from the Alizadeh et al. paper in Nature 2000

8 cDNA chips from Alizadeh lymphoma paper

## Usage

``` r
data(lymphoma)
```

## Format

`lymphoma` is an `ExpressionSet` containing the data from 8 chips from
the lymphoma data set by Alizadeh et al. (see references). Each chip
represents two samples: on color channel 1 (CH1, Cy3, green) the common
reference sample, and on color channel 2 (CH2, Cy5, red) the various
disease samples. See `pData(lymphoma)`. The 9216x16 matrix
`exprs(lymphoma)` contains the background-subtracted spot intensities
(CH1I-CH1B and CH2I-CH2B, respectively).

## Details

The chip intensity files were downloaded from the Stanford microarray
database. Starting from the link below, this was done by following the
links *Published Data* -\> *Alizadeh AA, et al. (2000) Nature
403(6769):503-11* -\> *Data in SMD* -\> *Display Data*, and selecting
the following 8 slides:

|         |
|---------|
| lc7b019 |
| lc7b047 |
| lc7b048 |
| lc7b056 |
| lc7b057 |
| lc7b058 |
| lc7b069 |
| lc7b070 |

Then, the script `makedata.R` from the `scripts` subdirectory of this
package was run to generate the R data object.

## References

A. Alizadeh et al., Distinct types of diffuse large B-cell lymphoma
identified by gene expression profiling. Nature 403(6769):503-11, Feb 3,
2000.

## Source

http://genome-www5.stanford.edu/MicroArray/SMD

## Examples

``` r
   data("lymphoma")
   lymphoma
#> ExpressionSet (storageMode: lockedEnvironment)
#> assayData: 9216 features, 16 samples 
#>   element names: exprs 
#> protocolData: none
#> phenoData
#>   sampleNames: lc7b047.reference lc7b047.CLL-13 ... lc7b058.DLCL-0023
#>     (16 total)
#>   varLabels: name sample dye
#>   varMetadata: labelDescription
#> featureData: none
#> experimentData: use 'experimentData(object)'
#> Annotation:  
   pData(lymphoma)
#>                      name    sample dye
#> lc7b047.reference lc7b047 reference Cy3
#> lc7b047.CLL-13    lc7b047    CLL-13 Cy5
#> lc7b048.reference lc7b048 reference Cy3
#> lc7b048.CLL-13    lc7b048    CLL-13 Cy5
#> lc7b069.reference lc7b069 reference Cy3
#> lc7b069.CLL-52    lc7b069    CLL-52 Cy5
#> lc7b070.reference lc7b070 reference Cy3
#> lc7b070.CLL-39    lc7b070    CLL-39 Cy5
#> lc7b019.reference lc7b019 reference Cy3
#> lc7b019.DLCL-0032 lc7b019 DLCL-0032 Cy5
#> lc7b056.reference lc7b056 reference Cy3
#> lc7b056.DLCL-0024 lc7b056 DLCL-0024 Cy5
#> lc7b057.reference lc7b057 reference Cy3
#> lc7b057.DLCL-0029 lc7b057 DLCL-0029 Cy5
#> lc7b058.reference lc7b058 reference Cy3
#> lc7b058.DLCL-0023 lc7b058 DLCL-0023 Cy5
```
