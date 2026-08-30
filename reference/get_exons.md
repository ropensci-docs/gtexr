# Get Exons

This service returns exons from all known transcripts of the given gene.

- A versioned GENCODE ID is required to ensure that all exons are from a
  single gene.

- A dataset ID or both GENCODE version and genome build must be
  provided.

- Although annotated exons are not dataset dependent, specifying a
  dataset here is equivalent to specifying the GENCODE version and
  genome build used by that dataset.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Reference-Genome-Endpoints/operation/get_exons_api_v2_reference_exon_get)

## Usage

``` r
get_exons(
  gencodeIds,
  gencodeVersion = NULL,
  genomeBuild = NULL,
  datasetId = "gtex_v8",
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

- gencodeVersion:

  String (default = "v26"). GENCODE annotation release. Either "v26" or
  "v19".

- genomeBuild:

  String. Options: "GRCh38/hg38", "GRCh37/hg19". Default =
  "GRCh38/hg38".

- datasetId:

  String. Unique identifier of a dataset. Usually includes a data source
  and data release. Options: "gtex_v8", "gtex_snrnaseq_pilot".

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
[`get_gene_search()`](https://docs.ropensci.org/gtexr/reference/get_gene_search.md),
[`get_genes()`](https://docs.ropensci.org/gtexr/reference/get_genes.md),
[`get_genomic_features()`](https://docs.ropensci.org/gtexr/reference/get_genomic_features.md),
[`get_gwas_catalog_by_location()`](https://docs.ropensci.org/gtexr/reference/get_gwas_catalog_by_location.md),
[`get_neighbor_gene()`](https://docs.ropensci.org/gtexr/reference/get_neighbor_gene.md),
[`get_transcripts()`](https://docs.ropensci.org/gtexr/reference/get_transcripts.md)

## Examples

``` r
get_exons(gencodeIds = c("ENSG00000132693.12", "ENSG00000203782.5"))
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 23
#> # A tibble: 23 × 13
#>    featureType       end genomeBuild    start exonId source chromosome gencodeId
#>    <chr>           <int> <chr>          <int> <chr>  <chr>  <chr>      <chr>    
#>  1 exon        153259733 GRCh38/hg38   1.53e8 ENSE0… HAVANA chr1       ENSG0000…
#>  2 exon        153262122 GRCh38/hg38   1.53e8 ENSE0… HAVANA chr1       ENSG0000…
#>  3 exon        159714589 GRCh38/hg38   1.60e8 ENSE0… HAVANA chr1       ENSG0000…
#>  4 exon        159714138 GRCh38/hg38   1.60e8 ENSE0… HAVANA chr1       ENSG0000…
#>  5 exon        159713767 GRCh38/hg38   1.60e8 ENSE0… HAVANA chr1       ENSG0000…
#>  6 exon        159712794 GRCh38/hg38   1.60e8 ENSE0… HAVANA chr1       ENSG0000…
#>  7 exon        159714589 GRCh38/hg38   1.60e8 ENSE0… ENSEM… chr1       ENSG0000…
#>  8 exon        159713972 GRCh38/hg38   1.60e8 ENSE0… ENSEM… chr1       ENSG0000…
#>  9 exon        159712794 GRCh38/hg38   1.60e8 ENSE0… ENSEM… chr1       ENSG0000…
#> 10 exon        159714589 GRCh38/hg38   1.60e8 ENSE0… HAVANA chr1       ENSG0000…
#> # ℹ 13 more rows
#> # ℹ 5 more variables: transcriptId <chr>, geneSymbol <chr>,
#> #   gencodeVersion <chr>, strand <chr>, exonNumber <chr>
```
