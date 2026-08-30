# Create a BibTeX File from a BibEntry Object e Creates a Bibtex File from a BibEntry object for use with either BibTeX or BibLaTex.

Create a BibTeX File from a BibEntry Object e Creates a Bibtex File from
a BibEntry object for use with either BibTeX or BibLaTex.

## Usage

``` r
WriteBib(
  bib,
  file = "references.bib",
  biblatex = TRUE,
  append = FALSE,
  verbose = TRUE,
  ...
)
```

## Arguments

- bib:

  a BibEntry object to be written to file

- file:

  character string naming a file, should; end in “.bib”. Can be `NULL`,
  in which case the BibEntry object will be written to
  [`stdout`](https://rdrr.io/r/base/showConnections.html).

- biblatex:

  boolean; if `TRUE`,
  [`toBiblatex`](https://docs.ropensci.org/RefManageR/reference/toBiblatex.md)
  is used and no conversions of the BibEntry object are done; if `FALSE`
  entries will be converted as described in
  [`toBibtex.BibEntry`](https://docs.ropensci.org/RefManageR/reference/toBiblatex.md).

- append:

  as in `write.bib` in package `bibtex`

- verbose:

  as in `write.bib` in package `bibtex`

- ...:

  additional arguments passed to
  [`writeLines`](https://rdrr.io/r/base/writeLines.html)

## Value

`bib` - invisibly

## Note

To write the contents of `bib` “as is”, the argument `biblatex` should
be `TRUE`, otherwise conversion is done as in
[`toBibtex.BibEntry`](https://docs.ropensci.org/RefManageR/reference/toBiblatex.md).

## See also

`write.bib` in package `bibtex`,
[`ReadBib`](https://docs.ropensci.org/RefManageR/reference/ReadBib.md),
[`toBibtex.BibEntry`](https://docs.ropensci.org/RefManageR/reference/toBiblatex.md),
[`toBiblatex`](https://docs.ropensci.org/RefManageR/reference/toBiblatex.md),
[`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md)

## Author

McLean, M. W. based on `write.bib` by Gaujoux, R. in package `bibtex`.

## Examples

``` r
if (requireNamespace("bibtex")){
    bib <- BibEntry("Article", key = "Carroll_2012",
                    doi = "10.1080/01621459.2012.699793",
                    year = "2012", month = "sep",
                    volume = 107, number = 499,
                    pages = {1166--1177},
      author = "R. Carroll and A. Delaigle and P. Hall",
      title = "Deconvolution When Classifying Noisy Data ...",
      journal = "Journal of the American Statistical Association")

  ## Write bib if no server error and bibtex available
  if (length(bib)){
    tfile <- tempfile(fileext = ".bib")
    WriteBib(bib, tfile, biblatex = TRUE)
    identical(ReadBib(tfile), bib)
    unlink(tfile)
  }
}
#> Writing 1 Bibtex entries ... 
#> OK
#> Results written to file ‘/tmp/RtmpANbFg5/file5b51e7a7854.bib’
```
