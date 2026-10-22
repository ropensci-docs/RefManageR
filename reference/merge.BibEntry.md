# Merge two BibEntry objects while discarding duplicates

Merges two BibEntry objects comparing only the specified fields to
detect duplicates, thus it is can be made less strict than using
`duplicated`, `unique`, etc. Attributes are also merged and keys are
ensured to be unique. `merge` and `+` simply provide different
interfaces for merging.

## Usage

``` r
# S3 method for class 'BibEntry'
e1 + e2

# S3 method for class 'BibEntry'
merge(
  x,
  y,
  fields.to.check = BibOptions()$merge.fields.to.check,
  ignore.case = BibOptions()$ignore.case,
  ...
)
```

## Arguments

- e1:

  BibEntry object

- e2:

  BibEntry object to be merged with e1

- x:

  BibEntry object

- y:

  BibEntry object

- fields.to.check:

  character vector; which BibLaTeX fields should be checked to determine
  if an entry is a duplicate? Can include `"bibtype"` to check entry
  type and `"key"` to check entry keys. Specifying `"all"` checks all
  fields using [`duplicated`](https://rdrr.io/r/base/duplicated.html).

- ignore.case:

  logical; if `TRUE`, case is ignored when determining if fields are
  duplicates.

- ...:

  ignored

## Value

an object of class BibEntry

## See also

[`duplicated`](https://rdrr.io/r/base/duplicated.html),
[`unique`](https://rdrr.io/r/base/unique.html)

Other operators:
[`$.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/cash-.BibEntry.md),
`$<-.BibEntry()`,
[`[.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md),
`[<-.BibEntry()`,
[`[[.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/sub-sub-.BibEntry.md),
`[[<-.BibEntry()`,
[`c.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/c.BibEntry.md)

## Author

McLean, M. W. <mathew.w.mclean@gmail.com>

## Examples

``` r
if (requireNamespace("bibtex")) {
    file.name <- system.file("Bib", "biblatexExamples.bib", package="RefManageR")
    bib <- suppressMessages(ReadBib(file.name))
    bib1 <- bib[seq_len(44)]
    bib2 <- bib[45:length(bib)]

    ## The following is FALSE because the parent entry of one entry in bib1
    ##   is in bib2, so the child entry is expanded in the BibEntry object
    ##   returned by `[` to include the fields inherited from the dropped parent
    identical(merge(bib1, bib2, 'all'), bib)
    toBiblatex(bib1[[1L]])
    toBiblatex(bib[[1L]])

    ## Alternatively, the operator `[[` for BibEntry objects does not expand
    ##   cross references
    bib1 <- bib[[seq_len(44)]]
    bib2 <- bib[[45:length(bib)]]
    identical(merge(bib1, bib2, 'all'), bib)

    ## Not strict enough
    invisible(merge(bib1, bib2, c('title', 'date')))
 }
#> Duplicate entries found in second BibEntry object in position(s): 1

## New publications of R.J. Carroll from Google Scholar and Crossref
if (FALSE) { # \dontrun{
if (requireNamespace("bibtex")) {
    bib1 <- ReadGS(scholar.id = "CJOHNoQAAAAJ", limit = '10', sort.by.date = TRUE)
    bib2 <- ReadCrossRef(query = "rj carroll", limit = 10, sort = "relevance",
      min.relevance = 80)
    oldopt <- BibOptions(merge.fields.to.check = "title")
    rjc.new.pubs <- bib1 + bib2
    BibOptions(oldopt)
}
} # }
```
