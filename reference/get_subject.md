# Get Subject

This service returns information of subjects used in analyses from all
datasets. Results may be filtered by dataset ID, subject ID, sex, age
bracket or Hardy Scale. By default, this service queries the latest GTEx
release.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Datasets-Endpoints/operation/get_subject_api_v2_dataset_subject_get)

## Usage

``` r
get_subject(
  datasetId = "gtex_v8",
  sex = NULL,
  ageBrackets = NULL,
  hardyScale = NULL,
  subjectIds = NULL,
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

- sex:

  String. Options: "male", "female".

- ageBrackets:

  The age bracket(s) of the donors of interest. Options: "20-29",
  "30-39", "40-49", "50-59", "60-69", "70-79".

- hardyScale:

  String A Hardy Scale of interest. Options: "Ventilator case", "Fast
  death - violent", "Fast death - natural causes", "Intermediate death",
  "Slow death".

- subjectIds:

  Character vector. GTEx subject ID.

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
[`get_functional_annotation()`](https://docs.ropensci.org/gtexr/reference/get_functional_annotation.md),
[`get_linkage_disequilibrium_by_variant_data()`](https://docs.ropensci.org/gtexr/reference/get_linkage_disequilibrium_by_variant_data.md),
[`get_linkage_disequilibrium_data()`](https://docs.ropensci.org/gtexr/reference/get_linkage_disequilibrium_data.md),
[`get_sample_datasets()`](https://docs.ropensci.org/gtexr/reference/get_sample_datasets.md),
[`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md),
[`get_variant()`](https://docs.ropensci.org/gtexr/reference/get_variant.md),
[`get_variant_by_location()`](https://docs.ropensci.org/gtexr/reference/get_variant_by_location.md)

## Examples

``` r
get_subject()
#> Warning: ! Total number of items (979) exceeds the selected maximum page size (250).
#> ✖ 729 items were not retrieved.
#> ℹ To retrieve all available items, increase `itemsPerPage`, ensuring you reuse
#>   your original query parameters e.g. `get_subject(<your_existing_parameters>,
#>   itemsPerPage = 100000)`
#> ℹ Alternatively, adjust global "gtexr.itemsPerPage" setting e.g.
#>   `options(list(gtexr.itemsPerPage = 100000))`
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 4
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 979
#> # A tibble: 250 × 5
#>    hardyScale                  ageBracket subjectId  sex    datasetId
#>    <chr>                       <chr>      <chr>      <chr>  <chr>    
#>  1 Slow death                  60-69      GTEX-1117F female gtex_v8  
#>  2 Ventilator case             50-59      GTEX-111CU male   gtex_v8  
#>  3 Fast death - violent        60-69      GTEX-111FC male   gtex_v8  
#>  4 Intermediate death          60-69      GTEX-111VG male   gtex_v8  
#>  5 Ventilator case             60-69      GTEX-111YS male   gtex_v8  
#>  6 Ventilator case             60-69      GTEX-1122O female gtex_v8  
#>  7 Fast death - natural causes 60-69      GTEX-1128S female gtex_v8  
#>  8 NA                          60-69      GTEX-113IC male   gtex_v8  
#>  9 Fast death - natural causes 50-59      GTEX-113JC female gtex_v8  
#> 10 Fast death - natural causes 60-69      GTEX-117XS male   gtex_v8  
#> # ℹ 240 more rows
```
