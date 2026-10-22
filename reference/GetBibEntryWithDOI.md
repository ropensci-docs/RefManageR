# Lookup a Bibtex entry using a Digital Object Identifier

Uses the DOI System API to look up bibliography information given a set
of DOIs.

## Usage

``` r
GetBibEntryWithDOI(
  doi,
  temp.file = tempfile(fileext = ".bib"),
  delete.file = TRUE
)
```

## Arguments

- doi:

  character vector; DOIs to use to retrieve bibliographic information.

- temp.file:

  string; a file to write the Bibtex data returned by the DOI System to.

- delete.file:

  logical; should `temp.file` be deleted when the function exits?

## Value

an object of class BibEntry.

## Details

The bibliographic information returned by the search of the
<https://www.doi.org/> API is temporarily written to a file and then
read back into `R` and return as a `BibEntry` object.

## References

<https://www.doi.org/tools.html>

## See also

[`ReadCrossRef`](https://docs.ropensci.org/RefManageR/reference/ReadCrossRef.md),
[`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md)

## Examples

``` r
if (interactive() && !httr::http_error("https://www.doi.org/"))
  GetBibEntryWithDOI(c("10.1016/j.iheduc.2003.11.004", "10.3998/3336451.0004.203"))
```
