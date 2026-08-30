# Introduction to gtexr

The [GTEx Portal API V2](https://gtexportal.org/home/apiPage) enables
programmatic access to data available from the Genotype-Tissue
Expression Portal. The gtexr package wraps this API, providing R
functions that correspond to each [API
endpoint](https://gtexportal.org/api/v2/redoc):

- R function names mirror those of their corresponding endpoint,
  converted to lower case with spaces replaced with underscores[^1]
  e.g. the R function for [“Get Service
  Info”](https://gtexportal.org/api/v2/redoc#tag/GTEx-Portal-API-Info/operation/get_service_info_api_v2__get)
  is
  [`get_service_info()`](https://docs.ropensci.org/gtexr/reference/get_service_info.md).
- Query parameters are similarly mirrored by function arguments e.g. the
  arguments for
  [`get_maintenance_message()`](https://docs.ropensci.org/gtexr/reference/get_maintenance_message.md)
  (corresponding to the endpoint [“Get Maintenance
  Message”](https://gtexportal.org/api/v2/redoc#tag/Admin-Endpoints/operation/get_maintenance_message_api_v2_admin_maintenanceMessage_get))
  are `page` and `itemsPerPage`. For query parameters that accept an
  array of values however, the corresponding function argument is
  pluralised to indicate this e.g. for endpoint [“Get Eqtl
  Genes”](https://gtexportal.org/api/v2/redoc#tag/Static-Association-Endpoints/operation/get_eqtl_genes_api_v2_association_egene_get)
  the query parameter ‘tissueSiteDetailId’ is pluralised to argument
  name `tissueSiteDetailIds` in
  [`get_eqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_eqtl_genes.md).
- Default values for arguments mirror those for the API.
- The documentation for each function includes at least one working
  example
  e.g. [`?get_eqtl_genes`](https://docs.ropensci.org/gtexr/reference/get_eqtl_genes.md)
  provides example valid values for the required argument
  `tissueSiteDetailIds`.
- All functions return a
  [`tibble::tibble`](https://tibble.tidyverse.org/reference/tibble.html)
  by default. Alternatively, the raw JSON from an API call may be
  retrieved by setting argument `.return_raw` to `TRUE`
  e.g. `get_service_info(.return_raw = TRUE)`.

## Shiny app

Users can try out all functions interatively with the ⭐[gtexr shiny
app](https://7hocgq-rmgpanw.shinyapps.io/gtexr/)⭐, which pre-populates
query parameters with those for the first working example from each
function’s documentation. To run the app locally:

``` r

shiny::runApp(system.file("app", package = "gtexr"))
```

## Paginated responses

``` r

library(gtexr)
library(dplyr)
library(purrr)
```

Many API endpoints return only the first 250 available items by default.
A warning is raised if the number of available items exceeds the
selected maximum page size e.g.

``` r

get_eqtl_genes("Whole_Blood")
#> Warning: ! Total number of items (12360) exceeds the selected maximum page size (250).
#> ✖ 12110 items were not retrieved.
#> ℹ To retrieve all available items, increase `itemsPerPage`, ensuring you reuse
#>   your original query parameters e.g.
#>   `get_eqtl_genes(<your_existing_parameters>, itemsPerPage = 100000)`
#> ℹ Alternatively, adjust global "gtexr.itemsPerPage" setting e.g.
#>   `options(list(gtexr.itemsPerPage = 100000))`
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 50
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 12360
#> # A tibble: 250 × 10
#>    tissueSiteDetailId ontologyId  datasetId empiricalPValue gencodeId geneSymbol
#>    <chr>              <chr>       <chr>               <dbl> <chr>     <chr>     
#>  1 Whole_Blood        UBERON:001… gtex_v8          1.05e- 9 ENSG0000… WASH7P    
#>  2 Whole_Blood        UBERON:001… gtex_v8          1.06e-25 ENSG0000… RP11-34P1…
#>  3 Whole_Blood        UBERON:001… gtex_v8          6.31e- 2 ENSG0000… CICP27    
#>  4 Whole_Blood        UBERON:001… gtex_v8          8.71e- 9 ENSG0000… RP11-34P1…
#>  5 Whole_Blood        UBERON:001… gtex_v8          6.01e-20 ENSG0000… RP11-34P1…
#>  6 Whole_Blood        UBERON:001… gtex_v8          6.96e- 9 ENSG0000… RP11-34P1…
#>  7 Whole_Blood        UBERON:001… gtex_v8          3.10e- 4 ENSG0000… RP11-34P1…
#>  8 Whole_Blood        UBERON:001… gtex_v8          1.92e- 3 ENSG0000… ABC7-4304…
#>  9 Whole_Blood        UBERON:001… gtex_v8          1.58e- 3 ENSG0000… RP11-34P1…
#> 10 Whole_Blood        UBERON:001… gtex_v8          7.82e- 2 ENSG0000… AP006222.2
#> # ℹ 240 more rows
#> # ℹ 4 more variables: log2AllelicFoldChange <dbl>, pValue <dbl>,
#> #   pValueThreshold <dbl>, qValue <dbl>
```

For most cases, the simplest solution is to increase the value of
`itemsPerPage`
e.g. `get_eqtl_genes("Whole_Blood", itemsPerPage = 100000)`. This limit
can be set globally by setting the “gtexr.itemsPerPage” option with
`options(list(gtexr.itemsPerPage = 100000))`.

Alternatively, multiple pages can be retrieved sequentially e.g.

``` r

# to retrieve the first 3 pages, with default setting of 250 items per page
1:3 |>
  map(\(page) get_eqtl_genes("Whole_Blood", page = page, .verbose = FALSE) |>
        suppressWarnings()) |>
  bind_rows()
#> # A tibble: 750 × 10
#>    tissueSiteDetailId ontologyId  datasetId empiricalPValue gencodeId geneSymbol
#>    <chr>              <chr>       <chr>               <dbl> <chr>     <chr>     
#>  1 Whole_Blood        UBERON:001… gtex_v8          5.44e- 2 ENSG0000… ARID1A    
#>  2 Whole_Blood        UBERON:001… gtex_v8          2.60e-21 ENSG0000… PIGV      
#>  3 Whole_Blood        UBERON:001… gtex_v8          3.46e-17 ENSG0000… ZDHHC18   
#>  4 Whole_Blood        UBERON:001… gtex_v8          8.02e- 4 ENSG0000… GPN2      
#>  5 Whole_Blood        UBERON:001… gtex_v8          3.48e- 8 ENSG0000… TRNP1     
#>  6 Whole_Blood        UBERON:001… gtex_v8          2.15e- 3 ENSG0000… SLC9A1    
#>  7 Whole_Blood        UBERON:001… gtex_v8          1.09e- 7 ENSG0000… WDTC1     
#>  8 Whole_Blood        UBERON:001… gtex_v8          5.17e- 4 ENSG0000… RP11-4K3_…
#>  9 Whole_Blood        UBERON:001… gtex_v8          5.98e- 4 ENSG0000… TMEM222   
#> 10 Whole_Blood        UBERON:001… gtex_v8          7.62e- 6 ENSG0000… SYTL1     
#> # ℹ 740 more rows
#> # ℹ 4 more variables: log2AllelicFoldChange <dbl>, pValue <dbl>,
#> #   pValueThreshold <dbl>, qValue <dbl>
```

Note that paging information is printed to the R console by default. Set
argument `.verbose` to `FALSE` to silence these messages, or disable
globally with `options(list(gtexr.verbose = FALSE))`.

## Examples

The rest of this vignette outlines some example applications of gtexr.

### Get build 37 coordinates for a variant

``` r

get_variant(snpId = "rs1410858") |>
  tidyr::separate(
    col = b37VariantId,
    into = c(
      "chromosome",
      "position",
      "reference_allele",
      "alternative_allele",
      "genome_build"
    ),
    sep = "_",
    remove = FALSE
  ) |>
  select(snpId:genome_build)
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 1
#> # A tibble: 1 × 7
#>   snpId     b37VariantId chromosome position reference_allele alternative_allele
#>   <chr>     <chr>        <chr>      <chr>    <chr>            <chr>             
#> 1 rs1410858 1_153182116… 1          1531821… C                A                 
#> # ℹ 1 more variable: genome_build <chr>
```

### Convert gene symbol to versioned GENCODE ID

Use `get_gene()` or
[`get_genes()`](https://docs.ropensci.org/gtexr/reference/get_genes.md)

``` r

get_genes("CRP") |>
  select(geneSymbol, gencodeId)
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 1
#> # A tibble: 1 × 2
#>   geneSymbol gencodeId         
#>   <chr>      <chr>             
#> 1 CRP        ENSG00000132693.12
```

### Convert rsID to GTEx variant ID

Use
[`get_variant()`](https://docs.ropensci.org/gtexr/reference/get_variant.md)

``` r

get_variant(snpId = "rs1410858") |>
  select(snpId, variantId)
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 1
#> # A tibble: 1 × 2
#>   snpId     variantId             
#>   <chr>     <chr>                 
#> 1 rs1410858 chr1_153209640_C_A_b38
```

### For a gene of interest, which tissues have significant *cis*-eQTLs?

Use
[`get_significant_single_tissue_eqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_eqtls.md)
(note this requires versioned GENCODE IDs)

``` r

gene_symbol_of_interest <- "CRP"

gene_gencodeId_of_interest <- get_genes(gene_symbol_of_interest) |>
  pull(gencodeId) |>
  suppressMessages()

gene_gencodeId_of_interest |>
  get_significant_single_tissue_eqtls() |>
  distinct(geneSymbol, gencodeId, tissueSiteDetailId)
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 1
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 93
#> # A tibble: 3 × 3
#>   geneSymbol gencodeId          tissueSiteDetailId                 
#>   <chr>      <chr>              <chr>                              
#> 1 CRP        ENSG00000132693.12 Thyroid                            
#> 2 CRP        ENSG00000132693.12 Esophagus_Gastroesophageal_Junction
#> 3 CRP        ENSG00000132693.12 Muscle_Skeletal
```

### Get data for non-eQTL variants

Some analyses (e.g. Mendelian randomisation) require data for variants
which may or may not be significant eQTLs. Use
[`calculate_expression_quantitative_trait_loci()`](https://docs.ropensci.org/gtexr/reference/calculate_expression_quantitative_trait_loci.md)
with [`purrr::map()`](https://purrr.tidyverse.org/reference/map.html) to
retrieve data for multiple variants

``` r

variants_of_interest <- c("rs12119111", "rs6605071", "rs1053870")

variants_of_interest |>
  set_names() |>
  map(
    \(x) calculate_expression_quantitative_trait_loci(
      tissueSiteDetailId = "Liver",
      gencodeId = "ENSG00000237973.1",
      variantId = x
    )
  ) |>
  bind_rows(.id = "rsid") |>
  # optionally, reformat output - first extract genomic coordinates and alleles
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
  mutate(
    alt_allele_count = (2 * homoAltCount) + hetCount,
    total_allele_count = 2 * (homoAltCount + hetCount + homoRefCount),
    alternative_allele_frequency = alt_allele_count / total_allele_count
  ) |>
  select(
    rsid,
    beta = nes,
    se = error,
    pValue,
    minor_allele_frequency = maf,
    alternative_allele_frequency,
    chromosome:genome_build,
    tissueSiteDetailId
  )
#> # A tibble: 3 × 12
#>   rsid         beta     se  pValue minor_allele_frequency alternative_allele_f…¹
#>   <chr>       <dbl>  <dbl>   <dbl>                  <dbl>                  <dbl>
#> 1 rs121191…  0.0270 0.0670 6.88e-1                 0.365                   0.635
#> 2 rs6605071 -0.601  0.166  3.88e-4                 0.0409                  0.959
#> 3 rs1053870  0.0247 0.0738 7.38e-1                 0.214                   0.214
#> # ℹ abbreviated name: ¹​alternative_allele_frequency
#> # ℹ 6 more variables: chromosome <chr>, position <chr>, reference_allele <chr>,
#> #   alternative_allele <chr>, genome_build <chr>, tissueSiteDetailId <chr>
```

[^1]: With the exception of
    [`get_sample_biobank_data()`](https://docs.ropensci.org/gtexr/reference/get_sample_biobank_data.md)
    and
    [`get_sample_datasets()`](https://docs.ropensci.org/gtexr/reference/get_sample_datasets.md),
    for which ‘get_sample’ is additionally appended with their
    respective category titles ‘biobank_data’ and ‘datasets’.
