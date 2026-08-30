# Get Significant Single Tissue Isqtls

Retrieve Interaction sQTL Data.

- This service retrieves cell type interaction sQTLs (isQTLs), from a
  specified dataset.

- Results may be filtered by tissue

- By default, the service queries the latest GTEx release.

The retrieved data is split into pages with `items_per_page` entries per
page

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Static-Association-Endpoints/operation/get_significant_single_tissue_isqtls_api_v2_association_singleTissueISqtl_get).

## Usage

``` r
get_significant_single_tissue_isqtls(
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
[`get_significant_single_tissue_ieqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_ieqtls.md),
[`get_significant_single_tissue_sqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_sqtls.md),
[`get_sqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_sqtl_genes.md)

## Examples

``` r
get_significant_single_tissue_isqtls(gencodeIds = c(
  "ENSG00000065613.9",
  "ENSG00000203782.5"
))
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 4
#> # A tibble: 4 × 25
#>   snpId      bGISE    pos snpIdUpper pValueG pValueGI geneSymbol geneSymbolUpper
#>   <chr>      <dbl>  <int> <chr>        <dbl>    <dbl> <chr>      <chr>          
#> 1 rs4845790 0.0194 1.53e8 RS4845790  0.00645  8.97e-7 LOR        LOR            
#> 2 rs4845790 0.0196 1.53e8 RS4845790  0.0118   1.41e-7 LOR        LOR            
#> 3 rs359327… 0.0289 1.54e8 RS35932716 0.0142   3.70e-5 LOR        LOR            
#> 4 rs146285… 0.0293 1.53e8 RS1462851… 0.0225   3.03e-5 LOR        LOR            
#> # ℹ 17 more variables: pValueI <dbl>, bGI <dbl>, tissueSiteDetailId <chr>,
#> #   ontologyId <chr>, chromosome <chr>, tissueCellType <chr>,
#> #   tssDistance <int>, bGSE <dbl>, variantId <chr>, maf <dbl>, bISE <dbl>,
#> #   datasetId <chr>, bG <dbl>, pValueAdjustedBH <dbl>, bI <dbl>,
#> #   gencodeId <chr>, phenotypeId <chr>
```
