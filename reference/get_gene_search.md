# Get Gene Search

Find genes that are partial or complete match of a gene_id

- gene_id could be a gene symbol, a gencode ID, or an Ensemble ID

- Gencode Version and Genome Build must be specified

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Reference-Genome-Endpoints/operation/get_gene_search_api_v2_reference_geneSearch_get)

## Usage

``` r
get_gene_search(
  geneId,
  gencodeVersion = "v26",
  genomeBuild = "GRCh38/hg38",
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

- geneId:

  String. A gene symbol, a gencode ID, or an Ensemble ID.

- gencodeVersion:

  String (default = "v26"). GENCODE annotation release. Either "v26" or
  "v19".

- genomeBuild:

  String. Options: "GRCh38/hg38", "GRCh37/hg19". Default =
  "GRCh38/hg38".

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

Other Reference Genome Endpoints:
[`get_exons()`](https://docs.ropensci.org/gtexr/reference/get_exons.md),
[`get_genes()`](https://docs.ropensci.org/gtexr/reference/get_genes.md),
[`get_genomic_features()`](https://docs.ropensci.org/gtexr/reference/get_genomic_features.md),
[`get_gwas_catalog_by_location()`](https://docs.ropensci.org/gtexr/reference/get_gwas_catalog_by_location.md),
[`get_neighbor_gene()`](https://docs.ropensci.org/gtexr/reference/get_neighbor_gene.md),
[`get_transcripts()`](https://docs.ropensci.org/gtexr/reference/get_transcripts.md)

## Examples

``` r
get_gene_search("CRP")
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 2
#> # A tibble: 2 × 15
#>   chromosome dataSource description      end gencodeId gencodeVersion geneStatus
#>   <chr>      <chr>      <chr>          <int> <chr>     <chr>          <chr>     
#> 1 chr1       HAVANA     C-reactive p… 1.60e8 ENSG0000… v26            ""        
#> 2 chr1       HAVANA     C-reactive p… 1.60e8 ENSG0000… v26            ""        
#> # ℹ 8 more variables: geneSymbol <chr>, geneSymbolUpper <chr>, geneType <chr>,
#> #   genomeBuild <chr>, start <int>, strand <chr>, tss <int>, entrezGeneId <int>
```
