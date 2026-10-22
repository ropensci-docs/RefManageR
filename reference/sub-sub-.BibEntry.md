# Extract entries from a BibEntry object by index

Operator for extracting BibEntry objects by index.

## Usage

``` r
# S3 method for class 'BibEntry'
x[[i, drop = FALSE]]
```

## Arguments

- x:

  a BibEntry object

- i:

  numeric indices of entries to extract, or a character vector of keys
  corresponding to the entries to be extracted.

- drop:

  logical, should attributes besides class be dropped from result?

## Value

an object of class BibEntry.

## Note

This method is different than the usual operator `[[` for lists in that
a vector of indices may be specified.

This method behaves differently than the `[` operator for BibEntry
objects in that it does not expand crossreferences when returning, so
that a parent entry or xdata entry will be dropped if it is not also
indexed when indexing the child entry.

This method is not affected by the value of `BibOptions()$return.ind`.

## See also

Other operators:
[`$.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/cash-.BibEntry.md),
`$<-.BibEntry()`,
[`+.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/merge.BibEntry.md),
[`[.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md),
`[<-.BibEntry()`, `[[<-.BibEntry()`,
[`c.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/c.BibEntry.md)

## Examples

``` r
if (requireNamespace("bibtex")) {
    file.name <- system.file("Bib", "biblatexExamples.bib", package="RefManageR")
    bib <- suppressMessages(ReadBib(file.name))
    bib[[20:21]]
    bib[c("hyman", "loh")]

    ## Note this is FALSE because [[ does not inherit from the dropped parent entry while [ does.
    identical(bib[1], bib[[1]])
}
#> [1] FALSE
```
