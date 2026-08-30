# Get Image

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Histology-Endpoints/operation/get_image_api_v2_histology_image_get)

## Usage

``` r
get_image(
  tissueSampleIds = NULL,
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

- tissueSampleIds:

  Array of strings. A list of Tissue Sample ID(s).

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

## Examples

``` r
get_image()
#> Warning: ! Total number of items (25713) exceeds the selected maximum page size (250).
#> ✖ 25463 items were not retrieved.
#> ℹ To retrieve all available items, increase `itemsPerPage`, ensuring you reuse
#>   your original query parameters e.g. `get_image(<your_existing_parameters>,
#>   itemsPerPage = 100000)`
#> ℹ Alternatively, adjust global "gtexr.itemsPerPage" setting e.g.
#>   `options(list(gtexr.itemsPerPage = 100000))`
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 103
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 25713
#> # A tibble: 250 × 11
#>    ageBracket hardyScale hide  histologyImageId pathologyNotes   sex   subjectId
#>    <chr>      <chr>      <lgl> <chr>            <chr>            <chr> <chr>    
#>  1 60-69      Slow death FALSE GTEX-1117F-0126  6 pieces, minim… fema… GTEX-111…
#>  2 60-69      Slow death FALSE GTEX-1117F-0226  2 pieces, ~15% … fema… GTEX-111…
#>  3 60-69      Slow death FALSE GTEX-1117F-0326  2 pieces, clean… fema… GTEX-111…
#>  4 60-69      Slow death FALSE GTEX-1117F-0426  2 pieces, !5% f… fema… GTEX-111…
#>  5 60-69      Slow death FALSE GTEX-1117F-0526  2 pieces, clean… fema… GTEX-111…
#>  6 60-69      Slow death FALSE GTEX-1117F-0626  2 pieces, up to… fema… GTEX-111…
#>  7 60-69      Slow death FALSE GTEX-1117F-0726  2 pieces, no ab… fema… GTEX-111…
#>  8 60-69      Slow death FALSE GTEX-1117F-0826  2 pieces, exten… fema… GTEX-111…
#>  9 60-69      Slow death FALSE GTEX-1117F-0926  6 pieces, adher… fema… GTEX-111…
#> 10 60-69      Slow death FALSE GTEX-1117F-1026  2 pieces, moder… fema… GTEX-111…
#> # ℹ 240 more rows
#> # ℹ 4 more variables: tissueSiteDetail <chr>, sampleId <chr>,
#> #   tissueSampleId <chr>, pathologyNotesCategories <tibble[,31]>

# filter by `tissueSampleId`
result <- get_image(tissueSampleIds = "GTEX-1117F-0526")
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 1
print(result)
#> # A tibble: 1 × 11
#>   ageBracket hardyScale hide  histologyImageId pathologyNotes                   
#>   <chr>      <chr>      <lgl> <chr>            <chr>                            
#> 1 60-69      Slow death FALSE GTEX-1117F-0526  2 pieces, clean, Monckebeg media…
#> # ℹ 6 more variables: pathologyNotesCategories <tibble[,2]>, sampleId <chr>,
#> #   sex <chr>, subjectId <chr>, tissueSampleId <chr>, tissueSiteDetail <chr>

# note that `pathologyNotesCategories` (if present) is a list column
print(result$pathologyNotesCategories)
#> # A tibble: 1 × 2
#>   monckeberg sclerotic
#>   <lgl>      <lgl>    
#> 1 TRUE       TRUE     
```
