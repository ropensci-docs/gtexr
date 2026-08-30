# Get Linkage Disequilibrium By Variant Data

Find linkage disequilibrium (LD) data for a given variant

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Datasets-Endpoints/operation/get_linkage_disequilibrium_by_variant_data_api_v2_dataset_ldByVariant_get)

## Usage

``` r
get_linkage_disequilibrium_by_variant_data(
  variantId,
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

- variantId:

  String. A gtex variant ID.

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
[`get_linkage_disequilibrium_data()`](https://docs.ropensci.org/gtexr/reference/get_linkage_disequilibrium_data.md),
[`get_sample_datasets()`](https://docs.ropensci.org/gtexr/reference/get_sample_datasets.md),
[`get_subject()`](https://docs.ropensci.org/gtexr/reference/get_subject.md),
[`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md),
[`get_variant()`](https://docs.ropensci.org/gtexr/reference/get_variant.md),
[`get_variant_by_location()`](https://docs.ropensci.org/gtexr/reference/get_variant_by_location.md)

## Examples

``` r
get_linkage_disequilibrium_by_variant_data("chr1_159245536_C_T_b38")
#> Warning: ! Total number of items (503) exceeds the selected maximum page size (250).
#> ✖ 253 items were not retrieved.
#> ℹ To retrieve all available items, increase `itemsPerPage`, ensuring you reuse
#>   your original query parameters e.g.
#>   `get_linkage_disequilibrium_by_variant_data(<your_existing_parameters>,
#>   itemsPerPage = 100000)`
#> ℹ Alternatively, adjust global "gtexr.itemsPerPage" setting e.g.
#>   `options(list(gtexr.itemsPerPage = 100000))`
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 3
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 503
#> # A tibble: 250 × 3
#>    variantId_1             variantId_2               ld
#>    <chr>                   <chr>                  <dbl>
#>  1 chr1_159163610_GA_G_b38 chr1_159245536_C_T_b38 0.114
#>  2 chr1_159163924_G_A_b38  chr1_159245536_C_T_b38 0.114
#>  3 chr1_159164864_T_C_b38  chr1_159245536_C_T_b38 0.114
#>  4 chr1_159165054_A_G_b38  chr1_159245536_C_T_b38 0.113
#>  5 chr1_159165563_T_C_b38  chr1_159245536_C_T_b38 0.113
#>  6 chr1_159174791_T_C_b38  chr1_159245536_C_T_b38 0.252
#>  7 chr1_159176518_G_T_b38  chr1_159245536_C_T_b38 0.146
#>  8 chr1_159176900_C_A_b38  chr1_159245536_C_T_b38 0.271
#>  9 chr1_159177147_A_T_b38  chr1_159245536_C_T_b38 0.274
#> 10 chr1_159179691_T_C_b38  chr1_159245536_C_T_b38 0.253
#> # ℹ 240 more rows
```
