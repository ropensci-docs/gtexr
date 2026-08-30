# Get Downloads Page Data

Retrieves all the files belonging to the given `project_id` for display
on the `Downloads Page`

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Datasets-Endpoints/operation/get_downloads_page_data_api_v2_dataset_openAccessFilesMetadata_get)

## Usage

``` r
get_downloads_page_data(project_id, .return_raw = FALSE)
```

## Arguments

- project_id:

  String. Options: "gtex", "adult-gtex", "egtex".

- .return_raw:

  Logical. If `TRUE`, return the raw API JSON response. Default =
  `FALSE`

## Value

A tibble. Or a list if `.return_raw = TRUE`.

## Details

Note: The GTEx Portal API documentation states "GTEx currently has one
project available: gtex". However, `project_id` values "adult-gtex" and
"egtex" both return results, whereas "gtex" does not (see examples).

## See also

Other Datasets Endpoints:
[`get_annotation()`](https://docs.ropensci.org/gtexr/reference/get_annotation.md),
[`get_collapsed_gene_model_exon()`](https://docs.ropensci.org/gtexr/reference/get_collapsed_gene_model_exon.md),
[`get_file_list()`](https://docs.ropensci.org/gtexr/reference/get_file_list.md),
[`get_full_get_collapsed_gene_model_exon()`](https://docs.ropensci.org/gtexr/reference/get_full_get_collapsed_gene_model_exon.md),
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
# "adult-gtex" (default `project_id` value) and "egtex" both return results
get_downloads_page_data("adult-gtex")
#> # A tibble: 9 × 6
#>   name                         displayName description order parent children    
#>   <chr>                        <chr>       <chr>       <int> <chr>  <list>      
#> 1 gs://adult-gtex/bulk-gex/    Bulk tissu… ""              1 gs://… <named list>
#> 2 gs://adult-gtex/bulk-qtl/    QTL         ""              2 gs://… <named list>
#> 3 gs://adult-gtex/single-cell/ Single cell ""              3 gs://… <named list>
#> 4 gs://adult-gtex/long-read-d… Long read … "Long Read…     4 gs://… <named list>
#> 5 gs://adult-gtex/haplotype-e… Haplotype … "Haplotype…     5 gs://… <named list>
#> 6 gs://adult-gtex/variants/    Variants    ""              6 gs://… <named list>
#> 7 gs://adult-gtex/references/  Reference   ""              7 gs://… <named list>
#> 8 gs://adult-gtex/annotations/ Metadata    ""              8 gs://… <named list>
#> 9 gs://adult-gtex/additional_… Additional… ""              9 gs://… <named list>
egtex <- get_downloads_page_data("egtex")
egtex
#> # A tibble: 3 × 6
#>   name                    displayName description      order parent children    
#>   <chr>                   <chr>       <chr>            <int> <chr>  <list>      
#> 1 gs://egtex/methylation/ Methylation ""                   1 gs://… <named list>
#> 2 gs://egtex/proteomics/  Proteomics  "Relative prote…     2 gs://… <named list>
#> 3 gs://egtex/telomeres/   Telomeres   "Relative telom…     3 gs://… <named list>

# ..."gtex" does not
get_downloads_page_data("gtex")
#> # A tibble: 0 × 0

# get details for whole blood methylation data, including download URL
purrr::pluck(
  egtex$children,
  1,
  "folders",
  "Methylation - EPIC Array",
  "children",
  "folders",
  "mQTLs",
  "children",
  "files",
  "WholeBlood.mQTLs.regular.txt.gz"
)
#> $displayName
#> [1] "WholeBlood.mQTLs.regular.txt.gz"
#> 
#> $description
#> [1] ""
#> 
#> $fileSize
#> [1] 43461408219
#> 
#> $url
#> [1] "https://storage.googleapis.com/egtex/methylation/epic-arrays/mQTLs/WholeBlood.mQTLs.regular.txt.gz"
#> 
#> $order
#> [1] 27
#> 
#> $parent
#> [1] "gs://egtex/methylation/epic-arrays/mQTLs/"
#> 
```
