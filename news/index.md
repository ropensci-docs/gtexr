# Changelog

## gtexr (development version)

## gtexr 0.2.1

CRAN release: 2025-08-19

### Major changes

- **Breaking changes:**

  - [`get_sample_datasets()`](https://docs.ropensci.org/gtexr/reference/get_sample_datasets.md)
    has been fixed to return a tibble with one row per data item
    ([\#24](https://github.com/ropensci/gtexr/issues/24)).

## gtexr 0.2.0

CRAN release: 2025-04-23

### Major changes

- All functions now include a `.return_raw` argument, enabling the user
  to retrieve the raw JSON from API calls.

- Functions that return a paginated response now include a `.verbose`
  argument, which can be set to `FALSE` to suppress pagination messages.
  The `itemsPerPage` argument for these functions can also be set
  globally by adjusting option “gtexr.itemsPerPage”.

- [`get_dataset_info()`](https://docs.ropensci.org/gtexr/reference/get_dataset_info.md)
  has now been fixed (previously returned an empty tibble).

- **Breaking changes:**

  - `get_sample_datasets_endpoints()` has been renamed to
    [`get_sample_datasets()`](https://docs.ropensci.org/gtexr/reference/get_sample_datasets.md).
    This is to match the naming convention used for
    [`get_sample_biobank_data()`](https://docs.ropensci.org/gtexr/reference/get_sample_biobank_data.md),
    whereby ‘get_sample’ is appended with their respective category
    titles ‘datasets’ and ‘biobank_data’.

  - [`get_multi_tissue_eqtls()`](https://docs.ropensci.org/gtexr/reference/get_multi_tissue_eqtls.md)
    has been fixed to return a tibble with one row per data item.
    Argument `gencodeIds` has also been renamed to `gencodeId` to match
    the GTEx API.

### Minor changes and bug fixes

- Various function arguments have been updated to match the GTEx API:

  - [`get_sqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_sqtl_genes.md)
    argument `tissueSiteDetailId` has been pluralised to
    `tissueSiteDetailIds`.

  - [`get_eqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_eqtl_genes.md),
    [`get_sqtl_genes()`](https://docs.ropensci.org/gtexr/reference/get_sqtl_genes.md),
    [`get_exons()`](https://docs.ropensci.org/gtexr/reference/get_exons.md),
    [`get_neighbor_gene()`](https://docs.ropensci.org/gtexr/reference/get_neighbor_gene.md),
    [`get_subject()`](https://docs.ropensci.org/gtexr/reference/get_subject.md),
    [`get_tissue_site_detail()`](https://docs.ropensci.org/gtexr/reference/get_tissue_site_detail.md),
    [`get_significant_single_tissue_sqtls()`](https://docs.ropensci.org/gtexr/reference/get_significant_single_tissue_sqtls.md),
    [`download()`](https://docs.ropensci.org/gtexr/reference/download.md)
    and
    [`get_sample_datasets()`](https://docs.ropensci.org/gtexr/reference/get_sample_datasets.md)
    (formerly called `get_sample_datasets_endpoints()`) default argument
    values now match API.

## gtexr 0.1.0

CRAN release: 2024-09-19

- Initial version accepted on CRAN.
