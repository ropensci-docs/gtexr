# Get Fine Mapping

Retrieve Fine Mapping Data

- Finds and returns `Fine Mapping` data for the provided list of genes

- By default, this endpoint fetches data from the latest `GTEx` version

The retrieved data is split into pages with `items_per_page` entries per
page

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Static-Association-Endpoints/operation/get_fine_mapping_api_v2_association_fineMapping_get)

## Usage

``` r
get_fine_mapping(
  gencodeIds,
  datasetId = "gtex_v8",
  variantId = NULL,
  tissueSiteDetailIds = NULL,
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

- datasetId:

  String. Unique identifier of a dataset. Usually includes a data source
  and data release. Options: "gtex_v8", "gtex_snrnaseq_pilot".

- variantId:

  String. A gtex variant ID.

- tissueSiteDetailIds:

  Character vector of IDs for tissues of interest. Can be GTEx specific
  IDs (e.g. "Whole_Blood"; use
  [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  to see valid values) or Ontology IDs.

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
[`get_independent_eqtl()`](https://docs.ropensci.org/gtexr/reference/get_independent_eqtl.md),
[`get_multi_tissue_eqtls()`](https://docs.ropensci.org/gtexr/reference/get_multi_tissue_eqtls.md),
[`get_significant_single_tissue_eqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_eqtls.md),
[`get_significant_single_tissue_eqtls_by_location()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_eqtls_by_location.md),
[`get_significant_single_tissue_ieqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_ieqtls.md),
[`get_significant_single_tissue_isqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_isqtls.md),
[`get_significant_single_tissue_sqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_sqtls.md),
[`get_sqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_sqtl_genes.md)

## Examples

``` r
# search by gene
get_fine_mapping(gencodeIds = c(
  "ENSG00000132693.12",
  "ENSG00000203782.5"
))
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 27
#> # A tibble: 27 × 9
#>    datasetId gencodeId          method     pip setId setSize tissueSiteDetailId
#>    <chr>     <chr>              <chr>    <dbl> <int>   <int> <chr>             
#>  1 gtex_v8   ENSG00000132693.12 DAP-G  0.0235      1       5 Thyroid           
#>  2 gtex_v8   ENSG00000132693.12 DAP-G  0.0221      1       5 Thyroid           
#>  3 gtex_v8   ENSG00000132693.12 DAP-G  0.0171      1       5 Thyroid           
#>  4 gtex_v8   ENSG00000132693.12 DAP-G  0.0252      1       5 Thyroid           
#>  5 gtex_v8   ENSG00000132693.12 DAP-G  0.892       1       5 Thyroid           
#>  6 gtex_v8   ENSG00000203782.5  DAP-G  0.0126      1      22 Whole_Blood       
#>  7 gtex_v8   ENSG00000203782.5  DAP-G  0.00690     1      22 Whole_Blood       
#>  8 gtex_v8   ENSG00000203782.5  DAP-G  0.0313      1      22 Whole_Blood       
#>  9 gtex_v8   ENSG00000203782.5  DAP-G  0.00852     1      22 Whole_Blood       
#> 10 gtex_v8   ENSG00000203782.5  DAP-G  0.0105      1      22 Whole_Blood       
#> # ℹ 17 more rows
#> # ℹ 2 more variables: ontologyId <chr>, variantId <chr>

# optionally filter for a single variant and/or one or more tissues
get_fine_mapping(
  gencodeIds = c(
    "ENSG00000132693.12",
    "ENSG00000203782.5"
  ),
  variantId = "chr1_153228363_A_G_b38",
  tissueSiteDetailIds = c(
    "Whole_Blood",
    "Thyroid"
  )
)
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 1
#> # A tibble: 1 × 9
#>   datasetId gencodeId  method    pip setId setSize tissueSiteDetailId ontologyId
#>   <chr>     <chr>      <chr>   <dbl> <int>   <int> <chr>              <chr>     
#> 1 gtex_v8   ENSG00000… DAP-G  0.0126     1      22 Whole_Blood        UBERON:00…
#> # ℹ 1 more variable: variantId <chr>
```
