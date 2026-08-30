# Get Median Gene Expression

Find median gene expression data along with hierarchical clusters.

- Returns median gene expression in tissues.

- By default, this endpoint queries the latest GTEx release.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Expression-Data-Endpoints/operation/get_median_gene_expression_api_v2_expression_medianGeneExpression_get)

## Usage

``` r
get_median_gene_expression(
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
[`get_median_junction_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_junction_expression.md),
[`get_median_transcript_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_transcript_expression.md),
[`get_single_nucleus_gex()`](https://docs.ropensci.org/gtexr/reference/get_single_nucleus_gex.md),
[`get_single_nucleus_gex_summary()`](https://docs.ropensci.org/gtexr/reference/get_single_nucleus_gex_summary.md),
[`get_top_expressed_genes()`](https://docs.ropensci.org/gtexr/reference/get_top_expressed_genes.md)

## Examples

``` r
get_median_gene_expression(gencodeIds = "ENSG00000132693.12")
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 54
#> # A tibble: 54 × 7
#>    median tissueSiteDetailId     ontologyId datasetId gencodeId geneSymbol unit 
#>     <dbl> <chr>                  <chr>      <chr>     <chr>     <chr>      <chr>
#>  1 0.347  Adipose_Subcutaneous   UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  2 0.240  Adipose_Visceral_Omen… UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  3 0.384  Adrenal_Gland          UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  4 0.198  Artery_Aorta           UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  5 0.332  Artery_Coronary        UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  6 0.117  Artery_Tibial          UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  7 0.631  Bladder                UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  8 0.0347 Brain_Amygdala         UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  9 0.0433 Brain_Anterior_cingul… UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#> 10 0.0226 Brain_Caudate_basal_g… UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#> # ℹ 44 more rows
```
