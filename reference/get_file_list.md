# Get File List

Get all the files in GTEx dataset for Download page

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Datasets-Endpoints/operation/get_file_list_api_v2_dataset_fileList_get)

## Usage

``` r
get_file_list(.return_raw = FALSE)
```

## Arguments

- .return_raw:

  Logical. If `TRUE`, return the raw API JSON response. Default =
  `FALSE`

## Value

A tibble. Or a list if `.return_raw = TRUE`.

## Details

The returned tibble includes a nested list column, "filesets". This
details files, sub-categorised by fileset (see examples section).

## See also

Other Datasets Endpoints:
[`get_annotation()`](https://docs.ropensci.org/gtexr/reference/get_annotation.md),
[`get_collapsed_gene_model_exon()`](https://docs.ropensci.org/gtexr/reference/get_collapsed_gene_model_exon.md),
[`get_downloads_page_data()`](https://docs.ropensci.org/gtexr/reference/get_downloads_page_data.md),
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
# Column "filesets" is a list column
get_file_list()
#> # A tibble: 11 × 10
#>    name            subpath dbgapId dataset release order type  id    description
#>    <chr>           <chr>   <chr>   <chr>   <chr>   <int> <chr> <chr> <chr>      
#>  1 GTEx Analysis … gtex_a… "phs00… GTEx    v3         10 data… gtex… ""         
#>  2 GTEx Analysis … gtex_a… ""      GTEx    v6p         7 data… gtex… "The GTEx …
#>  3 Biobank Invent… gtex_b… ""      GTEx    biobank     5 data… biob… ""         
#>  4 GTEx Analysis … gtex_a… "phs00… GTEx    v7          6 data… gtex… ""         
#>  5 GTEx Analysis … gtex_a… "phs00… GTEx    v6          8 data… gtex… ""         
#>  6 Additional Dat… gtex_a… ""      GTEx    additi…     3 data… addi… ""         
#>  7 GTEx Analysis … gtex_a… "phs00… GTEx    v4          9 data… gtex… ""         
#>  8 External Datas… gtex_e… ""      GTEx    extern…     4 data… exte… ""         
#>  9 GTEx Analysis … gtex_a… "phs00… GTEx    v8          1 data… gtex… "The GTEx …
#> 10 eGTEx           gtex_e… ""      GTEx    egtex       2 data… egtex "The Enhan…
#> 11 GTEx Analysis … gtex_a… "phs00… GTEx    v9          0 data… gtex… "Open-acce…
#> # ℹ 1 more variable: filesets <list>

# Get "GTEx Analysis V9" file list
gtex_v9_files <- get_file_list() |>
  dplyr::filter(name == "GTEx Analysis V9") |>
  dplyr::pull(filesets)

# "GTEx Analysis V9" filesets
names(gtex_v9_files[[1]])
#> [1] "snRNA-Seq Data" "Long Read Data"

# "GTEx Analysis V9", "snRNA-Seq Data" fileset files
names(gtex_v9_files[[1]][["snRNA-Seq Data"]]$files)
#> [1] "GTEx_8_tissues_snRNAseq_atlas_071421.public_obs.h5ad"       
#> [2] "GTEx_8_tissues_snRNAseq_immune_atlas_071421.public_obs.h5ad"
```
