# Get Median Junction Expression

Find junction gene expression data.

- Returns median junction read counts in tissues of a given gene from
  all known transcripts.

- Results may be filtered by dataset or tissue.

By default, this service queries the latest GTEx release.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Expression-Data-Endpoints/operation/get_median_junction_expression_api_v2_expression_medianJunctionExpression_get)

## Usage

``` r
get_median_junction_expression(
  gencodeIds,
  datasetId = "gtex_v8",
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

Other Expression Data Endpoints:
[`get_clustered_median_exon_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_exon_expression.md),
[`get_clustered_median_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_gene_expression.md),
[`get_clustered_median_junction_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_junction_expression.md),
[`get_clustered_median_transcript_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_transcript_expression.md),
[`get_expression_pca()`](https://docs.ropensci.org/gtexr/reference/get_expression_pca.md),
[`get_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_gene_expression.md),
[`get_median_exon_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_exon_expression.md),
[`get_median_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_gene_expression.md),
[`get_median_transcript_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_transcript_expression.md),
[`get_single_nucleus_gex()`](https://docs.ropensci.org/gtexr/reference/get_single_nucleus_gex.md),
[`get_single_nucleus_gex_summary()`](https://docs.ropensci.org/gtexr/reference/get_single_nucleus_gex_summary.md),
[`get_top_expressed_genes()`](https://docs.ropensci.org/gtexr/reference/get_top_expressed_genes.md)

## Examples

``` r
get_median_junction_expression(gencodeIds = "ENSG00000132693.12")
#> Warning: ! Total number of items (378) exceeds the selected maximum page size (250).
#> ✖ 128 items were not retrieved.
#> ℹ To retrieve all available items, increase `itemsPerPage`, ensuring you reuse
#>   your original query parameters e.g.
#>   `get_median_junction_expression(<your_existing_parameters>, itemsPerPage =
#>   100000)`
#> ℹ Alternatively, adjust global "gtexr.itemsPerPage" setting e.g.
#>   `options(list(gtexr.itemsPerPage = 100000))`
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 2
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 378
#> # A tibble: 250 × 8
#>    median junctionId           tissueSiteDetailId ontologyId datasetId gencodeId
#>     <dbl> <chr>                <chr>              <chr>      <chr>     <chr>    
#>  1      0 chr1_159712581_1597… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000…
#>  2      0 chr1_159712795_1597… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000…
#>  3      0 chr1_159712795_1597… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000…
#>  4      0 chr1_159713604_1597… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000…
#>  5      0 chr1_159713641_1597… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000…
#>  6      0 chr1_159713973_1597… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000…
#>  7      0 chr1_159714139_1597… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000…
#>  8      0 chr1_159712581_1597… Adipose_Visceral_… UBERON:00… gtex_v8   ENSG0000…
#>  9      0 chr1_159712795_1597… Adipose_Visceral_… UBERON:00… gtex_v8   ENSG0000…
#> 10      0 chr1_159712795_1597… Adipose_Visceral_… UBERON:00… gtex_v8   ENSG0000…
#> # ℹ 240 more rows
#> # ℹ 2 more variables: geneSymbol <chr>, unit <chr>
```
