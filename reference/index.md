# Package index

## GTEx Portal API Info

Retrieve general service information about the GTEx API.

- [`get_service_info()`](https://docs.ropensci.org/gtexr/reference/get_service_info.md)
  : Get Service Info

## Admin Endpoints

Access maintenance messages and news updates from GTEx.

- [`get_maintenance_message()`](https://docs.ropensci.org/gtexr/reference/get_maintenance_message.md)
  : Get Maintenance Message
- [`get_news_item()`](https://docs.ropensci.org/gtexr/reference/get_news_item.md)
  : Get News Item

## Static Association Endpoints

Query precomputed eQTL and sQTL associations across tissues.

- [`get_eqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_eqtl_genes.md)
  : Get Eqtl Genes
- [`get_fine_mapping()`](https://docs.ropensci.org/gtexr/reference/get_fine_mapping.md)
  : Get Fine Mapping
- [`get_independent_eqtl()`](https://docs.ropensci.org/gtexr/reference/get_independent_eqtl.md)
  : Get Independent Eqtl
- [`get_multi_tissue_eqtls()`](https://docs.ropensci.org/gtexr/reference/get_multi_tissue_eqtls.md)
  : Get Multi Tissue Eqtls
- [`get_significant_single_tissue_eqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_eqtls.md)
  : Get Significant Single Tissue Eqtls
- [`get_significant_single_tissue_eqtls_by_location()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_eqtls_by_location.md)
  : Get Significant Single Tissue eQTLs By Location
- [`get_significant_single_tissue_ieqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_ieqtls.md)
  : Get Significant Single Tissue Ieqtls
- [`get_significant_single_tissue_isqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_isqtls.md)
  : Get Significant Single Tissue Isqtls
- [`get_significant_single_tissue_sqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_sqtls.md)
  : Get Significant Single Tissue Sqtls
- [`get_sqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_sqtl_genes.md)
  : Get Sqtl Genes

## Dynamic Association Endpoints

Perform on-the-fly eQTL and sQTL calculations.

- [`calculate_expression_quantitative_trait_loci()`](https://docs.ropensci.org/gtexr/reference/calculate_expression_quantitative_trait_loci.md)
  : Calculate Expression Quantitative Trait Loci
- [`calculate_ieqtls()`](https://docs.ropensci.org/gtexr/reference/calculate_ieqtls.md)
  : Calculate Ieqtls
- [`calculate_isqtls()`](https://docs.ropensci.org/gtexr/reference/calculate_isqtls.md)
  : Calculate Isqtls
- [`calculate_splicing_quantitative_trait_loci()`](https://docs.ropensci.org/gtexr/reference/calculate_splicing_quantitative_trait_loci.md)
  : Calculate Splicing Quantitative Trait Loci

## Biobank Data Endpoints

Retrieve metadata on biobank samples.

- [`download()`](https://docs.ropensci.org/gtexr/reference/download.md)
  : Download
- [`get_sample_biobank_data()`](https://docs.ropensci.org/gtexr/reference/get_sample_biobank_data.md)
  : Get Sample (Biobank Data)

## Datasets Endpoints

Access various GTEx dataset information, as well as variant annotation
and linkage disequilibrium data.

- [`get_annotation()`](https://docs.ropensci.org/gtexr/reference/get_annotation.md)
  : Get Annotation
- [`get_collapsed_gene_model_exon()`](https://docs.ropensci.org/gtexr/reference/get_collapsed_gene_model_exon.md)
  : Get Collapsed Gene Model Exon
- [`get_downloads_page_data()`](https://docs.ropensci.org/gtexr/reference/get_downloads_page_data.md)
  : Get Downloads Page Data
- [`get_file_list()`](https://docs.ropensci.org/gtexr/reference/get_file_list.md)
  : Get File List
- [`get_full_get_collapsed_gene_model_exon()`](https://docs.ropensci.org/gtexr/reference/get_full_get_collapsed_gene_model_exon.md)
  : Get Full Get Collapsed Gene Model Exon
- [`get_functional_annotation()`](https://docs.ropensci.org/gtexr/reference/get_functional_annotation.md)
  : Get Functional Annotation
- [`get_linkage_disequilibrium_by_variant_data()`](https://docs.ropensci.org/gtexr/reference/get_linkage_disequilibrium_by_variant_data.md)
  : Get Linkage Disequilibrium By Variant Data
- [`get_linkage_disequilibrium_data()`](https://docs.ropensci.org/gtexr/reference/get_linkage_disequilibrium_data.md)
  : Get Linkage Disequilibrium Data
- [`get_sample_datasets()`](https://docs.ropensci.org/gtexr/reference/get_sample_datasets.md)
  : Get Sample (Datasets)
- [`get_subject()`](https://docs.ropensci.org/gtexr/reference/get_subject.md)
  : Get Subject
- [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  : Get Tissue Site Detail
- [`get_variant()`](https://docs.ropensci.org/gtexr/reference/get_variant.md)
  : Get Variant
- [`get_variant_by_location()`](https://docs.ropensci.org/gtexr/reference/get_variant_by_location.md)
  : Get Variant By Location

## Expression Data Endpoints

Obtain expression levels across tissues, including gene, exon, junction,
and transcript-level data.

- [`get_clustered_median_exon_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_exon_expression.md)
  : Get Clustered Median Exon Expression
- [`get_clustered_median_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_gene_expression.md)
  : Get Clustered Median Gene Expression
- [`get_clustered_median_junction_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_junction_expression.md)
  : Get Clustered Median Junction Expression
- [`get_clustered_median_transcript_expression()`](https://docs.ropensci.org/gtexr/reference/get_clustered_median_transcript_expression.md)
  : Get Clustered Median Transcript Expression
- [`get_expression_pca()`](https://docs.ropensci.org/gtexr/reference/get_expression_pca.md)
  : Get Expression Pca
- [`get_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_gene_expression.md)
  : Get Gene Expression
- [`get_median_exon_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_exon_expression.md)
  : Get Median Exon Expression
- [`get_median_gene_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_gene_expression.md)
  : Get Median Gene Expression
- [`get_median_junction_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_junction_expression.md)
  : Get Median Junction Expression
- [`get_median_transcript_expression()`](https://docs.ropensci.org/gtexr/reference/get_median_transcript_expression.md)
  : Get Median Transcript Expression
- [`get_single_nucleus_gex()`](https://docs.ropensci.org/gtexr/reference/get_single_nucleus_gex.md)
  : Get Single Nucleus Gex
- [`get_single_nucleus_gex_summary()`](https://docs.ropensci.org/gtexr/reference/get_single_nucleus_gex_summary.md)
  : Get Single Nucleus Gex Summary
- [`get_top_expressed_genes()`](https://docs.ropensci.org/gtexr/reference/get_top_expressed_genes.md)
  : Get Top Expressed Genes

## Histology Endpoints

Retrieve tissue histology image data.

- [`get_image()`](https://docs.ropensci.org/gtexr/reference/get_image.md)
  : Get Image

## Metadata Endpoints

Get dataset metadata (currently not active).

- [`get_dataset_info()`](https://docs.ropensci.org/gtexr/reference/get_dataset_info.md)
  : Get Dataset Info

## Reference Genome Endpoints

Query reference genome features, including genetic coordinates for
genes, transcripts and exons, as well as reported phenotype associations
for a region.

- [`get_exons()`](https://docs.ropensci.org/gtexr/reference/get_exons.md)
  : Get Exons
- [`get_gene_search()`](https://docs.ropensci.org/gtexr/reference/get_gene_search.md)
  : Get Gene Search
- [`get_genes()`](https://docs.ropensci.org/gtexr/reference/get_genes.md)
  : Get Genes
- [`get_genomic_features()`](https://docs.ropensci.org/gtexr/reference/get_genomic_features.md)
  : Get Genomic Features
- [`get_gwas_catalog_by_location()`](https://docs.ropensci.org/gtexr/reference/get_gwas_catalog_by_location.md)
  : Get Gwas Catalog By Location
- [`get_neighbor_gene()`](https://docs.ropensci.org/gtexr/reference/get_neighbor_gene.md)
  : Get Neighbor Gene
- [`get_transcripts()`](https://docs.ropensci.org/gtexr/reference/get_transcripts.md)
  : Get Transcripts
