# Calculate Ieqtls

Calculate your own Cell Specific eQTLs.

- This service calculates the gene-variant association for any given
  pair of gene and variant, which may or may not be significant.

- This requires as input a GENCODE ID, GTEx variant ID, and tissue site
  detail ID.

By default, the calculation is based on the latest GTEx release.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Dynamic-Association-Endpoints/operation/calculate_ieqtls_api_v2_association_dynieqtl_get).

## Usage

``` r
calculate_ieqtls(
  cellType,
  tissueSiteDetailId,
  gencodeId,
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

- gencodeId:

  String. A Versioned GENCODE ID of a gene, e.g. "ENSG00000065613.9".

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
[`calculate_isqtls()`](https://docs.ropensci.org/gtexr/reference/calculate_isqtls.md),
[`calculate_splicing_quantitative_trait_loci()`](https://docs.ropensci.org/gtexr/reference/calculate_splicing_quantitative_trait_loci.md)

## Examples

``` r
# perform request
calculate_ieqtls(
  cellType = "Adipocytes",
  tissueSiteDetailId = "Adipose_Subcutaneous",
  gencodeId = "ENSG00000203782.5",
  variantId = "chr1_1099341_T_C_b38"
)
#> # A tibble: 1 × 9
#>   cellType  data  datasetId enrichmentScores gencodeId genotypes regressionCoord
#>   <chr>     <lis> <chr>     <list>           <chr>     <list>    <list>         
#> 1 Adipocyt… <dbl> gtex_v8   <dbl [581]>      ENSG0000… <int>     <named list>   
#> # ℹ 2 more variables: tissueSiteDetailId <chr>, variantId <chr>
```
