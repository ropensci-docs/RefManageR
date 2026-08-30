# Combine BibEntry objects.

Combines mutliple BibEntry objects into a single one.

## Usage

``` r
# S3 method for class 'BibEntry'
c(..., recursive = FALSE)
```

## Arguments

- ...:

  \- BibEntry objects to be concatenated.

- recursive:

  \- logical; ignored.

## Value

a single BibEntry object.

## Note

`c` will remove all attributes besides `class`.

No checking for duplicate entries is performed though keys will be made
unique.

## See also

Other operators:
[`$.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/cash-.BibEntry.md),
`$<-.BibEntry()`,
[`+.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/merge.BibEntry.md),
[`[.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md),
`[<-.BibEntry()`,
[`[[.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/sub-sub-.BibEntry.md),
`[[<-.BibEntry()`

## Examples

``` r
bib <- c(BibEntry(bibtype = "article", key = "mclean2014a", title = "My New Article",
  author = "Mathew W. McLean", journaltitle = "The Journal", date = "2014-01"),
  BibEntry(bibtype = "article", key = "mclean2014b",
  title = "My Newer Article", author = "Mathew W. McLean", journaltitle = "The Journal",
  date = "2014-02"))
```
