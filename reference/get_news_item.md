# Get News Item

Getting all the news items from the database that are current.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Admin-Endpoints/operation/get_news_item_api_v2_admin_newsItem_get).

## Usage

``` r
get_news_item(
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

## See also

Other Admin Endpoints:
[`get_maintenance_message()`](https://docs.ropensci.org/gtexr/reference/get_maintenance_message.md)

## Examples

``` r
get_news_item()
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 34
#> # A tibble: 34 × 6
#>    title                                newsText  rank dateCreated release    id
#>    <chr>                                <chr>    <int> <chr>       <chr>   <int>
#>  1 New Top 50 Expressed Genes Visualiz… "The GT…   240 2018-04-04  news_i…   240
#>  2 New Multi-Gene Query Visualization   "The GT…   250 2018-04-04  news_i…   250
#>  3 New eQTL Dashboard Visualization     "The GT…   260 2018-04-04  news_i…   260
#>  4 Video Tutorial for the Gene-eQTL Vi… "Watch …   270 2018-04-05  news_i…   270
#>  5 Access GTEx Biospecimens Here        "We hav…   280 2018-05-10  news_i…   280
#>  6 Access GTEx Data Programmatically w… "You ca…   290 2018-09-20  news_i…   290
#>  7 Reuse GTEx Visualizations On Your W… "You ca…   300 2018-09-20  news_i…   300
#>  8 Use The GTEx Portal On Your Phone    "We hav…   310 2018-09-20  news_i…   310
#>  9 GTEx Portal Visualizations Updated   "We hav…   320 2018-12-06  news_i…   320
#> 10 Help Us Help You: New Feature Survey "PLEASE…   331 2019-02-06  news_i…   331
#> # ℹ 24 more rows
```
