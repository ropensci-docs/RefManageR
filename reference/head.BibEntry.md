# Return the first or last part of a BibEntry object

Prints the first or last entries of a BibEntry object (via
[`message`](https://rdrr.io/r/base/message.html)) and returns them
*invisibly* (via [`invisible`](https://rdrr.io/r/base/invisible.html)).

## Usage

``` r
# S3 method for class 'BibEntry'
head(x, n = 6L, suppress.messages = TRUE, ...)

# S3 method for class 'BibEntry'
tail(x, n = 6L, suppress.messages = TRUE, ...)
```

## Arguments

- x:

  an object of class BibEntry.

- n:

  a single integer. If positive, size for the resulting object: number
  of elements for a vector (including lists), rows for a matrix or data
  frame or lines for a function. If negative, all but the n last/first
  number of elements of x.

- suppress.messages:

  boolean; should the head/tail entries be printed via
  [`message`](https://rdrr.io/r/base/message.html)?

- ...:

  arguments to be passed to or from other methods.

## Value

an object of class BibEntry.

## Details

If `suppress.messages` is `FALSE`, the head/tail entries are output to
the console along with some additional formatting for the ‘bibtype’ and
‘key’, in addition to invisibly returning the entries.

## Examples

``` r
if (requireNamespace("bibtex")) {
    file <- system.file("Bib", "biblatexExamples.bib", package = "RefManageR")
    BibOptions(check.entries = FALSE)
    bib <- ReadBib(file)
    tail(bib, 2, suppress.messages = FALSE)
    bib <- head(bib, 1, suppress.messages = TRUE)
}
#> [[91]] Thesis: geer
#> [1] I. de Geer. “Earl, Saint, Bishop, Skald~- and Music. The Orkney
#> Earldom of the Twelfth Century. A Musicological Study”. PhD thesis.
#> Uppsala: Uppsala Universitet, 1985.
#> 
#> [[92]] Thesis: loh
#> [1] N. C. Loh. “High-Resolution Micromachined Interferometric
#> Accelerometer”. MA Thesis. Cambridge, Mass.: Massachusetts Institute of
#> Technology, 1992.
```
