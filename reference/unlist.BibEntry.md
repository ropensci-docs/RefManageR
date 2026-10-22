# Flatten and unflatten BibEntry objects

`RelistBibEntry` unflattens a BibEntry object that has been flattened
with `unlist`.

`unlist` flattens a BibEntry object to a single list where every field
(including `bibtype` and `key`) of every entry is a separate element in
the list.

## Usage

``` r
RelistBibEntry(flesh, skeleton = NULL)

# S3 method for class 'BibEntry'
unlist(x, recursive = FALSE, use.names = TRUE)
```

## Arguments

- flesh:

  list; an `unlist`ed BibEntry object

- skeleton:

  currently ignored

- x:

  a BibEntry object to flatten

- recursive:

  ignored.

- use.names:

  ignored.

## Value

`RelistBibEntry` - an object of class BibEntry

For `unlist`, a list with bib entries collapsed into a single list.

## Details

`RelistBibEntry` is only intended for use with `unlist`ed BibEntry
objects.

## Note

The names of the list elements from an unlisted BibEntry object will not
be unique. To do this see
[`make.unique`](https://rdrr.io/r/base/make.unique.html).

## See also

[`as.BibEntry`](https://docs.ropensci.org/RefManageR/reference/as.BibEntry.md)

## Examples

``` r
bib <- list(c(bibtype = "article", key = "mclean2014a", title = "My New Article",
  author = "Mathew W. McLean", journaltitle = "The Journal", date = "2014-01"),
  c(bibtype = "article", key = "mclean2014b", title = "My Newer Article",
  author = "Mathew W. McLean", journaltitle = "The Journal", date = "2014-02"))
bib <- as.BibEntry(bib)
unlist(bib)
#> $title
#> [1] "My New Article"
#> 
#> $author
#> [1] "Mathew W. McLean"
#> 
#> $journaltitle
#> [1] "The Journal"
#> 
#> $date
#> [1] "2014-01"
#> 
#> $bibtype
#> [1] "Article"
#> 
#> $dateobj
#> [1] "2014-01-01 UTC"
#> 
#> $key
#> [1] "mclean2014a"
#> 
#> $title
#> [1] "My Newer Article"
#> 
#> $author
#> [1] "Mathew W. McLean"
#> 
#> $journaltitle
#> [1] "The Journal"
#> 
#> $date
#> [1] "2014-02"
#> 
#> $bibtype
#> [1] "Article"
#> 
#> $dateobj
#> [1] "2014-02-01 UTC"
#> 
#> $key
#> [1] "mclean2014b"
#> 
RelistBibEntry(unlist(bib))
#> [1] M. W. McLean. “My New Article”. In: _The Journal_ (Jan. 2014).
#> 
#> [2] M. W. McLean. “My Newer Article”. In: _The Journal_ (Feb. 2014).
```
