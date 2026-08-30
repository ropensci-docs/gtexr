# Download

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Biobank-Data-Endpoints/operation/download_api_v2_biobank_download_get)

## Usage

``` r
download(
  materialTypes = NULL,
  tissueSiteDetailIds = NULL,
  pathCategory = NULL,
  tissueSampleIds = NULL,
  sex = NULL,
  sortBy = "sampleId",
  sortDirection = "asc",
  searchTerm = NULL,
  sampleIds = NULL,
  subjectIds = NULL,
  ageBrackets = NULL,
  hardyScales = NULL,
  hasExpressionData = NULL,
  hasGenotype = NULL,
  .return_raw = FALSE
)
```

## Arguments

- materialTypes:

  String, vector. Options: "Cells:Cell Line Viable", "DNA:DNA Genomic",
  "DNA:DNA Somatic", "RNA:Total RNA", "Tissue:PAXgene Preserved",
  "Tissue:PAXgene Preserved Paraffin-embedded", "Tissue:Fresh Frozen
  Tissue".

- tissueSiteDetailIds:

  Character vector of IDs for tissues of interest. Can be GTEx specific
  IDs (e.g. "Whole_Blood"; use
  [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  to see valid values) or Ontology IDs.

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

- tissueSampleIds:

  Array of strings. A list of Tissue Sample ID(s).

- sex:

  String. Options: "male", "female".

- sortBy:

  String. Options: "sampleId", "ischemicTime", "aliquotId",
  "tissueSampleId", "hardyScale", "pathologyNotes", "ageBracket",
  "tissueSiteDetailId", "sex".

- sortDirection:

  String. Options: "asc", "desc". Default = "asc".

- searchTerm:

  String.

- sampleIds:

  Character vector. GTEx sample ID.

- subjectIds:

  Character vector. GTEx subject ID.

- ageBrackets:

  The age bracket(s) of the donors of interest. Options: "20-29",
  "30-39", "40-49", "50-59", "60-69", "70-79".

- hardyScales:

  Character vector. A list of Hardy Scale(s) of interest. Options:
  "Ventilator case", "Fast death - violent", "Fast death - natural
  causes", "Intermediate death", "Slow death".

- hasExpressionData:

  Logical.

- hasGenotype:

  Logical.

- .return_raw:

  Logical. If `TRUE`, return the raw API JSON response. Default =
  `FALSE`

## Value

A tibble. Or a list if `.return_raw = TRUE`.

## Details

Note: running this request with no filters (i.e. `download()`) raises an
error.

## See also

Other Biobank Data Endpoints:
[`get_sample_biobank_data()`](https://docs.ropensci.org/gtexr/reference/get_sample_biobank_data.md)

## Examples

``` r
download(
  materialTypes = "RNA:Total RNA",
  tissueSiteDetailIds = "Thyroid",
  pathCategory = "clean_specimens",
  sex = "male",
  ageBrackets = "50-59"
)
#> # A tibble: 0 × 0
```
