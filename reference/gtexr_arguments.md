# gtexr arguments

Internal function that documents all arguments for exported gtexr
functions that wrap GTEx Portal API endpoints (using roxygen
`@inheritParams` tag).

## Usage

``` r
gtexr_arguments(
  ageBrackets = NULL,
  aliquotIds = NULL,
  attributeSubset = NULL,
  autolysisScores = NULL,
  cellType = NULL,
  bp_window = NULL,
  chromosome = NULL,
  datasetId = NULL,
  dataTypes = NULL,
  draw = NULL,
  end = NULL,
  excludeDataArray = NULL,
  .featureId = NULL,
  filterMtGene = NULL,
  gencodeId = NULL,
  gencodeIds = NULL,
  gencodeVersion = NULL,
  geneId = NULL,
  geneIds = NULL,
  genomeBuild = NULL,
  hardyScale = NULL,
  hardyScales = NULL,
  hasExpressionData = NULL,
  hasGenotype = NULL,
  itemsPerPage = NULL,
  ischemicTimes = NULL,
  ischemicTimeGroups = NULL,
  materialTypes = NULL,
  organizationName = NULL,
  page = NULL,
  pathCategory = NULL,
  phenotypeId = NULL,
  pos = NULL,
  poss = NULL,
  project_id = NULL,
  .return_raw = NULL,
  rins = NULL,
  sampleId = NULL,
  sampleIds = NULL,
  searchTerm = NULL,
  sex = NULL,
  snpId = NULL,
  sortBy = NULL,
  sortDirection = NULL,
  start = NULL,
  subjectIds = NULL,
  tissueSampleIds = NULL,
  tissueSiteDetailId = NULL,
  tissueSiteDetailIds = NULL,
  uberonIds = NULL,
  variantId = NULL,
  variantIds = NULL,
  .verbose = NULL
)
```

## Arguments

- ageBrackets:

  The age bracket(s) of the donors of interest. Options: "20-29",
  "30-39", "40-49", "50-59", "60-69", "70-79".

- aliquotIds:

  Character vector.

- attributeSubset:

  String. Examples include but are not limited to "sex", "ageBracket"

- autolysisScores:

  Character vector. Options: "None", "Mild", "Moderate", "Severe".

- cellType:

  String. "Adipocytes", "Epithelial_cells", "Hepatocytes",
  "Keratinocytes", "Myocytes", "Neurons", "Neutrophils".

- bp_window:

  Integer.

- chromosome:

  String. One of "chr1", "chr2", "chr3", "chr4", "chr5", "chr6", "chr7",
  "chr8", "chr9", "chr10", "chr11", "chr12", "chr13", "chr14", "chr15",
  "chr16", "chr17", "chr18", "chr19", "chr20", "chr21", "chr22", "chrM",
  "chrX", "chrY".

- datasetId:

  String. Unique identifier of a dataset. Usually includes a data source
  and data release. Options: "gtex_v8", "gtex_snrnaseq_pilot".

- dataTypes:

  Character vector. Options: "RNASEQ", "WGS", "WES", "OMNI", "EXCLUDE".

- draw:

  Integer.

- end:

  Integer.

- excludeDataArray:

  String. Options are TRUE or FALSE

- .featureId:

  String. A genomic feature e.g. GENCODE ID, RSID or GTEx Variant ID.

- filterMtGene:

  Logical. Exclude mitochondrial genes.

- gencodeId:

  String. A Versioned GENCODE ID of a gene, e.g. "ENSG00000065613.9".

- gencodeIds:

  A character vector of Versioned GENCODE IDs, e.g.
  c("ENSG00000132693.12", "ENSG00000203782.5").

- gencodeVersion:

  String (default = "v26"). GENCODE annotation release. Either "v26" or
  "v19".

- geneId:

  String. A gene symbol, a gencode ID, or an Ensemble ID.

- geneIds:

  A character vector of gene symbols, versioned gencodeIds, or
  unversioned gencodeIds.

- genomeBuild:

  String. Options: "GRCh38/hg38", "GRCh37/hg19". Default =
  "GRCh38/hg38".

- hardyScale:

  String A Hardy Scale of interest. Options: "Ventilator case", "Fast
  death - violent", "Fast death - natural causes", "Intermediate death",
  "Slow death".

- hardyScales:

  Character vector. A list of Hardy Scale(s) of interest. Options:
  "Ventilator case", "Fast death - violent", "Fast death - natural
  causes", "Intermediate death", "Slow death".

- hasExpressionData:

  Logical.

- hasGenotype:

  Logical.

- itemsPerPage:

  Integer (default = 250). Set globally to maximum value 100000 with
  `options(list(gtexr.itemsPerPage = 100000))`.

- ischemicTimes:

  Integer.

- ischemicTimeGroups:

  Character vector. Options: "\<= 0", "1 - 300", "301 - 600", "601 -
  900", "901 - 1200", "1201 - 1500", "\> 1500".

- materialTypes:

  String, vector. Options: "Cells:Cell Line Viable", "DNA:DNA Genomic",
  "DNA:DNA Somatic", "RNA:Total RNA", "Tissue:PAXgene Preserved",
  "Tissue:PAXgene Preserved Paraffin-embedded", "Tissue:Fresh Frozen
  Tissue".

- organizationName:

  String. Options: "GTEx Consortium" "Kid's First".

- page:

  Integer (default = 0).

- pathCategory:

  Character vector. Options: "adenoma", "amylacea", "atelectasis",
  "atherosclerosis", "atherosis", "atrophy", "calcification",
  "cirrhosis", "clean_specimens", "congestion", "corpora_albicantia",
  "cyst", "desquamation", "diabetic", "dysplasia", "edema", "emphysema",
  "esophagitis", "fibrosis", "gastritis", "glomerulosclerosis",
  "goiter", "gynecomastoid", "hashimoto", "heart_failure_cells",
  "hemorrhage", "hepatitis", "hyalinization", "hypereosinophilia",
  "hyperplasia", "hypertrophy", "hypoxic", "infarction", "inflammation",
  "ischemic_changes", "macrophages", "mastopathy", "metaplasia",
  "monckeberg", "necrosis", "nephritis", "nephrosclerosis",
  "no_abnormalities", "nodularity", "pancreatitis", "pigment",
  "pneumonia", "post_menopausal", "prostatitis", "saponification",
  "scarring", "sclerotic", "solar_elastosis", "spermatogenesis",
  "steatosis", "sweat_glands", "tma".

- phenotypeId:

  String. See [GTEx portal
  FAQs](https://www.gtexportal.org/home/faq#splicingPhenotypeId) for
  further details.

- pos:

  Integer.

- poss:

  Integer, vector.

- project_id:

  String. Options: "gtex", "adult-gtex", "egtex".

- .return_raw:

  Logical. If `TRUE`, return the raw API JSON response. Default =
  `FALSE`

- rins:

  Integer, vector.

- sampleId:

  String. `^GTEX-[A-Z0-9]{5}-[0-9]{4}-SM-[A-Z0-9]{5}$`

- sampleIds:

  Character vector. GTEx sample ID.

- searchTerm:

  String.

- sex:

  String. Options: "male", "female".

- snpId:

  String

- sortBy:

  String. Options: "sampleId", "ischemicTime", "aliquotId",
  "tissueSampleId", "hardyScale", "pathologyNotes", "ageBracket",
  "tissueSiteDetailId", "sex".

- sortDirection:

  String. Options: "asc", "desc". Default = "asc".

- start:

  Integer.

- subjectIds:

  Character vector. GTEx subject ID.

- tissueSampleIds:

  Array of strings. A list of Tissue Sample ID(s).

- tissueSiteDetailId:

  String. The ID of the tissue of interest. Can be a GTEx specific ID
  (e.g. "Whole_Blood"; use
  [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  to see valid values) or an Ontology ID.

- tissueSiteDetailIds:

  Character vector of IDs for tissues of interest. Can be GTEx specific
  IDs (e.g. "Whole_Blood"; use
  [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  to see valid values) or Ontology IDs.

- uberonIds:

  Character vector of Uberon IDs (e.g. "UBERON:EFO_0000572"; use
  [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  to see valid values).

- variantId:

  String. A gtex variant ID.

- variantIds:

  Character vector. Gtex variant IDs.

- .verbose:

  Logical. If `TRUE` (default), print paging information. Set to `FALSE`
  globally with `options(list(gtexr.verbose = FALSE))`.

## Value

A tibble of gtexr arguments and their metadata. Used for documentation
only.
