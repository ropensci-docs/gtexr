# Get Genes

This service returns information about reference genes. A genome build
and GENCODE version must be provided.

- Genes are searchable by gene symbol, GENCODE ID and versioned GENCODE
  ID.

- Versioned GENCODE ID is recommended to ensure unique ID matching.

- By default, this service queries the genome build and GENCODE version
  used by the latest GTEx release.

[GTEx API Portal
documentation](https://gtexportal.org/api/v2/redoc#tag/Reference-Genome-Endpoints/operation/get_genes_api_v2_reference_gene_get)

## Usage

``` r
get_genes(
  geneIds,
  gencodeVersion = "v26",
  genomeBuild = "GRCh38/hg38",
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

- geneIds:

  A character vector of gene symbols, versioned gencodeIds, or
  unversioned gencodeIds.

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
[`get_gene_search()`](https://docs.ropensci.org/gtexr/reference/get_gene_search.md),
[`get_genomic_features()`](https://docs.ropensci.org/gtexr/reference/get_genomic_features.md),
[`get_gwas_catalog_by_location()`](https://docs.ropensci.org/gtexr/reference/get_gwas_catalog_by_location.md),
[`get_neighbor_gene()`](https://docs.ropensci.org/gtexr/reference/get_neighbor_gene.md),
[`get_transcripts()`](https://docs.ropensci.org/gtexr/reference/get_transcripts.md)

## Examples

``` r
get_genes(c("CRP", "IL6R"))
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 2
#> # A tibble: 2 × 15
#>   chromosome dataSource description    end entrezGeneId gencodeId gencodeVersion
#>   <chr>      <chr>      <chr>        <int>        <int> <chr>     <chr>         
#> 1 chr1       HAVANA     interleuki… 1.54e8         3570 ENSG0000… v26           
#> 2 chr1       HAVANA     C-reactive… 1.60e8         1401 ENSG0000… v26           
#> # ℹ 8 more variables: geneStatus <chr>, geneSymbol <chr>,
#> #   geneSymbolUpper <chr>, geneType <chr>, genomeBuild <chr>, start <int>,
#> #   strand <chr>, tss <int>
```
