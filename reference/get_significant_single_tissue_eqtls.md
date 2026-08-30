# Get Significant Single Tissue Eqtls

Find significant single tissue eQTLs.

- This service returns precomputed significant single tissue eQTLs.

- Results may be filtered by tissue, gene, variant or dataset.

- To search by gene, use the versioned GENCODE ID.

- To search by variant, use the dbSNP rs ID (snpId).

By default, the service queries the latest GTEx release and the
retrieved data is split into pages with `items_per_page` entries per
page

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Static-Association-Endpoints/operation/get_significant_single_tissue_eqtls_api_v2_association_singleTissueEqtl_get).

## Usage

``` r
get_significant_single_tissue_eqtls(
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

## Details

**Note:** although the GTEx Portal API documentation says to use the
dbSNP rsID when searching by variant, this returns no results. Instead
use gtex variant IDs e.g. use "chr1_153209640_C_A_b38" instead of
"rs1410858".

## See also

Other Static Association Endpoints:
[`get_eqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_eqtl_genes.md),
[`get_fine_mapping()`](https://docs.ropensci.org/gtexr/reference/get_fine_mapping.md),
[`get_independent_eqtl()`](https://docs.ropensci.org/gtexr/reference/get_independent_eqtl.md),
[`get_multi_tissue_eqtls()`](https://docs.ropensci.org/gtexr/reference/get_multi_tissue_eqtls.md),
[`get_significant_single_tissue_eqtls_by_location()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_eqtls_by_location.md),
[`get_significant_single_tissue_ieqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_ieqtls.md),
[`get_significant_single_tissue_isqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_isqtls.md),
[`get_significant_single_tissue_sqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_sqtls.md),
[`get_sqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_sqtl_genes.md)

## Examples

``` r
# search by gene
get_significant_single_tissue_eqtls(gencodeIds = c(
  "ENSG00000132693.12",
  "ENSG00000203782.5"
))
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 249
#> # A tibble: 249 × 13
#>    snpId            pos snpIdUpper variantId  geneSymbol  pValue geneSymbolUpper
#>    <chr>          <int> <chr>      <chr>      <chr>        <dbl> <chr>          
#>  1 rs12128960 159343657 RS12128960 chr1_1593… CRP        8.52e-5 CRP            
#>  2 rs12132451 159344052 RS12132451 chr1_1593… CRP        7.92e-5 CRP            
#>  3 rs12136402 159347493 RS12136402 chr1_1593… CRP        7.92e-5 CRP            
#>  4 rs10908709 159350390 RS10908709 chr1_1593… CRP        7.92e-5 CRP            
#>  5 rs10908710 159351189 RS10908710 chr1_1593… CRP        7.92e-5 CRP            
#>  6 rs11265178 159359256 RS11265178 chr1_1593… CRP        9.62e-5 CRP            
#>  7 rs35532309 159360755 RS35532309 chr1_1593… CRP        6.11e-5 CRP            
#>  8 rs6692378  159369451 RS6692378  chr1_1593… CRP        1.17e-6 CRP            
#>  9 rs10908714 159370563 RS10908714 chr1_1593… CRP        1.80e-5 CRP            
#> 10 rs6656924  159372915 RS6656924  chr1_1593… CRP        1.00e-6 CRP            
#> # ℹ 239 more rows
#> # ℹ 6 more variables: datasetId <chr>, tissueSiteDetailId <chr>,
#> #   ontologyId <chr>, chromosome <chr>, gencodeId <chr>, nes <dbl>

# search by variant - must be variantId (not rsid)
get_significant_single_tissue_eqtls(variantIds = "chr1_153209640_C_A_b38")
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 2
#> # A tibble: 2 × 13
#>   snpId           pos snpIdUpper variantId   geneSymbol   pValue geneSymbolUpper
#>   <chr>         <int> <chr>      <chr>       <chr>         <dbl> <chr>          
#> 1 rs1410858 153209640 RS1410858  chr1_15320… LOR        5.47e- 5 LOR            
#> 2 rs1410858 153209640 RS1410858  chr1_15320… PRR9       5.35e-19 PRR9           
#> # ℹ 6 more variables: datasetId <chr>, tissueSiteDetailId <chr>,
#> #   ontologyId <chr>, chromosome <chr>, gencodeId <chr>, nes <dbl>

# filter by gene/variant and tissue site - either `gencodeIds` or `variantIds`
# should be supplied as a minimum
get_significant_single_tissue_eqtls(
  gencodeIds = c(
    "ENSG00000132693.12",
    "ENSG00000203782.5"
  ),
  variantIds = "chr1_153209640_C_A_b38",
  tissueSiteDetailIds = "Whole_Blood"
)
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 1
#> # A tibble: 1 × 13
#>   snpId    pos snpIdUpper variantId geneSymbol  pValue geneSymbolUpper datasetId
#>   <chr>  <int> <chr>      <chr>     <chr>        <dbl> <chr>           <chr>    
#> 1 rs14… 1.53e8 RS1410858  chr1_153… LOR        5.47e-5 LOR             gtex_v8  
#> # ℹ 5 more variables: tissueSiteDetailId <chr>, ontologyId <chr>,
#> #   chromosome <chr>, gencodeId <chr>, nes <dbl>
```
