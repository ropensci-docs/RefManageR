# BibLaTeX/BibTeX .bib file parser

Parser for bibliography databases in the bib format containing either
BibLaTeX or BibTeX entries.

## Usage

``` r
ReadBib(
  file,
  .Encoding = "UTF-8",
  header = if (length(preamble)) paste(preamble, sep = "\n") else "",
  footer = "",
  check = BibOptions()$check.entries
)
```

## Arguments

- file:

  string; bib file to parse.

- .Encoding:

  encoding

- header:

  header of the citation list. By default this is made from the Preamble
  entries found in the bib file.

- footer:

  footer of the citation list.

- check:

  “error”, “warn”, or logical `FALSE`. What action should be taken if an
  entry is missing required fields? `FALSE` means no checking is done,
  “warn” means entry is added with an error. “error” means the entry
  will not be added. See
  [`BibOptions`](https://docs.ropensci.org/RefManageR/reference/BibOptions.md).

## Note

Date fields are parsed using the locale specified by
`Sys.getlocale("LC_TIME")`. To read a bib file with character ‘month’
fields in a language other than the current locale, `Sys.setlocale`
should be used to change ‘LC_TIME’\` to match the bib file before
calling `ReadBib`.

Keys will be made unique by calling
[`make.unique`](https://rdrr.io/r/base/make.unique.html) with
`sep = ":"`.

## See also

[`read.bib`](https://docs.ropensci.org/bibtex/reference/read.bib.html)
in package `bibtex`

## Author

McLean, M. W., based on code in `bibtex` package by Francois, R.

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
ReadBib(tfile)
#> [1] M. W. McLean. _Straightforward Bibliography Management in R Using
#> the RefManager Package_. arXiv: 1403.2036 [cs.DL]. 2014.
#> <https://arxiv.org/abs/1403.2036>.
unlink(tfile)
if (FALSE) { # \dontrun{
    file.name <- system.file("Bib", "RJC.bib", package="RefManageR")
    bib <- ReadBib(file.name)
} # }
```
