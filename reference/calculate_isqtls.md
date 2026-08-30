# Calculate Isqtls

Calculate your own Cell Specific sQTLs.

- This service calculates the gene-variant association for any given
  pair of gene and variant, which may or may not be significant.

- This requires as input a GENCODE ID, GTEx variant ID, and tissue site
  detail ID.

By default, the calculation is based on the latest GTEx release.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Dynamic-Association-Endpoints/operation/calculate_ieqtls_api_v2_association_dynieqtl_get).

## Usage

``` r
calculate_isqtls(
  cellType,
  tissueSiteDetailId,
  phenotypeId,
  variantId,
  datasetId = "gtex_v8",
  .return_raw = FALSE
)
```

## Arguments

- cellType:

  String. "Adipocytes", "Epithelial_cells", "Hepatocytes",
  "Keratinocytes", "Myocytes", "Neurons", "Neutrophils".

- tissueSiteDetailId:

  String. The ID of the tissue of interest. Can be a GTEx specific ID
  (e.g. "Whole_Blood"; use
  [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  to see valid values) or an Ontology ID.

- phenotypeId:

  String. See [GTEx portal
  FAQs](https://www.gtexportal.org/home/faq#splicingPhenotypeId) for
  further details.

- variantId:

  String. A gtex variant ID.

- datasetId:

  String. Unique identifier of a dataset. Usually includes a data source
  and data release. Options: "gtex_v8", "gtex_snrnaseq_pilot".

- .return_raw:

  Logical. If `TRUE`, return the raw API JSON response. Default =
  `FALSE`

## Value

A tibble. Or a list if `.return_raw = TRUE`.

## See also

Other Dynamic Association Endpoints:
[`calculate_expression_quantitative_trait_loci()`](https://docs.ropensci.org/gtexr/reference/calculate_expression_quantitative_trait_loci.md),
[`calculate_ieqtls()`](https://docs.ropensci.org/gtexr/reference/calculate_ieqtls.md),
[`calculate_splicing_quantitative_trait_loci()`](https://docs.ropensci.org/gtexr/reference/calculate_splicing_quantitative_trait_loci.md)

## Examples

``` r
# perform request
calculate_isqtls(
  cellType = "Neutrophils",
  tissueSiteDetailId = "Whole_Blood",
  phenotypeId = "chr1:15947:16607:clu_40980:ENSG00000227232.5",
  variantId = "chr1_1099341_T_C_b38"
)
#> # A tibble: 1 × 9
#>   cellType    data   datasetId enrichmentScores phenotypeId   tissueSiteDetailId
#>   <chr>       <list> <chr>     <list>           <chr>         <chr>             
#> 1 Neutrophils <dbl>  gtex_v8   <dbl [670]>      chr1:15947:1… Whole_Blood       
#> # ℹ 3 more variables: variantId <chr>, genotypes <list>, regressionCoord <list>
```
