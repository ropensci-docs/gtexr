# Get Variant

This service returns information about a variant, including position,
dbSNP RS ID, the reference allele, the alternative allele, and whether
the minor allele frequency is \>= 1%. For GTEx v6p, there is also
information about whether the whole exome sequence and chip sequencing
data are available. Results may be queried by GTEx variant ID
(variantId), dbSNP RS ID (snpId) or genomic location (chromosome and
pos). Variants are identified based on the genotype data of each dataset
cohort, namely, are dataset-dependent. Each variant is assigned a unique
GTEx variant ID (i.e. the primary key). Not all variants have a mappable
dbSNP RS ID. By default, this service queries the latest GTEx release.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Datasets-Endpoints/operation/get_variant_api_v2_dataset_variant_get)

## Usage

``` r
get_variant(
  snpId = NULL,
  variantId = NULL,
  datasetId = "gtex_v8",
  chromosome = NULL,
  poss = NULL,
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

- snpId:

  String

- variantId:

  String. A gtex variant ID.

- datasetId:

  String. Unique identifier of a dataset. Usually includes a data source
  and data release. Options: "gtex_v8", "gtex_snrnaseq_pilot".

- chromosome:

  String. One of "chr1", "chr2", "chr3", "chr4", "chr5", "chr6", "chr7",
  "chr8", "chr9", "chr10", "chr11", "chr12", "chr13", "chr14", "chr15",
  "chr16", "chr17", "chr18", "chr19", "chr20", "chr21", "chr22", "chrM",
  "chrX", "chrY".

- poss:

  Integer, vector.

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
[`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md),
[`get_variant_by_location()`](https://docs.ropensci.org/gtexr/reference/get_variant_by_location.md)

## Examples

``` r
# search by rsid
get_variant(snpId = "rs1410858")
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 1
#> # A tibble: 1 × 10
#>   snpId     b37VariantId         pos maf01 variantId alt   chromosome snpIdUpper
#>   <chr>     <chr>              <int> <lgl> <chr>     <chr> <chr>      <chr>     
#> 1 rs1410858 1_153182116_C_A_… 1.53e8 TRUE  chr1_153… A     chr1       RS1410858 
#> # ℹ 2 more variables: datasetId <chr>, ref <chr>

# search by variantId
get_variant(variantId = "chr1_153209640_C_A_b38")
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 1
#> # A tibble: 1 × 10
#>   snpId     b37VariantId         pos maf01 variantId alt   chromosome snpIdUpper
#>   <chr>     <chr>              <int> <lgl> <chr>     <chr> <chr>      <chr>     
#> 1 rs1410858 1_153182116_C_A_… 1.53e8 TRUE  chr1_153… A     chr1       RS1410858 
#> # ℹ 2 more variables: datasetId <chr>, ref <chr>

# search by chromosome and position
get_variant(
  chromosome = "chr1",
  pos = 153209600:153209700
)
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 4
#> # A tibble: 4 × 10
#>   snpId       b37VariantId       pos maf01 variantId alt   chromosome snpIdUpper
#>   <chr>       <chr>            <int> <lgl> <chr>     <chr> <chr>      <chr>     
#> 1 rs11205220  1_153182115_T_… 1.53e8 TRUE  chr1_153… C     chr1       RS11205220
#> 2 rs1410858   1_153182116_C_… 1.53e8 TRUE  chr1_153… A     chr1       RS1410858 
#> 3 rs139296761 1_153182120_C_… 1.53e8 FALSE chr1_153… T     chr1       RS1392967…
#> 4 rs80104092  1_153182149_T_… 1.53e8 FALSE chr1_153… C     chr1       RS80104092
#> # ℹ 2 more variables: datasetId <chr>, ref <chr>
```
