# Calculate Expression Quantitative Trait Loci

Calculate your own eQTLs

- This service calculates the gene-variant association for any given
  pair of gene and variant, which may or may not be significant.

- This requires as input a GENCODE ID, GTEx variant ID, and tissue site
  detail ID.

By default, the calculation is based on the latest GTEx release.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Dynamic-Association-Endpoints/operation/calculate_expression_quantitative_trait_loci_api_v2_association_dyneqtl_get).

## Usage

``` r
calculate_expression_quantitative_trait_loci(
  tissueSiteDetailId,
  gencodeId,
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

- gencodeId:

  String. A Versioned GENCODE ID of a gene, e.g. "ENSG00000065613.9".

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

## Details

Notes on output:

- Beta and standard error are recorded in columns `nes` and `error`
  respectively (see [GTEx
  FAQs](https://gtexportal.org/home/faq#nes_beta))

- `variantId` contains (in order) chromosome, position, reference
  allele, alternative allele and human genome build separated by
  underscores. The reference and alternative alleles for
  "chr1_13550_G_A_b38" for example are "G" and "A" respectively.

- See examples for how to calculate minor and alternative allele
  frequencies.

Notes on input:

- Argument `variantId` also accepts RSIDs.

## See also

Other Dynamic Association Endpoints:
[`calculate_ieqtls()`](https://docs.ropensci.org/gtexr/reference/calculate_ieqtls.md),
[`calculate_isqtls()`](https://docs.ropensci.org/gtexr/reference/calculate_isqtls.md),
[`calculate_splicing_quantitative_trait_loci()`](https://docs.ropensci.org/gtexr/reference/calculate_splicing_quantitative_trait_loci.md)

## Examples

``` r
# perform request - returns a tibble with a single row
calculate_expression_quantitative_trait_loci(
  tissueSiteDetailId = "Whole_Blood",
  gencodeId = "ENSG00000203782.5",
  variantId = "rs79641866"
)
#> # A tibble: 1 × 15
#>   data               error gencodeId  geneSymbol genotypes hetCount homoAltCount
#>   <list>             <dbl> <chr>      <chr>      <list>       <int>        <int>
#> 1 <tibble [670 × 1]> 0.148 ENSG00000… LOR        <tibble>        38            0
#> # ℹ 8 more variables: homoRefCount <int>, maf <dbl>, nes <dbl>, pValue <dbl>,
#> #   pValueThreshold <dbl>, tStatistic <dbl>, tissueSiteDetailId <chr>,
#> #   variantId <chr>

# unnest list columns with tidyr::unnest()
calculate_expression_quantitative_trait_loci(
  tissueSiteDetailId = "Whole_Blood",
  gencodeId = "ENSG00000203782.5",
  variantId = "rs79641866"
) |>
  tidyr::unnest(c("data", "genotypes"))
#> # A tibble: 670 × 15
#>      data error gencodeId         geneSymbol genotypes hetCount homoAltCount
#>     <dbl> <dbl> <chr>             <chr>          <int>    <int>        <int>
#>  1 -0.837 0.148 ENSG00000203782.5 LOR                0       38            0
#>  2  0.864 0.148 ENSG00000203782.5 LOR                0       38            0
#>  3 -0.697 0.148 ENSG00000203782.5 LOR                0       38            0
#>  4 -0.471 0.148 ENSG00000203782.5 LOR                0       38            0
#>  5  1.51  0.148 ENSG00000203782.5 LOR                0       38            0
#>  6 -1.88  0.148 ENSG00000203782.5 LOR                0       38            0
#>  7  1.86  0.148 ENSG00000203782.5 LOR                0       38            0
#>  8 -0.641 0.148 ENSG00000203782.5 LOR                0       38            0
#>  9  2.61  0.148 ENSG00000203782.5 LOR                0       38            0
#> 10 -1.19  0.148 ENSG00000203782.5 LOR                0       38            0
#> # ℹ 660 more rows
#> # ℹ 8 more variables: homoRefCount <int>, maf <dbl>, nes <dbl>, pValue <dbl>,
#> #   pValueThreshold <dbl>, tStatistic <dbl>, tissueSiteDetailId <chr>,
#> #   variantId <chr>

# to calculate minor and alternative allele frequencies
calculate_expression_quantitative_trait_loci(
  tissueSiteDetailId = "Liver",
  gencodeId = "ENSG00000237973.1",
  variantId = "rs12119111"
) |>
  dplyr::bind_rows(.id = "rsid") |>
  tidyr::separate(
    col = "variantId",
    into = c(
      "chromosome",
      "position",
      "reference_allele",
      "alternative_allele",
      "genome_build"
    ),
    sep = "_"
  ) |>
  # ...then ascertain alternative_allele frequency
  dplyr::mutate(
    alt_allele_count = (2 * homoAltCount) + hetCount,
    total_allele_count = 2 * (homoAltCount + hetCount + homoRefCount),
    alternative_allele_frequency = alt_allele_count / total_allele_count
  ) |>
  dplyr::select(
    rsid,
    beta = nes,
    se = error,
    pValue,
    minor_allele_frequency = maf,
    alternative_allele_frequency,
    chromosome:genome_build,
    tissueSiteDetailId
  )
#> # A tibble: 1 × 12
#>   rsid    beta     se pValue minor_allele_frequency alternative_allele_frequency
#>   <chr>  <dbl>  <dbl>  <dbl>                  <dbl>                        <dbl>
#> 1 1     0.0270 0.0670  0.688                  0.365                        0.635
#> # ℹ 6 more variables: chromosome <chr>, position <chr>, reference_allele <chr>,
#> #   alternative_allele <chr>, genome_build <chr>, tissueSiteDetailId <chr>
```
