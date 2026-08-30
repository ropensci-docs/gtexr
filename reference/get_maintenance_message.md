# Get Maintenance Message

Getting all the maintenance messages from the database that are enabled.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Admin-Endpoints/operation/get_maintenance_message_api_v2_admin_maintenanceMessage_get).

## Usage

``` r
get_maintenance_message(
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

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

## Details

Note this typically returns an empty tibble.

## See also

Other Admin Endpoints:
[`get_news_item()`](https://docs.ropensci.org/gtexr/reference/get_news_item.md)

## Examples

``` r
get_maintenance_message()
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 0
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 0
#> # A tibble: 0 × 0
```
