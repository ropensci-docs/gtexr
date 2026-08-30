# Get Significant Single Tissue Ieqtls

Retrieve Interaction eQTL Data.

- This service returns cell type interaction eQTLs (ieQTLs), from a
  specified dataset.

- Results may be filtered by tissue

- By default, the service queries the latest GTEx release.

The retrieved data is split into pages with `items_per_page` entries per
page

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Static-Association-Endpoints/operation/get_significant_single_tissue_ieqtls_api_v2_association_singleTissueIEqtl_get)

## Usage

``` r
get_significant_single_tissue_ieqtls(
  gencodeIds,
  variantIds = NULL,
  tissueSiteDetailIds = NULL,
  datasetId = "gtex_v8",
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

- gencodeIds:

  A character vector of Versioned GENCODE IDs, e.g.
  c("ENSG00000132693.12", "ENSG00000203782.5").

- variantIds:

  Character vector. Gtex variant IDs.

- tissueSiteDetailIds:

  Character vector of IDs for tissues of interest. Can be GTEx specific
  IDs (e.g. "Whole_Blood"; use
  [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  to see valid values) or Ontology IDs.

- datasetId:

  String. Unique identifier of a dataset. Usually includes a data source
  and data release. Options: "gtex_v8", "gtex_snrnaseq_pilot".

- page:

  Integer (default = 0).

- itemsPerPage:

  Integer (default = 250). Set globally to maximum value 100000 with
  `options(list(gtexr.itemsPerPage = 100000))`.

- .verbose:

  Logical. If `TRUE` (default), print paging information. Set to `FALSE`
  globally with `options(list(gtexr.verbose = FALSE))`.

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
[`get_significant_single_tissue_eqtls_by_location()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_eqtls_by_location.md),
[`get_significant_single_tissue_isqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_isqtls.md),
[`get_significant_single_tissue_sqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_sqtls.md),
[`get_sqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_sqtl_genes.md)

## Examples

``` r
get_significant_single_tissue_ieqtls(c(
  "ENSG00000132693.12",
  "ENSG00000203782.5"
))
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 86
#> # A tibble: 86 × 24
#>    snpId     bGISE    pos snpIdUpper pValueG pValueGI geneSymbol geneSymbolUpper
#>    <chr>     <dbl>  <int> <chr>        <dbl>    <dbl> <chr>      <chr>          
#>  1 rs34188… 0.0890 1.54e8 RS34188388  0.102  0.00447  LOR        LOR            
#>  2 rs24945… 0.0654 1.60e8 RS2494523   0.867  0.00129  CRP        CRP            
#>  3 rs986760 0.148  1.53e8 RS986760    0.0454 0.00694  LOR        LOR            
#>  4 rs17697… 0.0428 1.59e8 RS17697329  0.515  0.000627 CRP        CRP            
#>  5 rs67415… 0.154  1.53e8 RS67415955  0.565  0.000754 LOR        LOR            
#>  6 rs12133… 0.157  1.60e8 RS12133356  0.634  0.00106  CRP        CRP            
#>  7 rs12132… 0.113  1.53e8 RS12132927  0.858  0.00365  LOR        LOR            
#>  8 rs30269… 0.0683 1.59e8 RS3026943   0.684  0.00222  CRP        CRP            
#>  9 rs24946… 0.0567 1.54e8 RS2494670   0.516  0.000595 LOR        LOR            
#> 10 rs12121… 0.0695 1.60e8 RS12121609  0.444  0.000266 CRP        CRP            
#> # ℹ 76 more rows
#> # ℹ 16 more variables: pValueI <dbl>, bGI <dbl>, tissueSiteDetailId <chr>,
#> #   ontologyId <chr>, chromosome <chr>, tissueCellType <chr>,
#> #   tssDistance <int>, bGSE <dbl>, variantId <chr>, maf <dbl>, bISE <dbl>,
#> #   datasetId <chr>, bG <dbl>, pValueAdjustedBH <dbl>, bI <dbl>,
#> #   gencodeId <chr>
```
