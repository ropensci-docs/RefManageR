# Open BibEntry in PDF viewer or web browser.

Attempts to open a connection to an entry in a BibEntry object using
fields such as ‘file’, ‘DOI’, ‘eprint’ + ‘eprinttype’, and ‘URL’.

## Usage

``` r
# S3 method for class 'BibEntry'
open(
  con,
  entry = 1L,
  open.field = c("file", "url", "eprint", "doi"),
  viewer,
  ...
)
```

## Arguments

- con:

  BibEntry object to extract connections from.

- entry:

  numeric index or character key of entry in `bib` to open.

- open.field:

  character vector of fields to use in `bib` to open the BibEntry.
  Possible fields are any combination of “file”, “url”, “eprint”, or
  “doi”. “eprint” is implemented for `eprinttype=` “JSTOR”, “PubMed”, or
  “arXiv”. When multiple fields are specified, they are tried in the
  order they appear in the vector.

- viewer:

  character string giving the name of the program to be used as
  hypertext browser. It should be in the PATH, or a full path specified.
  Alternatively, an R function to be called to invoke the browser.
  Defaults to `getOptions("pdfviewer")` if `open.field = "file"` and
  `getOptions("browser")`, otherwise.

- ...:

  not used.

## See also

[`browseURL`](https://rdrr.io/r/utils/browseURL.html)

## Author

McLean, M. W. <mathew.w.mclean@gmail.com>

## Examples

``` r
if (FALSE) { # \dontrun{
if (requireNamespace("bibtex")) {
    testbib <- ReadBib(system.file("REFERENCES.bib", package="bibtex"))
    open(testbib)
    testbib$file <- file.path(R.home("doc/manual"), "R-intro.pdf")
    open(testbib)
}
} # }
```
