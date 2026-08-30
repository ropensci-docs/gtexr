# Get Single Nucleus Gex Summary

Retrieve Summarized Single Nucleus Gene Expression Data.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Expression-Data-Endpoints/operation/get_single_nucleus_gex_summary_api_v2_expression_singleNucleusGeneExpressionSummary_get)

## Usage

``` r
get_single_nucleus_gex_summary(
  datasetId = "gtex_snrnaseq_pilot",
  tissueSiteDetailIds = NULL,
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

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
[`get_median_junction_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_junction_expression.md),
[`get_median_transcript_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_transcript_expression.md),
[`get_single_nucleus_gex()`](https://docs.ropensci.org/gtexr/reference/get_single_nucleus_gex.md),
[`get_top_expressed_genes()`](https://docs.ropensci.org/gtexr/reference/get_top_expressed_genes.md)

## Examples

``` r
# all tissues
get_single_nucleus_gex_summary()
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 114
#> # A tibble: 114 × 5
#>    tissueSiteDetailId ontologyId     datasetId           cellType       numCells
#>    <chr>              <chr>          <chr>               <chr>             <int>
#>  1 Muscle_Skeletal    UBERON:0011907 gtex_snrnaseq_pilot Myocyte (sk. …      769
#>  2 Muscle_Skeletal    UBERON:0011907 gtex_snrnaseq_pilot Myocyte (NMJ-…       95
#>  3 Muscle_Skeletal    UBERON:0011907 gtex_snrnaseq_pilot Endothelial c…     1124
#>  4 Muscle_Skeletal    UBERON:0011907 gtex_snrnaseq_pilot Myocyte (sk. …    20772
#>  5 Muscle_Skeletal    UBERON:0011907 gtex_snrnaseq_pilot Fibroblast         5944
#>  6 Muscle_Skeletal    UBERON:0011907 gtex_snrnaseq_pilot Pericyte/SMC        448
#>  7 Muscle_Skeletal    UBERON:0011907 gtex_snrnaseq_pilot Immune (DC/ma…      721
#>  8 Muscle_Skeletal    UBERON:0011907 gtex_snrnaseq_pilot Adipocyte           159
#>  9 Muscle_Skeletal    UBERON:0011907 gtex_snrnaseq_pilot Schwann cell         35
#> 10 Muscle_Skeletal    UBERON:0011907 gtex_snrnaseq_pilot Satellite cell      487
#> # ℹ 104 more rows

# filter for specific tissue
get_single_nucleus_gex_summary(tissueSiteDetailIds = c(
  "Breast_Mammary_Tissue",
  "Skin_Sun_Exposed_Lower_leg"
))
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 25
#> # A tibble: 25 × 5
#>    tissueSiteDetailId         ontologyId     datasetId         cellType numCells
#>    <chr>                      <chr>          <chr>             <chr>       <int>
#>  1 Breast_Mammary_Tissue      UBERON:0008367 gtex_snrnaseq_pi… Epithel…     4849
#>  2 Breast_Mammary_Tissue      UBERON:0008367 gtex_snrnaseq_pi… Adipocy…     1761
#>  3 Breast_Mammary_Tissue      UBERON:0008367 gtex_snrnaseq_pi… Immune …      358
#>  4 Breast_Mammary_Tissue      UBERON:0008367 gtex_snrnaseq_pi… Myoepit…      950
#>  5 Breast_Mammary_Tissue      UBERON:0008367 gtex_snrnaseq_pi… Fibrobl…      819
#>  6 Breast_Mammary_Tissue      UBERON:0008367 gtex_snrnaseq_pi… Endothe…      762
#>  7 Breast_Mammary_Tissue      UBERON:0008367 gtex_snrnaseq_pi… Endothe…      119
#>  8 Breast_Mammary_Tissue      UBERON:0008367 gtex_snrnaseq_pi… Pericyt…      152
#>  9 Skin_Sun_Exposed_Lower_leg UBERON:0004264 gtex_snrnaseq_pi… Sweat g…      300
#> 10 Skin_Sun_Exposed_Lower_leg UBERON:0004264 gtex_snrnaseq_pi… Epithel…       72
#> # ℹ 15 more rows
```
