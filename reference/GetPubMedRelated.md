# Retrieve related articles from PubMed using PubMed ID's

Searches PubMed for articles related to a set of PubMed ID's using
NCBI's E-Utilities.

## Usage

``` r
GetPubMedRelated(
  id,
  database = "pubmed",
  batch.mode = TRUE,
  max.results = 10,
  return.sim.scores = FALSE,
  return.related.ids = FALSE
)
```

## Arguments

- id:

  either a character vector of PubMed ID's or a BibEntry object, which
  is expected to have at least some entries with `eprinttype = "pubmed"`
  and eprint field specifying a PubMed ID.

- database:

  string; the Entrez database to search

- batch.mode:

  logical; if `TRUE`, the PubMed IDs in `id` are combined by Entrez when
  searching for linked IDs so that only one set of linked IDs is
  returned. If `FALSE`, a set of linked IDs is obtained for each ID in
  `id`. will be returned

- max.results:

  numeric vector; the maximum number of results to return if
  `batch.mode` `TRUE`; or if `batch.mode` is `FALSE`, this should have
  the same length as `id` with each element giving the maximum number of
  results to return for the corresponding ID.

- return.sim.scores:

  logical; Entrez returns a similarity score with each returned citation
  giving a measure of how similar the returned entry is to the ones
  specified by the query. If `TRUE` these scores are added to the
  returned BibEntry object in a field called ‘score’.

- return.related.ids:

  logical; should the original PubMed ID(s) that a returned entry is
  related to be stored in a field called ‘PMIDrelated’.

## Value

an object of class BibEntry.

## References

<https://www.ncbi.nlm.nih.gov/books/NBK25500/>

## See also

Other pubmed:
[`GetPubMedByID()`](https://docs.ropensci.org/RefManageR/reference/GetPubMedByID.md),
[`LookupPubMedID()`](https://docs.ropensci.org/RefManageR/reference/LookupPubMedID.md),
[`ReadCrossRef()`](https://docs.ropensci.org/RefManageR/reference/ReadCrossRef.md),
[`ReadPubMed()`](https://docs.ropensci.org/RefManageR/reference/ReadPubMed.md)

## Examples

``` r
if (interactive() && !httr::http_error("https://eutils.ncbi.nlm.nih.gov/")){
  file.name <- system.file("Bib", "RJC.bib", package="RefManageR")
  bib <- ReadBib(file.name)
  bib <- LookupPubMedID(bib[[101:102]])
  toBiblatex(GetPubMedRelated(bib, batch.mode = TRUE, max.results = 2,
  return.sim.scores = TRUE, return.related.ids = TRUE))
  GetPubMedRelated(bib, batch.mode = FALSE, max.results = c(2, 2))
}
```
