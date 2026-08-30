# Get Transcripts

Find all transcripts of a reference gene.

- This service returns information about transcripts of the given
  versioned GENCODE ID.

- A genome build and GENCODE version must be provided.

- By default, this service queries the genome build and GENCODE version
  used by the latest GTEx release.

[GTEx API Portal
documentation](https://gtexportal.org/api/v2/redoc#tag/Reference-Genome-Endpoints/operation/get_transcripts_api_v2_reference_transcript_get)

## Usage

``` r
get_transcripts(
  gencodeId,
  gencodeVersion = "v26",
  genomeBuild = "GRCh38/hg38",
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

- gencodeId:

  String. A Versioned GENCODE ID of a gene, e.g. "ENSG00000065613.9".

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
[`get_genes()`](https://docs.ropensci.org/gtexr/reference/get_genes.md),
[`get_genomic_features()`](https://docs.ropensci.org/gtexr/reference/get_genomic_features.md),
[`get_gwas_catalog_by_location()`](https://docs.ropensci.org/gtexr/reference/get_gwas_catalog_by_location.md),
[`get_neighbor_gene()`](https://docs.ropensci.org/gtexr/reference/get_neighbor_gene.md)

## Examples

``` r
get_transcripts(gencodeId = "ENSG00000203782.5")
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 1
#> # A tibble: 1 × 11
#>    start    end featureType genomeBuild transcriptId source chromosome gencodeId
#>    <int>  <int> <chr>       <chr>       <chr>        <chr>  <chr>      <chr>    
#> 1 1.53e8 1.53e8 transcript  GRCh38/hg38 ENST0000036… HAVANA chr1       ENSG0000…
#> # ℹ 3 more variables: geneSymbol <chr>, gencodeVersion <chr>, strand <chr>
```
