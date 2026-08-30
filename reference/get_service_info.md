# Get Service Info

General information about the GTEx service.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/GTEx-Portal-API-Info/operation/get_service_info_api_v2__get).

## Usage

``` r
get_service_info(.return_raw = FALSE)
```

## Arguments

- .return_raw:

  Logical. If `TRUE`, return the raw API JSON response. Default =
  `FALSE`

## Value

A tibble. Or a list if `.return_raw = TRUE`.

## Examples

``` r
get_service_info()
#> # A tibble: 1 × 9
#>   id     name  version organization_name organization_url description contactUrl
#>   <chr>  <chr> <chr>   <chr>             <chr>            <chr>       <chr>     
#> 1 org.g… GTEx… 2.0.0   GTEx Project      https://gtexpor… This servi… https://g…
#> # ℹ 2 more variables: documentationUrl <chr>, environment <chr>
```
