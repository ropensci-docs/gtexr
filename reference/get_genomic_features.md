# Get Genomic Features

[GTEx API Portal
documentation](https://gtexportal.org/api/v2/redoc#tag/Reference-Genome-Endpoints/operation/get_genomic_features_api_v2_reference_features__featureId__get)

## Usage

``` r
get_genomic_features(.featureId, datasetId = "gtex_v8", .return_raw = FALSE)
```

## Arguments

- .featureId:

  String. A genomic feature e.g. GENCODE ID, RSID or GTEx Variant ID.

- datasetId:

  String. Unique identifier of a dataset. Usually includes a data source
  and data release. Options: "gtex_v8", "gtex_snrnaseq_pilot".

- .return_raw:

  Logical. If `TRUE`, return the raw API JSON response. Default =
  `FALSE`

## Value

A tibble. Or a list if `.return_raw = TRUE`.

## Details

This endpoint takes a path parameter "featureId".

## See also

Other Reference Genome Endpoints:
[`get_exons()`](https://docs.ropensci.org/gtexr/reference/get_exons.md),
[`get_gene_search()`](https://docs.ropensci.org/gtexr/reference/get_gene_search.md),
[`get_genes()`](https://docs.ropensci.org/gtexr/reference/get_genes.md),
[`get_gwas_catalog_by_location()`](https://docs.ropensci.org/gtexr/reference/get_gwas_catalog_by_location.md),
[`get_neighbor_gene()`](https://docs.ropensci.org/gtexr/reference/get_neighbor_gene.md),
[`get_transcripts()`](https://docs.ropensci.org/gtexr/reference/get_transcripts.md)

## Examples

``` r
# gene symbol
get_genomic_features("brca1")
#> # A tibble: 1 × 17
#>   gencodeVersion      end description     geneSymbolUpper genomeBuild geneStatus
#>   <chr>             <int> <chr>           <chr>           <chr>       <chr>     
#> 1 v26            43170245 BRCA1, DNA rep… BRCA1           GRCh38/hg38 ""        
#> # ℹ 11 more variables: strand <chr>, entrezGeneId <int>, geneType <chr>,
#> #   start <int>, dataSource <chr>, gencodeId <chr>, geneSymbol <chr>,
#> #   tss <int>, chromosome <chr>, featureType <chr>, assembly <chr>

# GENCODE ID
get_genomic_features("ENSG00000132693.12")
#> # A tibble: 1 × 17
#>   gencodeVersion       end description    geneSymbolUpper genomeBuild geneStatus
#>   <chr>              <int> <chr>          <chr>           <chr>       <chr>     
#> 1 v26            159714589 C-reactive pr… CRP             GRCh38/hg38 ""        
#> # ℹ 11 more variables: strand <chr>, entrezGeneId <int>, geneType <chr>,
#> #   start <int>, dataSource <chr>, gencodeId <chr>, geneSymbol <chr>,
#> #   tss <int>, chromosome <chr>, featureType <chr>, assembly <chr>

# RSID
get_genomic_features("rs1815739")
#> # A tibble: 1 × 8
#>   featureType chromosome    start snpId     variantId       ref   alt   assembly
#>   <chr>       <chr>         <int> <chr>     <chr>           <chr> <chr> <chr>   
#> 1 snp         chr11      66560624 rs1815739 chr11_66560624… C     T     HG38    

# GTEx variant ID
get_genomic_features("chr11_66561023_G_GTTA_b38")
#> # A tibble: 1 × 8
#>   featureType chromosome    start snpId     variantId       ref   alt   assembly
#>   <chr>       <chr>         <int> <chr>     <chr>           <chr> <chr> <chr>   
#> 1 snp         chr11      66561023 rs3837428 chr11_66561023… G     GTTA  HG38    
```
