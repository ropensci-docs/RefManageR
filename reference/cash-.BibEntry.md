# Extract fields from a BibEntry object

used to extract a single field from each entry in a BibEntry object

## Usage

``` r
# S3 method for class 'BibEntry'
x$name
```

## Arguments

- x:

  an object of class BibEntry

- name:

  the field to extract

## Value

a named list of values for the field specified by name for each entry;
`NULL` if the field is not present for a particular entry. The names
attribute of the returned list contains the entry keys (potentially
back-quoted).

## Note

`name` may be “bibtype” to extract entry types or “key” to extract keys.

## See also

Other operators: `$<-.BibEntry()`,
[`+.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/merge.BibEntry.md),
[`[.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md),
`[<-.BibEntry()`,
[`[[.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/sub-sub-.BibEntry.md),
`[[<-.BibEntry()`,
[`c.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/c.BibEntry.md)

## Examples

``` r
if (requireNamespace("bibtex")) {
    file.name <- system.file("Bib", "biblatexExamples.bib", package="RefManageR")
    bib <- suppressMessages(ReadBib(file.name))
    bib[[50:55]]$author
    bib[[seq_len(5)]]$bibtype
 }
#> $`westfahl:space`
#> [1] "InCollection"
#> 
#> $set
#> [1] "Set"
#> 
#> $stdmodel
#> [1] "Set"
#> 
#> $aksin
#> [1] "Article"
#> 
#> $angenendt
#> [1] "Article"
#> 
```
