# Get Top Expressed Genes

Find top expressed genes for a specified tissue.

- Returns top expressed genes for a specified tissue in a dataset,
  sorted by median expression.

- When the optional parameter filterMtGene is set to true, mitochondrial
  genes will be excluded from the results. By default, this service
  queries the latest GTEx release.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Expression-Data-Endpoints/operation/get_top_expressed_genes_api_v2_expression_topExpressedGene_get)

## Usage

``` r
get_top_expressed_genes(
  tissueSiteDetailId,
  datasetId = "gtex_v8",
  filterMtGene = TRUE,
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

- tissueSiteDetailId:

  String. The ID of the tissue of interest. Can be a GTEx specific ID
  (e.g. "Whole_Blood"; use
  [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  to see valid values) or an Ontology ID.

- datasetId:

  String. Unique identifier of a dataset. Usually includes a data source
  and data release. Options: "gtex_v8", "gtex_snrnaseq_pilot".

- filterMtGene:

  Logical. Exclude mitochondrial genes.

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
[`get_single_nucleus_gex_summary()`](https://docs.ropensci.org/gtexr/reference/get_single_nucleus_gex_summary.md)

## Examples

``` r
get_top_expressed_genes(tissueSiteDetailId = "Artery_Aorta")
#> Warning: ! Total number of items (56163) exceeds the selected maximum page size (250).
#> ✖ 55913 items were not retrieved.
#> ℹ To retrieve all available items, increase `itemsPerPage`, ensuring you reuse
#>   your original query parameters e.g.
#>   `get_top_expressed_genes(<your_existing_parameters>, itemsPerPage = 100000)`
#> ℹ Alternatively, adjust global "gtexr.itemsPerPage" setting e.g.
#>   `options(list(gtexr.itemsPerPage = 100000))`
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 225
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 56163
#> # A tibble: 250 × 7
#>    tissueSiteDetailId ontologyId     datasetId gencodeId geneSymbol median unit 
#>    <chr>              <chr>          <chr>     <chr>     <chr>       <dbl> <chr>
#>  1 Artery_Aorta       UBERON:0001496 gtex_v8   ENSG0000… MGP        11936. TPM  
#>  2 Artery_Aorta       UBERON:0001496 gtex_v8   ENSG0000… FTL         9196. TPM  
#>  3 Artery_Aorta       UBERON:0001496 gtex_v8   ENSG0000… ACTB        9154. TPM  
#>  4 Artery_Aorta       UBERON:0001496 gtex_v8   ENSG0000… BGN         8167. TPM  
#>  5 Artery_Aorta       UBERON:0001496 gtex_v8   ENSG0000… TAGLN       6099. TPM  
#>  6 Artery_Aorta       UBERON:0001496 gtex_v8   ENSG0000… ACTA2       5736. TPM  
#>  7 Artery_Aorta       UBERON:0001496 gtex_v8   ENSG0000… IGFBP7      5639. TPM  
#>  8 Artery_Aorta       UBERON:0001496 gtex_v8   ENSG0000… MYL9        4275. TPM  
#>  9 Artery_Aorta       UBERON:0001496 gtex_v8   ENSG0000… HSPB1       3780. TPM  
#> 10 Artery_Aorta       UBERON:0001496 gtex_v8   ENSG0000… FLNA        3732. TPM  
#> # ℹ 240 more rows
```
