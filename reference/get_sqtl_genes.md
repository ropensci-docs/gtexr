# Get Sqtl Genes

Retrieve sGenes (sQTL Genes).

- This service returns sGenes (sQTL Genes) from the specified dataset.

- Results may be filtered by tissue.

- By default, the service queries the latest GTEx release.

The retrieved data is split into pages with `items_per_page` entries per
page

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Static-Association-Endpoints/operation/get_sqtl_genes_api_v2_association_sgene_get).

## Usage

``` r
get_sqtl_genes(
  tissueSiteDetailIds = NULL,
  datasetId = "gtex_v8",
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

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
[`get_significant_single_tissue_isqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_isqtls.md),
[`get_significant_single_tissue_sqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_sqtls.md)

## Examples

``` r
get_sqtl_genes("Whole_Blood")
#> Warning: ! Total number of items (3013) exceeds the selected maximum page size (250).
#> ✖ 2763 items were not retrieved.
#> ℹ To retrieve all available items, increase `itemsPerPage`, ensuring you reuse
#>   your original query parameters e.g.
#>   `get_sqtl_genes(<your_existing_parameters>, itemsPerPage = 100000)`
#> ℹ Alternatively, adjust global "gtexr.itemsPerPage" setting e.g.
#>   `options(list(gtexr.itemsPerPage = 100000))`
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 13
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 3013
#> # A tibble: 250 × 11
#>    nPhenotypes pValueThreshold phenotypeId        geneSymbol    pValue datasetId
#>          <int>           <dbl> <chr>              <chr>          <dbl> <chr>    
#>  1           9      0.0000145  chr1:15947:16607:… WASH7P     7.15e-  8 gtex_v8  
#>  2           6      0.00000634 chr1:1090428:1091… C1orf159   6.85e- 10 gtex_v8  
#>  3           7      0.00000908 chr1:1228946:1231… SDF4       1.16e-188 gtex_v8  
#>  4           6      0.00000861 chr1:1310688:1310… PUSL1      2.50e- 40 gtex_v8  
#>  5           3      0.00000954 chr1:1325102:1327… CPTP       9.60e-  7 gtex_v8  
#>  6           2      0.0000147  chr1:1487914:1489… ATAD3C     1.61e- 25 gtex_v8  
#>  7           5      0.00000740 chr1:1487914:1489… ATAD3B     1.61e- 25 gtex_v8  
#>  8           2      0.0000361  chr1:1545002:1547… SSU72      3.28e- 25 gtex_v8  
#>  9          19      0.00000176 chr1:1629311:1629… MIB2       1.97e- 12 gtex_v8  
#> 10           8      0.00000273 chr1:1641113:1641… CDK11B     3.08e- 56 gtex_v8  
#> # ℹ 240 more rows
#> # ℹ 5 more variables: empiricalPValue <dbl>, tissueSiteDetailId <chr>,
#> #   ontologyId <chr>, qValue <dbl>, gencodeId <chr>
```
