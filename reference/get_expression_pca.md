# Get Expression Pca

Find gene expression PCA data.

- Returns gene expression PCA (principal component analysis) in tissues.

- Results may be filtered by tissue, sample, or dataset.

By default, the service queries the latest GTEx release.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Expression-Data-Endpoints/operation/get_expression_pca_api_v2_expression_expressionPca_get)

## Usage

``` r
get_expression_pca(
  tissueSiteDetailIds,
  datasetId = "gtex_v8",
  sampleId = NULL,
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

- sampleId:

  String. `^GTEX-[A-Z0-9]{5}-[0-9]{4}-SM-[A-Z0-9]{5}$`

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

Other Expression Data Endpoints:
[`get_clustered_median_exon_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_exon_expression.md),
[`get_clustered_median_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_gene_expression.md),
[`get_clustered_median_junction_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_junction_expression.md),
[`get_clustered_median_transcript_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_transcript_expression.md),
[`get_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_gene_expression.md),
[`get_median_exon_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_exon_expression.md),
[`get_median_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_gene_expression.md),
[`get_median_junction_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_junction_expression.md),
[`get_median_transcript_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_transcript_expression.md),
[`get_single_nucleus_gex()`](https://docs.ropensci.org/gtexr/reference/get_single_nucleus_gex.md),
[`get_single_nucleus_gex_summary()`](https://docs.ropensci.org/gtexr/reference/get_single_nucleus_gex_summary.md),
[`get_top_expressed_genes()`](https://docs.ropensci.org/gtexr/reference/get_top_expressed_genes.md)

## Examples

``` r
get_expression_pca(tissueSiteDetailIds = c(
  "Adipose_Subcutaneous",
  "Whole_Blood"
))
#> Warning: ! Total number of items (1418) exceeds the selected maximum page size (250).
#> ✖ 1168 items were not retrieved.
#> ℹ To retrieve all available items, increase `itemsPerPage`, ensuring you reuse
#>   your original query parameters e.g.
#>   `get_expression_pca(<your_existing_parameters>, itemsPerPage = 100000)`
#> ℹ Alternatively, adjust global "gtexr.itemsPerPage" setting e.g.
#>   `options(list(gtexr.itemsPerPage = 100000))`
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 6
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 1418
#> # A tibble: 250 × 7
#>        pc1      pc2      pc3 sampleId    tissueSiteDetailId ontologyId datasetId
#>      <dbl>    <dbl>    <dbl> <chr>       <chr>              <chr>      <chr>    
#>  1  0.0385 -0.0178   0.0769  GTEX-1117F… Adipose_Subcutane… UBERON:00… gtex_v8  
#>  2 -0.0585  0.00809  0.00492 GTEX-111CU… Adipose_Subcutane… UBERON:00… gtex_v8  
#>  3  0.140  -0.0308  -0.0368  GTEX-111FC… Adipose_Subcutane… UBERON:00… gtex_v8  
#>  4  0.0597  0.140    0.0294  GTEX-111VG… Adipose_Subcutane… UBERON:00… gtex_v8  
#>  5 -0.0968  0.00233 -0.0174  GTEX-111YS… Adipose_Subcutane… UBERON:00… gtex_v8  
#>  6 -0.120   0.0195  -0.0594  GTEX-1122O… Adipose_Subcutane… UBERON:00… gtex_v8  
#>  7 -0.102   0.0652   0.00344 GTEX-1128S… Adipose_Subcutane… UBERON:00… gtex_v8  
#>  8  0.105   0.0174  -0.0568  GTEX-113IC… Adipose_Subcutane… UBERON:00… gtex_v8  
#>  9 -0.109  -0.0543   0.00594 GTEX-117YX… Adipose_Subcutane… UBERON:00… gtex_v8  
#> 10  0.132  -0.0335  -0.0350  GTEX-11DXW… Adipose_Subcutane… UBERON:00… gtex_v8  
#> # ℹ 240 more rows

get_expression_pca(
  tissueSiteDetailIds = "Adipose_Subcutaneous",
  sampleId = "GTEX-1117F-0226-SM-5GZZ7"
)
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 1
#> # A tibble: 1 × 7
#>      pc1     pc2    pc3 sampleId         tissueSiteDetailId ontologyId datasetId
#>    <dbl>   <dbl>  <dbl> <chr>            <chr>              <chr>      <chr>    
#> 1 0.0385 -0.0178 0.0769 GTEX-1117F-0226… Adipose_Subcutane… UBERON:00… gtex_v8  
```
