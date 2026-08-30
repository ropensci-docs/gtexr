# Get Sample (Datasets)

This service returns information of samples used in analyses from all
datasets. Results may be filtered by dataset ID, sample ID, subject ID,
sample metadata, or other provided parameters. By default, this service
queries the latest GTEx release.

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Datasets-Endpoints/operation/get_sample_api_v2_dataset_sample_get)

## Usage

``` r
get_sample_datasets(
  datasetId = "gtex_v8",
  sampleIds = NULL,
  tissueSampleIds = NULL,
  subjectIds = NULL,
  ageBrackets = NULL,
  sex = NULL,
  pathCategory = NULL,
  tissueSiteDetailIds = NULL,
  aliquotIds = NULL,
  autolysisScores = NULL,
  hardyScales = NULL,
  ischemicTimes = NULL,
  ischemicTimeGroups = NULL,
  rins = NULL,
  uberonIds = NULL,
  dataTypes = NULL,
  sortBy = "sampleId",
  sortDirection = "asc",
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

- datasetId:

  String. Unique identifier of a dataset. Usually includes a data source
  and data release. Options: "gtex_v8", "gtex_snrnaseq_pilot".

- sampleIds:

  Character vector. GTEx sample ID.

- tissueSampleIds:

  Array of strings. A list of Tissue Sample ID(s).

- subjectIds:

  Character vector. GTEx subject ID.

- ageBrackets:

  The age bracket(s) of the donors of interest. Options: "20-29",
  "30-39", "40-49", "50-59", "60-69", "70-79".

- sex:

  String. Options: "male", "female".

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

- tissueSiteDetailIds:

  Character vector of IDs for tissues of interest. Can be GTEx specific
  IDs (e.g. "Whole_Blood"; use
  [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  to see valid values) or Ontology IDs.

- aliquotIds:

  Character vector.

- autolysisScores:

  Character vector. Options: "None", "Mild", "Moderate", "Severe".

- hardyScales:

  Character vector. A list of Hardy Scale(s) of interest. Options:
  "Ventilator case", "Fast death - violent", "Fast death - natural
  causes", "Intermediate death", "Slow death".

- ischemicTimes:

  Integer.

- ischemicTimeGroups:

  Character vector. Options: "\<= 0", "1 - 300", "301 - 600", "601 -
  900", "901 - 1200", "1201 - 1500", "\> 1500".

- rins:

  Integer, vector.

- uberonIds:

  Character vector of Uberon IDs (e.g. "UBERON:EFO_0000572"; use
  [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md)
  to see valid values).

- dataTypes:

  Character vector. Options: "RNASEQ", "WGS", "WES", "OMNI", "EXCLUDE".

- sortBy:

  String. Options: "sampleId", "ischemicTime", "aliquotId",
  "tissueSampleId", "hardyScale", "pathologyNotes", "ageBracket",
  "tissueSiteDetailId", "sex".

- sortDirection:

  String. Options: "asc", "desc". Default = "asc".

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

Other Datasets Endpoints:
[`get_annotation()`](https://docs.ropensci.org/gtexr/reference/get_annotation.md),
[`get_collapsed_gene_model_exon()`](https://docs.ropensci.org/gtexr/reference/get_collapsed_gene_model_exon.md),
[`get_downloads_page_data()`](https://docs.ropensci.org/gtexr/reference/get_downloads_page_data.md),
[`get_file_list()`](https://docs.ropensci.org/gtexr/reference/get_file_list.md),
[`get_full_get_collapsed_gene_model_exon()`](https://docs.ropensci.org/gtexr/reference/get_full_get_collapsed_gene_model_exon.md),
[`get_functional_annotation()`](https://docs.ropensci.org/gtexr/reference/get_functional_annotation.md),
[`get_linkage_disequilibrium_by_variant_data()`](https://docs.ropensci.org/gtexr/reference/get_linkage_disequilibrium_by_variant_data.md),
[`get_linkage_disequilibrium_data()`](https://docs.ropensci.org/gtexr/reference/get_linkage_disequilibrium_data.md),
[`get_subject()`](https://docs.ropensci.org/gtexr/reference/get_subject.md),
[`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md),
[`get_variant()`](https://docs.ropensci.org/gtexr/reference/get_variant.md),
[`get_variant_by_location()`](https://docs.ropensci.org/gtexr/reference/get_variant_by_location.md)

## Examples

``` r
get_sample_datasets()
#> Warning: ! Total number of items (22734) exceeds the selected maximum page size (250).
#> ✖ 22484 items were not retrieved.
#> ℹ To retrieve all available items, increase `itemsPerPage`, ensuring you reuse
#>   your original query parameters e.g.
#>   `get_sample_datasets(<your_existing_parameters>, itemsPerPage = 100000)`
#> ℹ Alternatively, adjust global "gtexr.itemsPerPage" setting e.g.
#>   `options(list(gtexr.itemsPerPage = 100000))`
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 91
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems = 22734
#> # A tibble: 250 × 20
#>    ischemicTime aliquotId tissueSampleId       tissueSiteDetail         dataType
#>           <int> <chr>     <chr>                <chr>                    <chr>   
#>  1         1188 SM-58Q7G  GTEX-1117F-0003      Whole Blood              WES     
#>  2         1188 SM-5DWSB  GTEX-1117F-0003      Whole Blood              OMNI    
#>  3         1188 SM-6WBT7  GTEX-1117F-0003      Whole Blood              WGS     
#>  4         1193 SM-AHZ7F  GTEX-1117F-0011-R10a Brain - Frontal Cortex … NA      
#>  5         1193 SM-CYKQ8  GTEX-1117F-0011-R10b Brain - Frontal Cortex … NA      
#>  6         1214 SM-5GZZ7  GTEX-1117F-0226      Adipose - Subcutaneous   RNASEQ  
#>  7         1220 SM-5EGHI  GTEX-1117F-0426      Muscle - Skeletal        RNASEQ  
#>  8         1221 SM-5EGHJ  GTEX-1117F-0526      Artery - Tibial          RNASEQ  
#>  9         1243 SM-5N9CS  GTEX-1117F-0626      Artery - Coronary        RNASEQ  
#> 10         1244 SM-5GIEN  GTEX-1117F-0726      Heart - Atrial Appendage RNASEQ  
#> # ℹ 240 more rows
#> # ℹ 15 more variables: ischemicTimeGroup <chr>, freezeType <chr>,
#> #   sampleId <chr>, sampleIdUpper <chr>, ageBracket <chr>, hardyScale <chr>,
#> #   tissueSiteDetailId <chr>, subjectId <chr>, uberonId <chr>, sex <chr>,
#> #   datasetId <chr>, rin <dbl>, pathologyNotesCategories <tibble[,57]>,
#> #   pathologyNotes <chr>, autolysisScore <chr>
```
