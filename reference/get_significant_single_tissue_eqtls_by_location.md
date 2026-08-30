# Get Significant Single Tissue eQTLs By Location

Find significant single tissue eQTLs using Chromosomal Locations.

- This service returns precomputed significant single tissue eQTLs.

- Results may be filtered by tissue, and/or dataset.

By default, the service queries the latest GTEx release. Since this
endpoint is used to support a third party program on the portal, the
return structure is different from other endpoints and is not paginated.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Static-Association-Endpoints/operation/get_significant_single_tissue_eqtls_api_v2_association_singleTissueEqtl_get)

## Usage

``` r
get_significant_single_tissue_eqtls_by_location(
  tissueSiteDetailId,
  start,
  end,
  chromosome,
  datasetId = "gtex_v8",
  .return_raw = FALSE
)
```

## Arguments

- tissueSiteDetailId:

  String. The ID of the tissue of interest. Can be a GTEx specific ID
  (e.g. "Whole_Blood"; use
  [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  to see valid values) or an Ontology ID.

- start:

  Integer.

- end:

  Integer.

- chromosome:

  String. One of "chr1", "chr2", "chr3", "chr4", "chr5", "chr6", "chr7",
  "chr8", "chr9", "chr10", "chr11", "chr12", "chr13", "chr14", "chr15",
  "chr16", "chr17", "chr18", "chr19", "chr20", "chr21", "chr22", "chrM",
  "chrX", "chrY".

- datasetId:

  String. Unique identifier of a dataset. Usually includes a data source
  and data release. Options: "gtex_v8", "gtex_snrnaseq_pilot".

- .return_raw:

  Logical. If `TRUE`, return the raw API JSON response. Default =
  `FALSE`

## Value

A tibble. Or a list if `.return_raw = TRUE`.

## See also

Other Static Association Endpoints:
[`get_eqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_eqtl_genes.md),
[`get_fine_mapping()`](https://docs.ropensci.org/gtexr/reference/get_fine_mapping.md),
[`get_independent_eqtl()`](https://docs.ropensci.org/gtexr/reference/get_independent_eqtl.md),
[`get_multi_tissue_eqtls()`](https://docs.ropensci.org/gtexr/reference/get_multi_tissue_eqtls.md),
[`get_significant_single_tissue_eqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_eqtls.md),
[`get_significant_single_tissue_ieqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_ieqtls.md),
[`get_significant_single_tissue_isqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_isqtls.md),
[`get_significant_single_tissue_sqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_sqtls.md),
[`get_sqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_sqtl_genes.md)

## Examples

``` r
get_significant_single_tissue_eqtls_by_location(
  tissueSiteDetailId = "Artery_Aorta",
  start = 10000,
  end = 250000,
  chromosome = "chr11"
)
#> # A tibble: 434 × 11
#>    chromosome datasetId gencodeId      geneSymbol geneSymbolUpper   nes   pValue
#>    <chr>      <chr>     <chr>          <chr>      <chr>           <dbl>    <dbl>
#>  1 chr11      gtex_v8   ENSG000001779… BET1L      BET1L           0.381 1.11e- 6
#>  2 chr11      gtex_v8   ENSG000001779… BET1L      BET1L           0.364 2.25e- 6
#>  3 chr11      gtex_v8   ENSG000001779… BET1L      BET1L           0.417 3.10e- 8
#>  4 chr11      gtex_v8   ENSG000001779… BET1L      BET1L           0.480 8.39e- 9
#>  5 chr11      gtex_v8   ENSG000001779… BET1L      BET1L           0.462 6.36e- 9
#>  6 chr11      gtex_v8   ENSG000001779… BET1L      BET1L           0.553 8.89e-10
#>  7 chr11      gtex_v8   ENSG000001779… BET1L      BET1L           0.577 2.95e-12
#>  8 chr11      gtex_v8   ENSG000001779… BET1L      BET1L           0.547 6.13e-10
#>  9 chr11      gtex_v8   ENSG000001779… BET1L      BET1L           0.462 6.36e- 9
#> 10 chr11      gtex_v8   ENSG000001779… BET1L      BET1L           0.462 6.36e- 9
#> # ℹ 424 more rows
#> # ℹ 4 more variables: pos <int>, snpId <chr>, tissueSiteDetailId <chr>,
#> #   variantId <chr>
```
