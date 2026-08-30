# Get Significant Single Tissue Sqtls

Retrieve Single Tissue sQTL Data.

- This service returns single tissue sQTL data for the given genes, from
  a specified dataset.

- Results may be filtered by tissue

- By default, the service queries the latest GTEx release.

The retrieved data is split into pages with `items_per_page` entries per
page

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Static-Association-Endpoints/operation/get_significant_single_tissue_sqtls_api_v2_association_singleTissueSqtl_get).

## Usage

``` r
get_significant_single_tissue_sqtls(
  gencodeIds = NULL,
  variantIds = NULL,
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

- variantIds:

  Character vector. Gtex variant IDs.

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
[`get_independent_eqtl()`](https://docs.ropensci.org/gtexr/reference/get_independent_eqtl.md),
[`get_multi_tissue_eqtls()`](https://docs.ropensci.org/gtexr/reference/get_multi_tissue_eqtls.md),
[`get_significant_single_tissue_eqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_eqtls.md),
[`get_significant_single_tissue_eqtls_by_location()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_eqtls_by_location.md),
[`get_significant_single_tissue_ieqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_ieqtls.md),
[`get_significant_single_tissue_isqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_isqtls.md),
[`get_sqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_sqtl_genes.md)

## Examples

``` r
# search by gene
get_significant_single_tissue_sqtls(gencodeIds = c(
  "ENSG00000065613.9",
  "ENSG00000203782.5"
))
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 176
#> # A tibble: 176 × 14
#>    snpId            pos snpIdUpper variantId  geneSymbol  pValue geneSymbolUpper
#>    <chr>          <int> <chr>      <chr>      <chr>        <dbl> <chr>          
#>  1 rs4636462  152442732 RS4636462  chr1_1524… LOR        7.71e-5 LOR            
#>  2 rs4845768  152442997 RS4845768  chr1_1524… LOR        6.57e-5 LOR            
#>  3 rs12069640 152444300 RS12069640 chr1_1524… LOR        7.13e-5 LOR            
#>  4 rs11803629 152445670 RS11803629 chr1_1524… LOR        1.81e-4 LOR            
#>  5 rs12125681 152445737 RS12125681 chr1_1524… LOR        1.81e-4 LOR            
#>  6 rs11205004 152446586 RS11205004 chr1_1524… LOR        1.81e-4 LOR            
#>  7 rs11579085 152447965 RS11579085 chr1_1524… LOR        1.81e-4 LOR            
#>  8 rs1885529  152448570 RS1885529  chr1_1524… LOR        1.81e-4 LOR            
#>  9 rs1885528  152448978 RS1885528  chr1_1524… LOR        1.81e-4 LOR            
#> 10 rs1885527  152449069 RS1885527  chr1_1524… LOR        1.81e-4 LOR            
#> # ℹ 166 more rows
#> # ℹ 7 more variables: datasetId <chr>, tissueSiteDetailId <chr>,
#> #   ontologyId <chr>, chromosome <chr>, gencodeId <chr>, nes <dbl>,
#> #   phenotypeId <chr>
```
