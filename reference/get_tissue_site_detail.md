# Get Tissue Site Detail

Retrieve all tissue site detail information in the database

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Datasets-Endpoints/operation/get_tissue_site_detail_api_v2_dataset_tissueSiteDetail_get)

## Usage

``` r
get_tissue_site_detail(
  datasetId = "gtex_v8",
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
[`get_subject()`](https://docs.ropensci.org/gtexr/reference/get_subject.md),
[`get_variant()`](https://docs.ropensci.org/gtexr/reference/get_variant.md),
[`get_variant_by_location()`](https://docs.ropensci.org/gtexr/reference/get_variant_by_location.md)

## Examples

``` r
# returns a tibble with one row per tissue
get_tissue_site_detail()
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 54
#> # A tibble: 54 × 18
#>    tissueSiteDetailId  colorHex colorRgb datasetId eGeneCount expressedGeneCount
#>    <chr>               <chr>    <chr>    <chr>          <int>              <int>
#>  1 Adipose_Subcutaneo… FF6600   255,102… gtex_v8        15607              28830
#>  2 Adipose_Visceral_O… FFAA00   255,170… gtex_v8        12482              28881
#>  3 Adrenal_Gland       33DD33   51,221,… gtex_v8         8123              28235
#>  4 Artery_Aorta        FF5555   255,85,… gtex_v8        12493              28025
#>  5 Artery_Coronary     FFAA99   255,170… gtex_v8         6296              28462
#>  6 Artery_Tibial       FF0000   255,0,0  gtex_v8        15008              27217
#>  7 Bladder             AA0000   170,0,0  gtex_v8           NA              28949
#>  8 Brain_Amygdala      EEEE00   238,238… gtex_v8         3726              28196
#>  9 Brain_Anterior_cin… EEEE00   238,238… gtex_v8         5640              28921
#> 10 Brain_Caudate_basa… EEEE00   238,238… gtex_v8         8362              29230
#> # ℹ 44 more rows
#> # ℹ 12 more variables: hasEGenes <lgl>, hasSGenes <lgl>, mappedInHubmap <lgl>,
#> #   eqtlSampleSummary <list>, rnaSeqSampleSummary <list>, sGeneCount <int>,
#> #   samplingSite <chr>, tissueSite <chr>, tissueSiteDetail <chr>,
#> #   tissueSiteDetailAbbr <chr>, ontologyId <chr>, ontologyIri <chr>

# `eqtlSampleSummary` and `rnaSeqSampleSummary` are list columns
bladder_site_details <- get_tissue_site_detail() |>
  dplyr::filter(tissueSiteDetailId == "Bladder")
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 54

purrr::pluck(bladder_site_details, "eqtlSampleSummary", 1)
#> $totalCount
#> [1] 21
#> 
#> $female
#> $female$ageMax
#> [1] 59
#> 
#> $female$ageMin
#> [1] 27
#> 
#> $female$ageMean
#> [1] 43.6
#> 
#> $female$count
#> [1] 7
#> 
#> 
#> $male
#> $male$ageMax
#> [1] 61
#> 
#> $male$ageMin
#> [1] 21
#> 
#> $male$ageMean
#> [1] 46
#> 
#> $male$count
#> [1] 14
#> 
#> 

purrr::pluck(bladder_site_details, "rnaSeqSampleSummary", 1)
#> $totalCount
#> [1] 21
#> 
#> $female
#> $female$ageMax
#> [1] 59
#> 
#> $female$ageMin
#> [1] 27
#> 
#> $female$ageMean
#> [1] 43.6
#> 
#> $female$count
#> [1] 7
#> 
#> 
#> $male
#> $male$ageMax
#> [1] 61
#> 
#> $male$ageMin
#> [1] 21
#> 
#> $male$ageMean
#> [1] 46
#> 
#> $male$count
#> [1] 14
#> 
#> 
```
