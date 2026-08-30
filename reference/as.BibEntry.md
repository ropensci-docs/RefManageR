# Coerce to a BibEntry object

Functions to check if an object is a BibEntry, or coerce it if possible.

## Usage

``` r
as.BibEntry(x)

is.BibEntry(x)
```

## Arguments

- x:

  any `R` object.

## Value

`as.BibEntry` - if successful, an object of class BibEntry.

`is.BibEntry` - logical; `TRUE` if `x` is a BibEntry object.

## Details

`as.BibEntry` is able to coerce suitably formatted character vectors,
[`bibentry`](https://rdrr.io/r/utils/bibentry.html) objects, lists, and
data.frames to BibEntry objects. See the examples.

## Note

Each entry to be coerced should have a bibtype, key, and all required
fields for the specified bibtype.

## See also

[`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md)

## Examples

``` r
if (requireNamespace("bibtex")) {
    file.name <- system.file("Bib", "biblatexExamples.bib", package="RefManageR")
    bib <- suppressMessages(ReadBib(file.name))[[20:21]]
    identical(as.BibEntry(unlist(bib)), bib)  ## see also RelistBibEntry

    identical(as.BibEntry(unclass(bib)), bib)

    identical(as.BibEntry(as.data.frame(bib)), bib)
 }
#> [1] TRUE

bib <- c(bibtype = "article", key = "mclean2014", title = "My New Article",
  author = "Mathew W. McLean", journaltitle = "The Journal", date = "2014-01")
as.BibEntry(bib)
#> [1] M. W. McLean. “My New Article”. In: _The Journal_ (Jan. 2014).

bib <- bibentry(bibtype = "article", key = "mclean2014", title = "My New Article",
journal = "The Journal", year = 2014, author = "Mathew W. McLean")
print(bib, .bibstyle = "JSS")
#> McLean MW (2014). “My New Article.” _The Journal_.
as.BibEntry(bib)
#> [1] M. W. McLean. “My New Article”. In: _The Journal_ (2014).

bib <- list(c(bibtype = "article", key = "mclean2014a", title = "My New Article",
  author = "Mathew W. McLean", journaltitle = "The Journal", date = "2014-01"),
  c(bibtype = "article", key = "mclean2014b", title = "Newer Article",
  author = "Mathew W. McLean", journaltitle = "The Journal", date = "2014-02"))
as.BibEntry(bib)
#> [1] M. W. McLean. “My New Article”. In: _The Journal_ (Jan. 2014).
#> 
#> [2] M. W. McLean. “Newer Article”. In: _The Journal_ (Feb. 2014).
```
