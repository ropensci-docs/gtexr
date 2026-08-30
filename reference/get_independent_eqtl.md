# Get Independent Eqtl

Retrieve Independent eQTL Data

- Finds and returns `Independent eQTL Data` data for the provided list
  of genes

- By default, this endpoint fetches data from the latest `GTEx` version

The retrieved data is split into pages with `items_per_page` entries per
page

[GTEx portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Static-Association-Endpoints/operation/get_independent_eqtl_api_v2_association_independentEqtl_get)

## Usage

``` r
get_independent_eqtl(
  gencodeIds,
  tissueSiteDetailIds = NULL,
  datasetId = "gtex_v8",
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

- gencodeIds:

  A character vector of Versioned GENCODE IDs, e.g.
  c("ENSG00000132693.12", "ENSG00000203782.5").

- tissueSiteDetailIds:

  Character vector of IDs for tissues of interest. Can be GTEx specific
  IDs (e.g. "Whole_Blood"; use
  [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  to see valid values) or Ontology IDs.

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

Other Static Association Endpoints:
[`get_eqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_eqtl_genes.md),
[`get_fine_mapping()`](https://docs.ropensci.org/gtexr/reference/get_fine_mapping.md),
[`get_multi_tissue_eqtls()`](https://docs.ropensci.org/gtexr/reference/get_multi_tissue_eqtls.md),
[`get_significant_single_tissue_eqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_eqtls.md),
[`get_significant_single_tissue_eqtls_by_location()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_eqtls_by_location.md),
[`get_significant_single_tissue_ieqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_ieqtls.md),
[`get_significant_single_tissue_isqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_isqtls.md),
[`get_significant_single_tissue_sqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_sqtls.md),
[`get_sqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_sqtl_genes.md)

## Examples

``` r
# search by gene
get_independent_eqtl(gencodeIds = c(
  "ENSG00000132693.12",
  "ENSG00000203782.5"
))
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 8
#> # A tibble: 8 × 14
#>   gencodeId       geneSymbol variantId snpId tissueSiteDetailId ontologyId  rank
#>   <chr>           <chr>      <chr>     <chr> <chr>              <chr>      <int>
#> 1 ENSG0000013269… CRP        chr1_160… rs66… Esophagus_Gastroe… UBERON:00…     1
#> 2 ENSG0000013269… CRP        chr1_159… rs57… Thyroid            UBERON:00…     1
#> 3 ENSG0000020378… LOR        chr1_153… rs14… Artery_Coronary    UBERON:00…     1
#> 4 ENSG0000020378… LOR        chr1_153… rs87… Whole_Blood        UBERON:00…     1
#> 5 ENSG0000020378… LOR        chr1_153… rs12… Skin_Sun_Exposed_… UBERON:00…     1
#> 6 ENSG0000020378… LOR        chr1_152… rs77… Heart_Atrial_Appe… UBERON:00…     1
#> 7 ENSG0000020378… LOR        chr1_153… rs12… Esophagus_Mucosa   UBERON:00…     1
#> 8 ENSG0000013269… CRP        chr1_159… rs86… Muscle_Skeletal    UBERON:00…     1
#> # ℹ 7 more variables: tssDistance <int>, maf <dbl>, pValue <dbl>, nes <dbl>,
#> #   chromosome <chr>, pos <int>, datasetId <chr>

# optionally filter for a single variant and/or one or more tissues
get_independent_eqtl(
  gencodeIds = c(
    "ENSG00000132693.12",
    "ENSG00000203782.5"
  ),
  tissueSiteDetailIds = c(
    "Whole_Blood",
    "Thyroid"
  )
)
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 2
#> # A tibble: 2 × 14
#>   gencodeId       geneSymbol variantId snpId tissueSiteDetailId ontologyId  rank
#>   <chr>           <chr>      <chr>     <chr> <chr>              <chr>      <int>
#> 1 ENSG0000013269… CRP        chr1_159… rs57… Thyroid            UBERON:00…     1
#> 2 ENSG0000020378… LOR        chr1_153… rs87… Whole_Blood        UBERON:00…     1
#> # ℹ 7 more variables: tssDistance <int>, maf <dbl>, pValue <dbl>, nes <dbl>,
#> #   chromosome <chr>, pos <int>, datasetId <chr>
```
