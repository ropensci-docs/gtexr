# Get Gene Expression

Find normalized gene expression data.

- Returns normalized gene expression in tissues at the sample level.

- Results may be filtered by dataset, gene or tissue, but at least one
  gene must be provided.

By default, this service queries the latest GTEx release.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Expression-Data-Endpoints/operation/get_gene_expression_api_v2_expression_geneExpression_get)

## Usage

``` r
get_gene_expression(
  gencodeIds,
  datasetId = "gtex_v8",
  tissueSiteDetailIds = NULL,
  attributeSubset = NULL,
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

- attributeSubset:

  String. Examples include but are not limited to "sex", "ageBracket"

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
[`get_median_exon_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_exon_expression.md),
[`get_median_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_gene_expression.md),
[`get_median_junction_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_junction_expression.md),
[`get_median_transcript_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_transcript_expression.md),
[`get_single_nucleus_gex()`](https://docs.ropensci.org/gtexr/reference/get_single_nucleus_gex.md),
[`get_single_nucleus_gex_summary()`](https://docs.ropensci.org/gtexr/reference/get_single_nucleus_gex_summary.md),
[`get_top_expressed_genes()`](https://docs.ropensci.org/gtexr/reference/get_top_expressed_genes.md)

## Examples

``` r
# multiple genes, selected tissues
get_gene_expression(
  gencodeIds = c(
    "ENSG00000132693.12",
    "ENSG00000203782.5"
  ),
  tissueSiteDetailIds = c("Thyroid", "Whole_Blood")
)
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 4
#> # A tibble: 4 × 8
#>   data        tissueSiteDetailId ontologyId datasetId gencodeId geneSymbol unit 
#>   <list>      <chr>              <chr>      <chr>     <chr>     <chr>      <chr>
#> 1 <dbl [653]> Thyroid            UBERON:00… gtex_v8   ENSG0000… LOR        TPM  
#> 2 <dbl [755]> Whole_Blood        UBERON:00… gtex_v8   ENSG0000… LOR        TPM  
#> 3 <dbl [653]> Thyroid            UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#> 4 <dbl [755]> Whole_Blood        UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#> # ℹ 1 more variable: subsetGroup <lgl>

# single gene, selected (single) tissue
get_gene_expression(
  gencodeIds = "ENSG00000132693.12",
  tissueSiteDetailIds = "Whole_Blood"
)
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 1
#> # A tibble: 1 × 8
#>   data        tissueSiteDetailId ontologyId datasetId gencodeId geneSymbol unit 
#>   <list>      <chr>              <chr>      <chr>     <chr>     <chr>      <chr>
#> 1 <dbl [755]> Whole_Blood        UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#> # ℹ 1 more variable: subsetGroup <lgl>

# subset by sex
get_gene_expression(
  gencodeIds = "ENSG00000132693.12",
  tissueSiteDetailIds = "Whole_Blood",
  attributeSubset = "sex"
)
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 1
#> # A tibble: 1 × 8
#>   data        tissueSiteDetailId ontologyId datasetId gencodeId geneSymbol unit 
#>   <list>      <chr>              <chr>      <chr>     <chr>     <chr>      <chr>
#> 1 <dbl [755]> Whole_Blood        UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#> # ℹ 1 more variable: subsetGroup <lgl>

# subset by age bracket
get_gene_expression(
  gencodeIds = "ENSG00000132693.12",
  tissueSiteDetailIds = "Whole_Blood",
  attributeSubset = "ageBracket"
)
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 1
#> # A tibble: 1 × 8
#>   data        tissueSiteDetailId ontologyId datasetId gencodeId geneSymbol unit 
#>   <list>      <chr>              <chr>      <chr>     <chr>     <chr>      <chr>
#> 1 <dbl [755]> Whole_Blood        UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#> # ℹ 1 more variable: subsetGroup <lgl>
```
