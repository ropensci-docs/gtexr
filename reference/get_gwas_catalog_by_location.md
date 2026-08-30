# Get Gwas Catalog By Location

Find the GWAS Catalog on a certain chromosome between start and end
locations.

[GTEx API Portal
documentation](https://gtexportal.org/api/v2/redoc#tag/Reference-Genome-Endpoints/operation/get_gwas_catalog_by_location_api_v2_reference_gwasCatalogByLocation_get)

## Usage

``` r
get_gwas_catalog_by_location(
  start,
  end,
  chromosome,
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

- start:

  Integer.

- end:

  Integer.

- chromosome:

  String. One of "chr1", "chr2", "chr3", "chr4", "chr5", "chr6", "chr7",
  "chr8", "chr9", "chr10", "chr11", "chr12", "chr13", "chr14", "chr15",
  "chr16", "chr17", "chr18", "chr19", "chr20", "chr21", "chr22", "chrM",
  "chrX", "chrY".

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

Other Reference Genome Endpoints:
[`get_exons()`](https://docs.ropensci.org/gtexr/reference/get_exons.md),
[`get_gene_search()`](https://docs.ropensci.org/gtexr/reference/get_gene_search.md),
[`get_genes()`](https://docs.ropensci.org/gtexr/reference/get_genes.md),
[`get_genomic_features()`](https://docs.ropensci.org/gtexr/reference/get_genomic_features.md),
[`get_neighbor_gene()`](https://docs.ropensci.org/gtexr/reference/get_neighbor_gene.md),
[`get_transcripts()`](https://docs.ropensci.org/gtexr/reference/get_transcripts.md)

## Examples

``` r
get_gwas_catalog_by_location(start = 1, end = 10000000, chromosome = "chr1")
#> Warning: ! Total number of items (316) exceeds the selected maximum page size (250).
#> ✖ 66 items were not retrieved.
#> ℹ To retrieve all available items, increase `itemsPerPage`, ensuring you reuse
#>   your original query parameters e.g.
#>   `get_gwas_catalog_by_location(<your_existing_parameters>, itemsPerPage =
#>   100000)`
#> ℹ Alternatively, adjust global "gtexr.itemsPerPage" setting e.g.
#>   `options(list(gtexr.itemsPerPage = 100000))`
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 2
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 316
#> # A tibble: 250 × 10
#>    chromosome   start     end phenotype  pValue   beta pubmedId snpId riskAllele
#>    <chr>        <int>   <int> <chr>       <dbl>  <dbl>    <int> <chr> <chr>     
#>  1 chr1       9653328 9653329 Testicula…  6e-13 1.14   28604728 rs42… T         
#>  2 chr1       8428505 8428506 Autism sp…  7e- 9 1.06   28540026 rs30… ?         
#>  3 chr1       9651584 9651585 Monocyte …  2e- 9 0.0222 27863252 rs75… G         
#>  4 chr1       3080038 3080039 Mean corp…  1e-13 0.0311 27863252 rs15… C         
#>  5 chr1       3811497 3811498 Mean corp…  1e-13 0.0301 27863252 rs12… T         
#>  6 chr1       4544044 4544045 Adolescen…  3e- 9 1.2    26394188 rs24… ?         
#>  7 chr1       1312114 1312115 Inflammat…  8e-13 1.10   23128233 rs12… A         
#>  8 chr1       7961913 7961914 Inflammat…  1e-15 1.11   23128233 rs35… G         
#>  9 chr1       8444361 8444362 Eosinophi…  2e-19 0.0328 27863252 rs15… A         
#> 10 chr1       9281727 9281728 Eosinophi…  1e-10 0.0260 27863252 rs67… T         
#> # ℹ 240 more rows
#> # ℹ 1 more variable: genomeBuild <chr>
```
