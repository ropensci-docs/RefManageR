# Coerce to a Data Frame

Coerces a BibEntry object to a data.frame, with each row of the data
frame being a field present in at least one entry in the BibEntry object
being coerced.

## Usage

``` r
# S3 method for class 'BibEntry'
as.data.frame(x, row.names = NULL, optional = FALSE, ...)
```

## Arguments

- x:

  \- a BibEntry object

- row.names:

  \- ignored

- optional:

  \- ignored

- ...:

  \- ignored

## Value

a data.frame object with row names giving the keys, and first column
giving entry type.

## See also

[`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md),
[`as.BibEntry`](https://docs.ropensci.org/RefManageR/reference/as.BibEntry.md)

## Examples

``` r
bib <- list(c(bibtype = "article", key = "mclean2014a", title = "My New Article",
  author = "Mathew W. McLean", journaltitle = "The Journal", date = "2014-01"),
  c(bibtype = "article", key = "mclean2014b", volume = 10, title = "My Newer Article",
  author = "Mathew W. McLean", journaltitle = "The Journal", date = "2014-02"))
bib <- as.BibEntry(bib)
as.data.frame(bib)
#>             bibtype            title           author journaltitle    date
#> mclean2014a Article   My New Article Mathew W. McLean  The Journal 2014-01
#> mclean2014b Article My Newer Article Mathew W. McLean  The Journal 2014-02
#>             volume
#> mclean2014a   <NA>
#> mclean2014b     10
```
