# Replace values for a particular field in a BibEntry object

Used to replace the values stored for a specified field in a BibEntry
object.

## Usage

``` r
# S3 method for class 'BibEntry'
x$name <- value
```

## Arguments

- x:

  a BibEntry object

- name:

  string; the field to assign the new values to.

- value:

  character vector; the replacement field values to be assigned.

## Value

an object of class BibEntry with the updated fields.

## Note

The method expects date and name list fields to be in the format
expected by Biblatex. The field specified by `name` does not have to be
one currently in `x`.

## See also

Other operators:
[`$.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/cash-.BibEntry.md),
[`+.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/merge.BibEntry.md),
[`[.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md),
`[<-.BibEntry()`,
[`[[.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/sub-sub-.BibEntry.md),
`[[<-.BibEntry()`,
[`c.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/c.BibEntry.md)

## Examples

``` r
bib <- BibEntry(bibtype = "misc", key = "mclean", author = "Mathew W. McLean", 
  title = "My Work", year = "2012")
bib$year <- 2014
bib$author <- "McLean, M. W. and Carroll, R. J." 
bib$url <- "https://example.com"
bib
#> [1] M. W. McLean and R. J. Carroll. _My Work_. 2014.
#> <https://example.com>.

bib <- c(bib, as.BibEntry(citation()))
bib[1]$author[2] <- person(c("Raymond", "J."), "Carroll")
#> Error in eval(kal): object '*tmp*' not found
bib$author
#> $mclean
#> [1] "M. W. McLean"  "R. J. Carroll"
#> 
#> $`2026language`
#> [1] "R Core Team (ROR: <https://ror.org/02zz1nj61>)"
#> 
```
