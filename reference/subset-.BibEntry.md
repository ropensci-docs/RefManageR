# Update Different Fields of Multiple Entries of a BibEntry Object

Assign new values for specified fields in a BibEntry object using a
named character vector or list of named character vectors.

## Usage

``` r
# S3 method for class 'BibEntry'
x[i, j, ...] <- value
```

## Arguments

- x:

  \- a BibEntry object.

- i:

  \- see
  [`[.BibEntry`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md)

- j:

  \- see
  [`[.BibEntry`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md)

- ...:

  \- see
  [`[.BibEntry`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md)

- value:

  \- values to be assigned to `x`. To update one entry only, should be a
  named character vector with names corresponding to fields. To update
  multiple entries, should be a list of named character vectors. Can
  also be an object of class BibEntry.

## Value

an object of class BibEntry.

## Details

Date and name list fields should be in the format expected by Biblatex
(see
[`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md)).

To clear a field ‘field_name’ from an entry use `field_name = ""`.

## See also

Other operators:
[`$.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/cash-.BibEntry.md),
`$<-.BibEntry()`,
[`+.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/merge.BibEntry.md),
[`[.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md),
[`[[.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/sub-sub-.BibEntry.md),
`[[<-.BibEntry()`,
[`c.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/c.BibEntry.md)

## Examples

``` r
bib.text <- "@Manual{mclean2014,
  author = {Mathew William McLean},
  title = {Straightforward Bibliography Management in R Using the RefManager Package},
  note = {arXiv: 1403.2036 [cs.DL]},
  year = {2014},
  url = {https://arxiv.org/abs/1403.2036},
}"
tfile <- tempfile(fileext = ".bib")
writeLines(bib.text, tfile)
bib <- ReadBib(tfile)
bib[1] <- list(c(date = "2014-03", key = "mwm2014"))
#> Error in eval(kal): object '*tmp*' not found
bib
#> [1] M. W. McLean. _Straightforward Bibliography Management in R Using
#> the RefManager Package_. arXiv: 1403.2036 [cs.DL]. 2014.
#> <https://arxiv.org/abs/1403.2036>.
unlink(tfile)

if (FALSE) { # \dontrun{
    file.name <- system.file("Bib", "RJC.bib", package="RefManageR")
    bib <- ReadBib(file.name)
    print(bib[seq_len(3L)], .opts = list(sorting = "none", bib.style = "alphabetic"))
    ## add month to Serban et al., add URL and urldate to Jennings et al., and
    ##   add DOI and correct journal to Garcia et al.
    bib[seq_len(3L)] <- list(c(date="2013-12"),
                            c(url="https://bsb.eurasipjournals.com/content/2013/1/13",
                              urldate = "2014-02-02"),
                            c(doi="10.1093/bioinformatics/btt608",
                              journal = "Bioinformatics"))
    print(bib[seq_len(3L)], .opts = list(sorting = "none", bib.style = "alphabetic"))
    bib2 <- bib[seq_len(3L)]
    bib2[2:3] <- bib[5:6]
    bib2
    bib2[3] <- c(journal='', eprinttype = "arxiv", eprint = "1308.5427",
      eprintclass = "math.ST", pubstate = "submitted", bibtype = "misc")
    bib2
} # }
```
