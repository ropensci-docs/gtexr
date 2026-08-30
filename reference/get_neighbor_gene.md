# Get Neighbor Gene

Find all neighboring genes on a certain chromosome around a position
with a certain window size.

[GTEx API Portal
documentation](https://gtexportal.org/api/v2/redoc#tag/Reference-Genome-Endpoints/operation/get_neighbor_gene_api_v2_reference_neighborGene_get)

## Usage

``` r
get_neighbor_gene(
  pos,
  chromosome,
  bp_window,
  page = 0,
  gencodeVersion = "v26",
  genomeBuild = "GRCh38/hg38",
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

- pos:

  Integer.

- chromosome:

  String. One of "chr1", "chr2", "chr3", "chr4", "chr5", "chr6", "chr7",
  "chr8", "chr9", "chr10", "chr11", "chr12", "chr13", "chr14", "chr15",
  "chr16", "chr17", "chr18", "chr19", "chr20", "chr21", "chr22", "chrM",
  "chrX", "chrY".

- bp_window:

  Integer.

- page:

  Integer (default = 0).

- gencodeVersion:

  String (default = "v26"). GENCODE annotation release. Either "v26" or
  "v19".

- genomeBuild:

  String. Options: "GRCh38/hg38", "GRCh37/hg19". Default =
  "GRCh38/hg38".

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
[`get_gene_search()`](https://docs.ropensci.org/gtexr/reference/get_gene_search.md),
[`get_genes()`](https://docs.ropensci.org/gtexr/reference/get_genes.md),
[`get_genomic_features()`](https://docs.ropensci.org/gtexr/reference/get_genomic_features.md),
[`get_gwas_catalog_by_location()`](https://docs.ropensci.org/gtexr/reference/get_gwas_catalog_by_location.md),
[`get_transcripts()`](https://docs.ropensci.org/gtexr/reference/get_transcripts.md)

## Examples

``` r
get_neighbor_gene(pos = 1000000, chromosome = "chr1", bp_window = 10000)
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 4
#> # A tibble: 4 × 15
#>   chromosome dataSource description      end gencodeId gencodeVersion geneStatus
#>   <chr>      <chr>      <chr>          <int> <chr>     <chr>          <chr>     
#> 1 chr1       HAVANA     novel transc… 9.98e5 ENSG0000… v26            ""        
#> 2 chr1       HAVANA     hes family b… 1.00e6 ENSG0000… v26            ""        
#> 3 chr1       HAVANA     ISG15 ubiqui… 1.01e6 ENSG0000… v26            ""        
#> 4 chr1       HAVANA     ribosomal pr… 1.01e6 ENSG0000… v26            ""        
#> # ℹ 8 more variables: geneSymbol <chr>, geneSymbolUpper <chr>, geneType <chr>,
#> #   genomeBuild <chr>, start <int>, strand <chr>, tss <int>, entrezGeneId <int>
```
