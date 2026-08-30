# Get Single Nucleus Gex

Retrieve Single Nucleus Gene Expression Data for a given Gene.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Expression-Data-Endpoints/operation/get_single_nucleus_gex_api_v2_expression_singleNucleusGeneExpression_get)

## Usage

``` r
get_single_nucleus_gex(
  gencodeIds,
  datasetId = "gtex_snrnaseq_pilot",
  tissueSiteDetailIds = NULL,
  excludeDataArray = TRUE,
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

- tissueSiteDetailIds:

  Character vector of IDs for tissues of interest. Can be GTEx specific
  IDs (e.g. "Whole_Blood"; use
  [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  to see valid values) or Ontology IDs.

- excludeDataArray:

  String. Options are TRUE or FALSE

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
[`get_expression_pca()`](https://docs.ropensci.org/gtexr/reference/get_expression_pca.md),
[`get_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_gene_expression.md),
[`get_median_exon_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_exon_expression.md),
[`get_median_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_gene_expression.md),
[`get_median_junction_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_junction_expression.md),
[`get_median_transcript_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_transcript_expression.md),
[`get_single_nucleus_gex_summary()`](https://docs.ropensci.org/gtexr/reference/get_single_nucleus_gex_summary.md),
[`get_top_expressed_genes()`](https://docs.ropensci.org/gtexr/reference/get_top_expressed_genes.md)

## Examples

``` r
# Search for one or more genes - returns a tibble with one row per tissue.
# Column "cellTypes" now contains a tibble of expression summary data, with
# one row for each cell type
get_single_nucleus_gex(gencodeIds = c(
  "ENSG00000203782.5",
  "ENSG00000132693.12"
))
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 14
#> # A tibble: 14 × 7
#>    tissueSiteDetailId  ontologyId datasetId gencodeId geneSymbol cellTypes unit 
#>    <chr>               <chr>      <chr>     <chr>     <chr>      <list>    <chr>
#>  1 Muscle_Skeletal     UBERON:00… gtex_snr… ENSG0000… LOR        <tibble>  log(…
#>  2 Breast_Mammary_Tis… UBERON:00… gtex_snr… ENSG0000… LOR        <tibble>  log(…
#>  3 Esophagus_Mucosa    UBERON:00… gtex_snr… ENSG0000… LOR        <tibble>  log(…
#>  4 Esophagus_Muscular… UBERON:00… gtex_snr… ENSG0000… LOR        <tibble>  log(…
#>  5 Lung                UBERON:00… gtex_snr… ENSG0000… LOR        <tibble>  log(…
#>  6 Prostate            UBERON:00… gtex_snr… ENSG0000… LOR        <tibble>  log(…
#>  7 Skin_Sun_Exposed_L… UBERON:00… gtex_snr… ENSG0000… LOR        <tibble>  log(…
#>  8 Muscle_Skeletal     UBERON:00… gtex_snr… ENSG0000… CRP        <tibble>  log(…
#>  9 Breast_Mammary_Tis… UBERON:00… gtex_snr… ENSG0000… CRP        <tibble>  log(…
#> 10 Esophagus_Mucosa    UBERON:00… gtex_snr… ENSG0000… CRP        <tibble>  log(…
#> 11 Esophagus_Muscular… UBERON:00… gtex_snr… ENSG0000… CRP        <tibble>  log(…
#> 12 Heart_Left_Ventric… UBERON:00… gtex_snr… ENSG0000… CRP        <tibble>  log(…
#> 13 Lung                UBERON:00… gtex_snr… ENSG0000… CRP        <tibble>  log(…
#> 14 Prostate            UBERON:00… gtex_snr… ENSG0000… CRP        <tibble>  log(…

# `excludeDataArray = FALSE` - expression values are stored under "celltypes"
# in an additional column called "data"
response <- get_single_nucleus_gex(
  gencodeIds = "ENSG00000132693.12",
  excludeDataArray = FALSE,
  itemsPerPage = 2
)
#> Warning: ! Total number of items (7) exceeds the selected maximum page size (2).
#> ✖ 5 items were not retrieved.
#> ℹ To retrieve all available items, increase `itemsPerPage`, ensuring you reuse
#>   your original query parameters e.g.
#>   `get_single_nucleus_gex(<your_existing_parameters>, itemsPerPage = 100000)`
#> ℹ Alternatively, adjust global "gtexr.itemsPerPage" setting e.g.
#>   `options(list(gtexr.itemsPerPage = 100000))`
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 4
#> • page = 0
#> • maxItemsPerPage = 2
#> • totalNumberOfItems = 7

response
#> # A tibble: 2 × 7
#>   tissueSiteDetailId   ontologyId datasetId gencodeId geneSymbol cellTypes unit 
#>   <chr>                <chr>      <chr>     <chr>     <chr>      <list>    <chr>
#> 1 Muscle_Skeletal      UBERON:00… gtex_snr… ENSG0000… CRP        <tibble>  log(…
#> 2 Breast_Mammary_Tiss… UBERON:00… gtex_snr… ENSG0000… CRP        <tibble>  log(…

# "cellTypes" contains a tibble of data with one row for each
# cell type e.g. for Breast_Mammary_Tissue
response$cellTypes[[2]]
#> # A tibble: 2 × 8
#>   cellType                  count meanWithZeros meanWithoutZeros medianWithZeros
#>   <chr>                     <int>         <dbl>            <dbl>           <dbl>
#> 1 Epithelial cell (luminal)     2      0.000902             2.19               0
#> 2 Endothelial cell (vascul…     1      0.00401              3.05               0
#> # ℹ 3 more variables: medianWithoutZeros <dbl>, numZeros <int>, data <list>

# when `excludeDataArray = FALSE`, expression values are stored in "data"
# e.g. for Breast_Mammary_Tissue, Epithelial cell (luminal):
response$cellTypes[[2]]$data[[1]]
#> [1] 1.593315 2.782725
```
