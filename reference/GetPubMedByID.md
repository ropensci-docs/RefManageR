# Retrieve citation information from NCBI's Entrez for a set of PubMed IDs

Uses NCBI's E-Utilities to retrieve bibliographic information given a
vector of PubMed ID's and returns the results as a BibEntry object.

## Usage

``` r
GetPubMedByID(id, db = "pubmed", ...)
```

## Arguments

- id:

  character vector; PubMed ID's for searching NCBI's Entrez.

- db:

  string; Entrez database to search.

- ...:

  additional parameters to use for the search. See the Entrez
  documentation listed in the *References*.

## Value

a BibEntry object.

## Note

Returned entries will have `bibtype` “Article” or “Book”, unless a
collection title is present – in which case the `bibtype` will be
“InBook” – or there is no journal information returned for an article –
in which case the `bibtype` will be “Misc”.

## References

<https://www.ncbi.nlm.nih.gov/books/NBK25500/>

## See also

Other pubmed:
[`GetPubMedRelated()`](https://docs.ropensci.org/RefManageR/reference/GetPubMedRelated.md),
[`LookupPubMedID()`](https://docs.ropensci.org/RefManageR/reference/LookupPubMedID.md),
[`ReadCrossRef()`](https://docs.ropensci.org/RefManageR/reference/ReadCrossRef.md),
[`ReadPubMed()`](https://docs.ropensci.org/RefManageR/reference/ReadPubMed.md)

## Examples

``` r
if (interactive() && !httr::http_error("https://eutils.ncbi.nlm.nih.gov/"))
  GetPubMedByID(c("11209037", "21245076"))
```
