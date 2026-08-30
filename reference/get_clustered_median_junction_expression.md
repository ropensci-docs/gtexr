# Get Clustered Median Junction Expression

Find median junction expression data along with hierarchical clusters.

- Returns median junction read counts in tissues of a given gene from
  all known transcripts along with the hierarchical clustering results
  of tissues and genes, based on junction expression, in Newick format.

- Results may be filtered by dataset, gene or tissue, but at least one
  gene must be provided.

- The hierarchical clustering is performed by calculating Euclidean
  distances and using the average linkage method.

- **This endpoint is not paginated.**

By default, this service queries the latest GTEx release.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Expression-Data-Endpoints/operation/get_clustered_median_junction_expression_api_v2_expression_clusteredMedianJunctionExpression_get)

## Usage

``` r
get_clustered_median_junction_expression(
  gencodeIds,
  datasetId = "gtex_v8",
  tissueSiteDetailIds = NULL,
  .return_raw = FALSE
)
```

## Arguments

- gencodeIds:

  A character vector of Versioned GENCODE IDs, e.g.
  c("ENSG00000132693.12", "ENSG00000203782.5").

- datasetId:

  String. Unique identifier of a dataset. Usually includes a data source
  and data release. Options: "gtex_v8", "gtex_snrnaseq_pilot".

- tissueSiteDetailIds:

  Character vector of IDs for tissues of interest. Can be GTEx specific
  IDs (e.g. "Whole_Blood"; use
  [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  to see valid values) or Ontology IDs.

- .return_raw:

  Logical. If `TRUE`, return the raw API JSON response. Default =
  `FALSE`

## Value

A tibble. Or a list if `.return_raw = TRUE`.

## See also

Other Expression Data Endpoints:
[`get_clustered_median_exon_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_exon_expression.md),
[`get_clustered_median_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_gene_expression.md),
[`get_clustered_median_transcript_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_transcript_expression.md),
[`get_expression_pca()`](https://docs.ropensci.org/gtexr/reference/get_expression_pca.md),
[`get_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_gene_expression.md),
[`get_median_exon_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_exon_expression.md),
[`get_median_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_gene_expression.md),
[`get_median_junction_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_junction_expression.md),
[`get_median_transcript_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_transcript_expression.md),
[`get_single_nucleus_gex()`](https://docs.ropensci.org/gtexr/reference/get_single_nucleus_gex.md),
[`get_single_nucleus_gex_summary()`](https://docs.ropensci.org/gtexr/reference/get_single_nucleus_gex_summary.md),
[`get_top_expressed_genes()`](https://docs.ropensci.org/gtexr/reference/get_top_expressed_genes.md)

## Examples

``` r
get_clustered_median_junction_expression(gencodeIds = c(
  "ENSG00000203782.5",
  "ENSG00000132693.12"
))
#> ℹ Retrieve clustering data with `attr(<df>, 'clusters')`
#> # A tibble: 432 × 8
#>    median junctionId           tissueSiteDetailId ontologyId datasetId gencodeId
#>     <dbl> <chr>                <chr>              <chr>      <chr>     <chr>    
#>  1      0 chr1_159712581_1597… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000…
#>  2      0 chr1_159712795_1597… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000…
#>  3      0 chr1_159712795_1597… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000…
#>  4      0 chr1_159713604_1597… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000…
#>  5      0 chr1_159713641_1597… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000…
#>  6      0 chr1_159713973_1597… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000…
#>  7      0 chr1_159714139_1597… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000…
#>  8      0 chr1_159712581_1597… Adipose_Visceral_… UBERON:00… gtex_v8   ENSG0000…
#>  9      0 chr1_159712795_1597… Adipose_Visceral_… UBERON:00… gtex_v8   ENSG0000…
#> 10      0 chr1_159712795_1597… Adipose_Visceral_… UBERON:00… gtex_v8   ENSG0000…
#> # ℹ 422 more rows
#> # ℹ 2 more variables: geneSymbol <chr>, unit <chr>

# clustering data is stored as an attribute "clusters"
result <- get_clustered_median_junction_expression(c(
  "ENSG00000203782.5",
  "ENSG00000132693.12"
))
#> ℹ Retrieve clustering data with `attr(<df>, 'clusters')`
attr(result, "clusters")
#> $junction
#> [1] "((((((chr1_159713641_159714006:0.03,chr1_159713604_159714002:0.03):0.67,(chr1_159712795_159714006:0.01,chr1_159712581_159713502:0.01):0.69):0.56,chr1_159712795_159713502:1.26):0.90,chr1_159713973_159714498:2.16):0.54,chr1_159714139_159714424:2.70):2.61,chr1_153259734_153260926:5.31);"
#> 
#> $tissue
#> [1] "(((((((((((((((((Adipose_Visceral_Omentum:0.00,Adipose_Subcutaneous:0.00):0.00,Artery_Aorta:0.00):0.00,Artery_Coronary:0.00):0.00,Artery_Tibial:0.00):0.00,Brain_Cortex:0.00):0.00,Breast_Mammary_Tissue:0.00):0.00,Colon_Sigmoid:0.00):0.00,Heart_Atrial_Appendage:0.00):0.00,Muscle_Skeletal:0.00):0.00,Nerve_Tibial:0.00):0.00,Vagina:0.00):0.08,Kidney_Medulla:0.08):0.03,(((((((((((((((((((((Brain_Amygdala:0.00,Bladder:0.00):0.00,Brain_Anterior_cingulate_cortex_BA24:0.00):0.00,Brain_Caudate_basal_ganglia:0.00):0.00,Brain_Cerebellar_Hemisphere:0.00):0.00,Brain_Cerebellum:0.00):0.00,Brain_Frontal_Cortex_BA9:0.00):0.00,Brain_Hippocampus:0.00):0.00,Brain_Hypothalamus:0.00):0.00,Brain_Nucleus_accumbens_basal_ganglia:0.00):0.00,Brain_Putamen_basal_ganglia:0.00):0.00,Brain_Spinal_cord_cervical_c-1:0.00):0.00,Brain_Substantia_nigra:0.00):0.00,Cells_EBV-transformed_lymphocytes:0.00):0.00,Colon_Transverse:0.00):0.00,Esophagus_Gastroesophageal_Junction:0.00):0.00,Esophagus_Muscularis:0.00):0.00,Heart_Left_Ventricle:0.00):0.00,Kidney_Cortex:0.00):0.00,Pituitary:0.00):0.00,Thyroid:0.00):0.00,Whole_Blood:0.00):0.11):0.03,((((((((((((Cells_Cultured_fibroblasts:0.00,Adrenal_Gland:0.00):0.00,Esophagus_Mucosa:0.00):0.00,Fallopian_Tube:0.00):0.00,Lung:0.00):0.00,Minor_Salivary_Gland:0.00):0.00,Ovary:0.00):0.00,Prostate:0.00):0.00,Small_Intestine_Terminal_Ileum:0.00):0.00,Spleen:0.00):0.00,Stomach:0.00):0.00,Uterus:0.00):0.06,((Cervix_Endocervix:0.00,Cervix_Ectocervix:0.00):0.00,Testis:0.00):0.06):0.09):0.19,Pancreas:0.33):0.27,(Skin_Sun_Exposed_Lower_leg:0.02,Skin_Not_Sun_Exposed_Suprapubic:0.02):0.59):0.68,Liver:1.29);"
#> 

# process clustering data with the ape package
# install.packages("ape")
# phylo_tree <- ape::read.tree(text = attr(result, "clusters")$tissue)
# plot(phylo_tree)
# print(phylo_tree)
```
