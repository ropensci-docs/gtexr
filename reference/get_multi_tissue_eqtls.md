# Get Multi Tissue Eqtls

Find multi-tissue eQTL `Metasoft` results.

- This service returns multi-tissue eQTL Metasoft results for a given
  gene and variant in a specified dataset.

- A Versioned GENCODE ID must be provided.

- For each tissue, the results include: m-value (mValue), normalized
  effect size (nes), p-value (pValue), and standard error (se).

- The m-value is the posterior probability that an eQTL effect exists in
  each tissue tested in the cross-tissue meta-analysis (Han and Eskin,
  PLoS Genetics 8(3): e1002555, 2012).

- The normalized effect size is the slope of the linear regression of
  normalized expression data versus the three genotype categories using
  single-tissue eQTL analysis, representing eQTL effect size.

- The p-value is from a t-test that compares observed NES from
  single-tissue eQTL analysis to a null NES of 0.

By default, the service queries the latest GTEx release. The retrieved
data is split into pages with `items_per_page` entries per page

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Static-Association-Endpoints/operation/get_multi_tissue_eqtls_api_v2_association_metasoft_get)

## Usage

``` r
get_multi_tissue_eqtls(
  gencodeId,
  variantId = NULL,
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

- variantId:

  String. A gtex variant ID.

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
[`get_significant_single_tissue_eqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_eqtls.md),
[`get_significant_single_tissue_eqtls_by_location()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_eqtls_by_location.md),
[`get_significant_single_tissue_ieqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_ieqtls.md),
[`get_significant_single_tissue_isqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_isqtls.md),
[`get_significant_single_tissue_sqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_sqtls.md),
[`get_sqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_sqtl_genes.md)

## Examples

``` r
# search by gene
get_multi_tissue_eqtls(gencodeId = "ENSG00000132693.12")
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 93
#> # A tibble: 93 × 5
#>    gencodeId          datasetId    metaP variantId               tissues 
#>    <chr>              <chr>        <dbl> <chr>                   <list>  
#>  1 ENSG00000132693.12 gtex_v8   0.00142  chr1_159476920_T_C_b38  <tibble>
#>  2 ENSG00000132693.12 gtex_v8   0.0927   chr1_159245536_C_T_b38  <tibble>
#>  3 ENSG00000132693.12 gtex_v8   0.00158  chr1_159439013_C_T_b38  <tibble>
#>  4 ENSG00000132693.12 gtex_v8   0.000735 chr1_159441913_T_A_b38  <tibble>
#>  5 ENSG00000132693.12 gtex_v8   0.00158  chr1_159471651_G_A_b38  <tibble>
#>  6 ENSG00000132693.12 gtex_v8   0.00158  chr1_159396484_C_T_b38  <tibble>
#>  7 ENSG00000132693.12 gtex_v8   0.00158  chr1_159386699_AT_A_b38 <tibble>
#>  8 ENSG00000132693.12 gtex_v8   0.00263  chr1_159545608_A_T_b38  <tibble>
#>  9 ENSG00000132693.12 gtex_v8   0.00142  chr1_159476580_G_A_b38  <tibble>
#> 10 ENSG00000132693.12 gtex_v8   0.00166  chr1_159505857_T_A_b38  <tibble>
#> # ℹ 83 more rows

# note that 'tissues' is a list-column
x <- get_multi_tissue_eqtls(gencodeId = "ENSG00000132693.12",
                            variantId = "chr1_159476920_T_C_b38")
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 1

x$tissues[[1]]
#> # A tibble: 49 × 5
#>    tissue                          mValue    pValue     se     nes
#>    <chr>                            <dbl>     <dbl>  <dbl>   <dbl>
#>  1 Thyroid                          0.983 0.0000292 0.0593  0.250 
#>  2 Testis                           0.342 0.0404    0.0835 -0.172 
#>  3 Small_Intestine_Terminal_Ileum   0.551 0.864     0.122  -0.0211
#>  4 Brain_Frontal_Cortex_BA9         0.489 0.204     0.113  -0.144 
#>  5 Skin_Not_Sun_Exposed_Suprapubic  0.552 0.806     0.0654  0.0160
#>  6 Vagina                           0.514 0.437     0.130  -0.102 
#>  7 Whole_Blood                      0.494 0.632     0.0407  0.0195
#>  8 Breast_Mammary_Tissue            0.679 0.395     0.0746  0.0636
#>  9 Pituitary                        0.421 0.175     0.0972 -0.132 
#> 10 Minor_Salivary_Gland             0.678 0.349     0.126   0.118 
#> # ℹ 39 more rows
```
