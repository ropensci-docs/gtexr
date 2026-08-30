# Get Clustered Median Gene Expression

Find median gene expression data along with hierarchical clusters.

- Returns median gene expression in tissues along with The hierarchical
  clustering results of tissues and genes, based on gene expression, in
  Newick format.

- Results may be filtered by dataset, gene or tissue, but at least one
  gene must be provided

- The hierarchical clustering is performed by calculating Euclidean
  distances and using the average linkage method.

- **This endpoint is not paginated.**

By default, this service queries the latest GTEx release.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Expression-Data-Endpoints/operation/get_clustered_median_gene_expression_api_v2_expression_clusteredMedianGeneExpression_get)

## Usage

``` r
get_clustered_median_gene_expression(
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
[`get_clustered_median_junction_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_junction_expression.md),
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
get_clustered_median_gene_expression(gencodeIds = c(
  "ENSG00000203782.5",
  "ENSG00000132693.12"
))
#> ℹ Retrieve clustering data with `attr(<df>, 'clusters')`
#> # A tibble: 108 × 7
#>    median tissueSiteDetailId     ontologyId datasetId gencodeId geneSymbol unit 
#>     <dbl> <chr>                  <chr>      <chr>     <chr>     <chr>      <chr>
#>  1 0.347  Adipose_Subcutaneous   UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  2 0.240  Adipose_Visceral_Omen… UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  3 0.384  Adrenal_Gland          UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  4 0.198  Artery_Aorta           UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  5 0.332  Artery_Coronary        UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  6 0.117  Artery_Tibial          UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  7 0.631  Bladder                UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  8 0.0347 Brain_Amygdala         UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#>  9 0.0433 Brain_Anterior_cingul… UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#> 10 0.0226 Brain_Caudate_basal_g… UBERON:00… gtex_v8   ENSG0000… CRP        TPM  
#> # ℹ 98 more rows

# clustering data is stored as an attribute "clusters"
result <- get_clustered_median_gene_expression(c(
  "ENSG00000203782.5",
  "ENSG00000132693.12"
))
#> ℹ Retrieve clustering data with `attr(<df>, 'clusters')`
attr(result, "clusters")
#> $gene
#> [1] "Not enough data. At least three data sets are required for clustering."
#> 
#> $tissue
#> [1] "(((((((((((Cells_Cultured_fibroblasts:0.01,Bladder:0.01):0.01,Prostate:0.02):0.01,(Testis:0.02,Lung:0.02):0.02):0.01,(((((Thyroid:0.01,Minor_Salivary_Gland:0.01):0.01,Uterus:0.01):0.00,(((Artery_Coronary:0.00,Adipose_Subcutaneous:0.00):0.01,Small_Intestine_Terminal_Ileum:0.01):0.00,(Spleen:0.01,Breast_Mammary_Tissue:0.01):0.01):0.01):0.00,((Esophagus_Gastroesophageal_Junction:0.00,Adipose_Visceral_Omentum:0.00):0.00,Esophagus_Muscularis:0.01):0.01):0.01,((Ovary:0.00,Nerve_Tibial:0.00):0.01,Esophagus_Mucosa:0.01):0.02):0.01):0.00,(((((Stomach:0.00,Brain_Cerebellum:0.00):0.01,Pituitary:0.01):0.00,Colon_Transverse:0.01):0.01,Adrenal_Gland:0.02):0.00,(Kidney_Medulla:0.01,Kidney_Cortex:0.01):0.01):0.02):0.01,((((Whole_Blood:0.01,Heart_Left_Ventricle:0.01):0.01,Brain_Cerebellar_Hemisphere:0.02):0.01,(((Colon_Sigmoid:0.01,Brain_Substantia_nigra:0.01):0.00,(Muscle_Skeletal:0.00,Heart_Atrial_Appendage:0.00):0.00):0.00,((Brain_Nucleus_accumbens_basal_ganglia:0.00,Brain_Caudate_basal_ganglia:0.00):0.00,Brain_Putamen_basal_ganglia:0.01):0.01):0.01):0.01,(((((Cells_EBV-transformed_lymphocytes:0.00,Brain_Amygdala:0.00):0.00,Brain_Spinal_cord_cervical_c-1:0.01):0.00,Brain_Anterior_cingulate_cortex_BA24:0.01):0.00,Brain_Hippocampus:0.01):0.01,(Artery_Tibial:0.01,Artery_Aorta:0.01):0.01):0.01):0.02):0.02,(((Brain_Hypothalamus:0.01,Brain_Cortex:0.01):0.01,Brain_Frontal_Cortex_BA9:0.02):0.03,Vagina:0.05):0.02):0.03,((Cervix_Endocervix:0.02,Cervix_Ectocervix:0.02):0.01,Fallopian_Tube:0.04):0.07):0.10,Pancreas:0.20):0.37,(Skin_Sun_Exposed_Lower_leg:0.01,Skin_Not_Sun_Exposed_Suprapubic:0.01):0.56):0.07,Liver:0.64);"
#> 

# process clustering data with the ape package
# install.packages("ape")
# phylo_tree <- ape::read.tree(text = attr(result, "clusters")$tissue)
# plot(phylo_tree)
# print(phylo_tree)
```
