# Search NCBI's E-Utilities for citation information

This function takes a query and searches an Entrez database for
references using NCBI's E-Utilities, returning the results in a BibEntry
object.

## Usage

``` r
ReadPubMed(query, database = "PubMed", ...)
```

## Arguments

- query:

  string; search term.

- database:

  string; the Entrez database to search.

- ...:

  additional parameters to use for the search. See the *Details*.

## Value

an object of class BibEntry.

## Details

Optional additional parameters to pass to the server include

- `retstart` - index of the first retrieved ID that should be included
  in the results.

- `retmax` - maximum number of IDs the server will return (default 20).

- `field` - limits the query to search only the specified field (e.g.
  “title”).

- `datetype` - type of date to use when limiting search by dates. E.g.
  “mdat” for modification date or “pdat” for publication date.

- `reldate` - integer; only items that have (`datetype`) date values
  within `reldate` *days* of the current date will be returned.

- `mindate`, `maxdate` - date ranges to restrict search results.
  Possible formats are “YYYY”, “YYYY/MM”, and “YYYY/MM/DD”.

## Note

The returned entries will have type either ‘Article’ or ‘Misc’ depending
on whether journal information was retrieved. See the Entrez
documentation listed in the *References*.

The language of the entry will be returned in the field “language” and
the abstract will be returned in the field “abstract”, if they are
available.

## References

<https://www.ncbi.nlm.nih.gov/books/NBK25499/#chapter4.ESearch>

## See also

Other pubmed:
[`GetPubMedByID()`](https://docs.ropensci.org/RefManageR/reference/GetPubMedByID.md),
[`GetPubMedRelated()`](https://docs.ropensci.org/RefManageR/reference/GetPubMedRelated.md),
[`LookupPubMedID()`](https://docs.ropensci.org/RefManageR/reference/LookupPubMedID.md),
[`ReadCrossRef()`](https://docs.ropensci.org/RefManageR/reference/ReadCrossRef.md)

## Examples

``` r
if (interactive() && !httr::http_error("https://eutils.ncbi.nlm.nih.gov/"))
  ReadPubMed(query = "raymond carroll measurement error", retmax = 5, mindate = 1990)
```
