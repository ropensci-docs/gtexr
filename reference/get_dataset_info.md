# Get Dataset Info

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Metadata-Endpoints/operation/get_dataset_info_api_v2_metadata_dataset_get)

## Usage

``` r
get_dataset_info(
  datasetId = NULL,
  organizationName = NULL,
  .return_raw = FALSE
)
```

## Arguments

- datasetId:

  String. Unique identifier of a dataset. Usually includes a data source
  and data release. Options: "gtex_v8", "gtex_snrnaseq_pilot".

- organizationName:

  String. Options: "GTEx Consortium" "Kid's First".

- .return_raw:

  Logical. If `TRUE`, return the raw API JSON response. Default =
  `FALSE`

## Value

A tibble. Or a list if `.return_raw = TRUE`.

## Examples

``` r
get_dataset_info(datasetId = "gtex_v8", organizationName = "GTEx Consortium")
#> # A tibble: 0 × 0
```
