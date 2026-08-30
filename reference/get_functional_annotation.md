# Get Functional Annotation

This endpoint retrieves the functional annotation of a certain
chromosome location. Default to most recent dataset release.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Datasets-Endpoints/operation/get_full_get_collapsed_gene_model_exon_api_v2_dataset_fullCollapsedGeneModelExon_get)

## Usage

``` r
get_functional_annotation(
  datasetId = "gtex_v8",
  chromosome,
  start,
  end,
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

- chromosome:

  String. One of "chr1", "chr2", "chr3", "chr4", "chr5", "chr6", "chr7",
  "chr8", "chr9", "chr10", "chr11", "chr12", "chr13", "chr14", "chr15",
  "chr16", "chr17", "chr18", "chr19", "chr20", "chr21", "chr22", "chrM",
  "chrX", "chrY".

- start:

  Integer.

- end:

  Integer.

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

Other Datasets Endpoints:
[`get_annotation()`](https://docs.ropensci.org/gtexr/reference/get_annotation.md),
[`get_collapsed_gene_model_exon()`](https://docs.ropensci.org/gtexr/reference/get_collapsed_gene_model_exon.md),
[`get_downloads_page_data()`](https://docs.ropensci.org/gtexr/reference/get_downloads_page_data.md),
[`get_file_list()`](https://docs.ropensci.org/gtexr/reference/get_file_list.md),
[`get_full_get_collapsed_gene_model_exon()`](https://docs.ropensci.org/gtexr/reference/get_full_get_collapsed_gene_model_exon.md),
[`get_linkage_disequilibrium_by_variant_data()`](https://docs.ropensci.org/gtexr/reference/get_linkage_disequilibrium_by_variant_data.md),
[`get_linkage_disequilibrium_data()`](https://docs.ropensci.org/gtexr/reference/get_linkage_disequilibrium_data.md),
[`get_sample_datasets()`](https://docs.ropensci.org/gtexr/reference/get_sample_datasets.md),
[`get_subject()`](https://docs.ropensci.org/gtexr/reference/get_subject.md),
[`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md),
[`get_variant()`](https://docs.ropensci.org/gtexr/reference/get_variant.md),
[`get_variant_by_location()`](https://docs.ropensci.org/gtexr/reference/get_variant_by_location.md)

## Examples

``` r
get_functional_annotation(chromosome = "chr1", start = 192168000, end = 192169000)
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 3
#> # A tibble: 3 × 23
#>   variantId         enhancer promoter openChromatinRegion promoterFlankingRegion
#>   <chr>             <lgl>    <lgl>    <lgl>               <lgl>                 
#> 1 chr1_192168015_T… TRUE     FALSE    FALSE               FALSE                 
#> 2 chr1_192168266_T… TRUE     FALSE    FALSE               FALSE                 
#> 3 chr1_192168728_T… FALSE    FALSE    FALSE               FALSE                 
#> # ℹ 18 more variables: ctcfBindingSite <lgl>, tfBindingSite <lgl>,
#> #   `3PrimeUtrVariant` <lgl>, `5PrimeUtrVariant` <lgl>,
#> #   frameshiftVariant <lgl>, intronVariant <lgl>, missenseVariant <lgl>,
#> #   nonCodingTranscriptExonVariant <lgl>, spliceAcceptorVariant <lgl>,
#> #   spliceDonorVariant <lgl>, spliceRegionVariant <lgl>, stopGained <lgl>,
#> #   synonymousVariant <lgl>, chromosome <chr>, pos <int>, ref <chr>, alt <chr>,
#> #   datasetId <chr>
```
