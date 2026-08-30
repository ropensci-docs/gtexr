# Get Clustered Median Exon Expression

Find median transcript expression data along with hierarchical clusters.

- Returns median normalized transcript expression in tissues of all
  known transcripts of a given gene along with the hierarchical
  clustering results of tissues and transcripts, based on exon
  expression, in Newick format.

- The hierarchical clustering is performed by calculating Euclidean
  distances and using the average linkage method.

- **This endpoint is not paginated.**

By default, this endpoint queries the latest GTEx release.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Expression-Data-Endpoints/operation/get_clustered_median_exon_expression_api_v2_expression_clusteredMedianExonExpression_get)

## Usage

``` r
get_clustered_median_exon_expression(
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
[`get_clustered_median_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_gene_expression.md),
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
get_clustered_median_exon_expression(c(
  "ENSG00000203782.5",
  "ENSG00000132693.12"
))
#> ℹ Retrieve clustering data with `attr(<df>, 'clusters')`
#> # A tibble: 216 × 8
#>     median exonId   tissueSiteDetailId ontologyId datasetId gencodeId geneSymbol
#>      <dbl> <chr>    <chr>              <chr>      <chr>     <chr>     <chr>     
#>  1  0.789  ENSG000… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000… CRP       
#>  2 16.8    ENSG000… Adipose_Subcutane… UBERON:00… gtex_v8   ENSG0000… CRP       
#>  3  0.0921 ENSG000… Adipose_Visceral_… UBERON:00… gtex_v8   ENSG0000… CRP       
#>  4 12      ENSG000… Adipose_Visceral_… UBERON:00… gtex_v8   ENSG0000… CRP       
#>  5  1      ENSG000… Adrenal_Gland      UBERON:00… gtex_v8   ENSG0000… CRP       
#>  6 22.7    ENSG000… Adrenal_Gland      UBERON:00… gtex_v8   ENSG0000… CRP       
#>  7  0      ENSG000… Artery_Aorta       UBERON:00… gtex_v8   ENSG0000… CRP       
#>  8  8      ENSG000… Artery_Aorta       UBERON:00… gtex_v8   ENSG0000… CRP       
#>  9  0      ENSG000… Artery_Coronary    UBERON:00… gtex_v8   ENSG0000… CRP       
#> 10 14      ENSG000… Artery_Coronary    UBERON:00… gtex_v8   ENSG0000… CRP       
#> # ℹ 206 more rows
#> # ℹ 1 more variable: unit <chr>

# clustering data is stored as an attribute "clusters"
result <- get_clustered_median_exon_expression(c(
  "ENSG00000203782.5",
  "ENSG00000132693.12"
))
#> ℹ Retrieve clustering data with `attr(<df>, 'clusters')`
attr(result, "clusters")
#> $exon
#> [1] "((ENSG00000203782.5_2:8.51,ENSG00000132693.12_2:8.51):0.79,(ENSG00000203782.5_1:5.92,ENSG00000132693.12_1:5.92):3.38);"
#> 
#> $tissue
#> [1] "(((((((((((Uterus:0.02,Stomach:0.02):0.04,(Pituitary:0.02,Brain_Cerebellum:0.02):0.04):0.01,((((Thyroid:0.03,Colon_Transverse:0.03):0.00,((Artery_Coronary:0.02,Adipose_Visceral_Omentum:0.02):0.00,(Esophagus_Muscularis:0.01,Esophagus_Gastroesophageal_Junction:0.01):0.01):0.01):0.01,Small_Intestine_Terminal_Ileum:0.04):0.00,Artery_Aorta:0.04):0.03):0.04,Kidney_Cortex:0.11):0.00,Brain_Cerebellar_Hemisphere:0.11):0.02,(((((((Ovary:0.01,Nerve_Tibial:0.01):0.00,Adipose_Subcutaneous:0.01):0.01,Esophagus_Mucosa:0.02):0.01,(Spleen:0.01,Breast_Mammary_Tissue:0.01):0.02):0.01,Minor_Salivary_Gland:0.03):0.01,(Prostate:0.02,Lung:0.02):0.02):0.04,Testis:0.09):0.04):0.02,((Fallopian_Tube:0.09,Cervix_Ectocervix:0.09):0.01,((Kidney_Medulla:0.06,Bladder:0.06):0.03,((Cells_Cultured_fibroblasts:0.01,Adrenal_Gland:0.01):0.04,Cervix_Endocervix:0.05):0.03):0.02):0.05):0.03,((Vagina:0.09,Brain_Hypothalamus:0.09):0.03,((((((Brain_Hippocampus:0.01,Brain_Amygdala:0.01):0.01,Cells_EBV-transformed_lymphocytes:0.02):0.01,Brain_Frontal_Cortex_BA9:0.02):0.01,((Brain_Nucleus_accumbens_basal_ganglia:0.00,Brain_Caudate_basal_ganglia:0.00):0.00,Brain_Putamen_basal_ganglia:0.01):0.03):0.02,(Brain_Cortex:0.02,Brain_Anterior_cingulate_cortex_BA24:0.02):0.03):0.02,(((((Brain_Substantia_nigra:0.01,Artery_Tibial:0.01):0.00,(Heart_Atrial_Appendage:0.00,Brain_Spinal_cord_cervical_c-1:0.00):0.00):0.00,Muscle_Skeletal:0.01):0.01,Colon_Sigmoid:0.02):0.01,(Whole_Blood:0.02,Heart_Left_Ventricle:0.02):0.02):0.04):0.05):0.06):0.20,Pancreas:0.39):0.34,(Skin_Sun_Exposed_Lower_leg:0.02,Skin_Not_Sun_Exposed_Suprapubic:0.02):0.71):0.12,Liver:0.85);"
#> 

# process clustering data with the ape package
# install.packages("ape")
# phylo_tree <- ape::read.tree(text = attr(result, "clusters")$tissue)
# plot(phylo_tree)
# print(phylo_tree)
```
