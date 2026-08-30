# Get Full Get Collapsed Gene Model Exon

This service allows the user to query the full Collapsed Gene Model Exon
of a specific gene by gencode ID

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Datasets-Endpoints/operation/get_full_get_collapsed_gene_model_exon_api_v2_dataset_fullCollapsedGeneModelExon_get)

## Usage

``` r
get_full_get_collapsed_gene_model_exon(
  gencodeId,
  datasetId = "gtex_v8",
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

- gencodeId:

  String. A Versioned GENCODE ID of a gene, e.g. "ENSG00000065613.9".

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

Other Datasets Endpoints:
[`get_annotation()`](https://docs.ropensci.org/gtexr/reference/get_annotation.md),
[`get_collapsed_gene_model_exon()`](https://docs.ropensci.org/gtexr/reference/get_collapsed_gene_model_exon.md),
[`get_downloads_page_data()`](https://docs.ropensci.org/gtexr/reference/get_downloads_page_data.md),
[`get_file_list()`](https://docs.ropensci.org/gtexr/reference/get_file_list.md),
[`get_functional_annotation()`](https://docs.ropensci.org/gtexr/reference/get_functional_annotation.md),
[`get_linkage_disequilibrium_by_variant_data()`](https://docs.ropensci.org/gtexr/reference/get_linkage_disequilibrium_by_variant_data.md),
[`get_linkage_disequilibrium_data()`](https://docs.ropensci.org/gtexr/reference/get_linkage_disequilibrium_data.md),
[`get_sample_datasets()`](https://docs.ropensci.org/gtexr/reference/get_sample_datasets.md),
[`get_subject()`](https://docs.ropensci.org/gtexr/reference/get_subject.md),
[`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md),
[`get_variant()`](https://docs.ropensci.org/gtexr/reference/get_variant.md),
[`get_variant_by_location()`](https://docs.ropensci.org/gtexr/reference/get_variant_by_location.md)

## Examples

``` r
get_full_get_collapsed_gene_model_exon(gencodeId = "ENSG00000203782.5")
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 2
#> # A tibble: 2 × 14
#>   featureType       end genomeBuild chromosome exonNumber geneSymbolUpper exonId
#>   <chr>           <int> <chr>       <chr>      <chr>      <chr>           <chr> 
#> 1 exon        153259733 GRCh38/hg38 chr1       1          LOR             ENSG0…
#> 2 exon        153262122 GRCh38/hg38 chr1       2          LOR             ENSG0…
#> # ℹ 7 more variables: datasetId <chr>, start <int>, dataSource <chr>,
#> #   gencodeId <chr>, geneSymbol <chr>, gencodeVersion <chr>, strand <chr>
```
