# Get Linkage Disequilibrium Data

Find linkage disequilibrium (LD) data for a given gene.

This endpoint returns linkage disequilibrium data for the cis-eQTLs
found associated with the provided gene in a specified dataset. Results
are queried by gencode ID. By default, the service queries the latest
GTEx release. Specify a dataset ID to fetch results from a different
dataset.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Datasets-Endpoints/operation/get_variant_by_location_api_v2_dataset_variantByLocation_get)

## Usage

``` r
get_linkage_disequilibrium_data(
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
[`get_full_get_collapsed_gene_model_exon()`](https://docs.ropensci.org/gtexr/reference/get_full_get_collapsed_gene_model_exon.md),
[`get_functional_annotation()`](https://docs.ropensci.org/gtexr/reference/get_functional_annotation.md),
[`get_linkage_disequilibrium_by_variant_data()`](https://docs.ropensci.org/gtexr/reference/get_linkage_disequilibrium_by_variant_data.md),
[`get_sample_datasets()`](https://docs.ropensci.org/gtexr/reference/get_sample_datasets.md),
[`get_subject()`](https://docs.ropensci.org/gtexr/reference/get_subject.md),
[`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md),
[`get_variant()`](https://docs.ropensci.org/gtexr/reference/get_variant.md),
[`get_variant_by_location()`](https://docs.ropensci.org/gtexr/reference/get_variant_by_location.md)

## Examples

``` r
get_linkage_disequilibrium_data(gencodeId = "ENSG00000132693.12")
#> Warning: ! Total number of items (3558) exceeds the selected maximum page size (250).
#> ✖ 3308 items were not retrieved.
#> ℹ To retrieve all available items, increase `itemsPerPage`, ensuring you reuse
#>   your original query parameters e.g.
#>   `get_linkage_disequilibrium_data(<your_existing_parameters>, itemsPerPage =
#>   100000)`
#> ℹ Alternatively, adjust global "gtexr.itemsPerPage" setting e.g.
#>   `options(list(gtexr.itemsPerPage = 100000))`
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 15
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 3558
#> # A tibble: 250 × 3
#>    variantId_1            variantId_2                         ld
#>    <chr>                  <chr>                            <dbl>
#>  1 chr1_159230230_G_T_b38 chr1_159230339_A_C_b38           1    
#>  2 chr1_159230230_G_T_b38 chr1_159245536_C_T_b38           0.971
#>  3 chr1_159230230_G_T_b38 chr1_159302270_T_C_b38           0.717
#>  4 chr1_159230230_G_T_b38 chr1_159343657_A_T_b38           0.302
#>  5 chr1_159230230_G_T_b38 chr1_159344052_G_A_b38           0.300
#>  6 chr1_159230230_G_T_b38 chr1_159347493_G_A_b38           0.300
#>  7 chr1_159230230_G_T_b38 chr1_159350390_C_A_b38           0.300
#>  8 chr1_159230230_G_T_b38 chr1_159351189_G_A_b38           0.300
#>  9 chr1_159230230_G_T_b38 chr1_159359256_C_A_b38           0.302
#> 10 chr1_159230230_G_T_b38 chr1_159360755_ATACATAAGTG_A_b38 0.300
#> # ℹ 240 more rows
```
