# Calculate Splicing Quantitative Trait Loci

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Dynamic-Association-Endpoints/operation/calculate_splicing_quantitative_trait_loci_api_v2_association_dynsqtl_get).

## Usage

``` r
calculate_splicing_quantitative_trait_loci(
  tissueSiteDetailId,
  phenotypeId,
  variantId,
  datasetId = "gtex_v8",
  .return_raw = FALSE
)
```

## Arguments

- tissueSiteDetailId:

  String. The ID of the tissue of interest. Can be a GTEx specific ID
  (e.g. "Whole_Blood"; use
  [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  to see valid values) or an Ontology ID.

- phenotypeId:

  String. See [GTEx portal
  FAQs](https://www.gtexportal.org/home/faq#splicingPhenotypeId) for
  further details.

- variantId:

  String. A gtex variant ID.

- datasetId:

  String. Unique identifier of a dataset. Usually includes a data source
  and data release. Options: "gtex_v8", "gtex_snrnaseq_pilot".

- .return_raw:

  Logical. If `TRUE`, return the raw API JSON response. Default =
  `FALSE`

## Value

A tibble. Or a list if `.return_raw = TRUE`.

## See also

Other Dynamic Association Endpoints:
[`calculate_expression_quantitative_trait_loci()`](https://docs.ropensci.org/gtexr/reference/calculate_expression_quantitative_trait_loci.md),
[`calculate_ieqtls()`](https://docs.ropensci.org/gtexr/reference/calculate_ieqtls.md),
[`calculate_isqtls()`](https://docs.ropensci.org/gtexr/reference/calculate_isqtls.md)

## Examples

``` r
# perform request - returns a tibble with a single row
calculate_splicing_quantitative_trait_loci(
  tissueSiteDetailId = "Whole_Blood",
  phenotypeId = "chr1:15947:16607:clu_40980:ENSG00000227232.5",
  variantId = "chr1_14677_G_A_b38"
)
#> # A tibble: 1 × 14
#>   data     error genotypes hetCount homoAltCount homoRefCount    maf   nes
#>   <list>   <dbl> <list>       <int>        <int>        <int>  <dbl> <dbl>
#> 1 <tibble> 0.139 <tibble>        69            0          601 0.0515 0.757
#> # ℹ 6 more variables: pValue <dbl>, pValueThreshold <dbl>, phenotypeId <chr>,
#> #   tStatistic <dbl>, tissueSiteDetailId <chr>, variantId <chr>
```
