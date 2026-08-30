# Get Sample (Biobank Data)

[GTEx Portal API
documentation](https://gtexportal.org/api/v2/redoc#tag/Biobank-Data-Endpoints/operation/get_sample_api_v2_biobank_sample_get)

## Usage

``` r
get_sample_biobank_data(
  draw = NULL,
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
  page = 0,
  itemsPerPage = getOption("gtexr.itemsPerPage"),
  .verbose = getOption("gtexr.verbose"),
  .return_raw = FALSE
)
```

## Arguments

- draw:

  Integer.

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

Other Biobank Data Endpoints:
[`download()`](https://docs.ropensci.org/gtexr/reference/download.md)

## Examples

``` r
get_sample_biobank_data(tissueSiteDetailIds = "Whole_Blood")
#> Warning: ! Total number of items (1360) exceeds the selected maximum page size (250).
#> ✖ 1110 items were not retrieved.
#> ℹ To retrieve all available items, increase `itemsPerPage`, ensuring you reuse
#>   your original query parameters e.g.
#>   `get_sample_biobank_data(<your_existing_parameters>, itemsPerPage = 100000)`
#> ℹ Alternatively, adjust global "gtexr.itemsPerPage" setting e.g.
#>   `options(list(gtexr.itemsPerPage = 100000))`
#> 
#> ── Paging info ─────────────────────────────────────────────────────────────────
#> • numberOfPages = 6
#> • page = 0
#> • maxItemsPerPage = 250
#> • totalNumberOfItems (recordsFiltered) = 1360
#> • recordsTotal = 75502
#> # A tibble: 250 × 26
#>    materialType    sampleId       sampleIdUpper sex   hasGTExImage concentration
#>    <chr>           <chr>          <chr>         <chr> <lgl>                <dbl>
#>  1 DNA:DNA Genomic GTEX-1117F-00… GTEX-1117F-0… fema… FALSE               125   
#>  2 RNA:Total RNA   GTEX-1117F-00… GTEX-1117F-0… fema… FALSE               154   
#>  3 RNA:Total RNA   GTEX-1117F-00… GTEX-1117F-0… fema… FALSE                41.2 
#>  4 RNA:Total RNA   GTEX-111CU-00… GTEX-111CU-0… male  FALSE                96.0 
#>  5 DNA:DNA Genomic GTEX-111FC-00… GTEX-111FC-0… male  FALSE               125   
#>  6 DNA:DNA Genomic GTEX-111FC-00… GTEX-111FC-0… male  FALSE                 4.35
#>  7 DNA:DNA Genomic GTEX-111FC-00… GTEX-111FC-0… male  FALSE                 4.35
#>  8 RNA:Total RNA   GTEX-111FC-00… GTEX-111FC-0… male  FALSE               128.  
#>  9 RNA:Total RNA   GTEX-111FC-00… GTEX-111FC-0… male  FALSE               128.  
#> 10 RNA:Total RNA   GTEX-111FC-00… GTEX-111FC-0… male  FALSE               128.  
#> # ℹ 240 more rows
#> # ℹ 20 more variables: analysisRelease <chr>, genotype <chr>, hardyScale <chr>,
#> #   pathologyNotes <chr>, subjectId <chr>, tissueSiteDetailId <chr>,
#> #   hasGenotype <lgl>, originalMaterialType <chr>, aliquotId <chr>,
#> #   tissueSampleId <chr>, ageBracket <chr>, brainTissueDonor <lgl>,
#> #   volume <dbl>, hasExpressionData <lgl>, hasBRDImage <lgl>,
#> #   tissueSiteDetail <chr>, amount <dbl>, mass <dbl>, tissueSite <chr>, …
```
