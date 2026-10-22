# Cite a BibEntry object in text and print all citations

The `Cite` functions allow for citing a `BibEntry` object in text. The
`PrintBibliography` function allows for printing the bibliography of all
the cited entries. The `NoCite` function adds references to the
bibliography without including a citation. These functions are most
useful when used in, e.g., a RMarkdown or RHTML document.

## Usage

``` r
Cite(bib, ..., textual = FALSE, before = NULL, after = NULL, .opts = list())

PrintBibliography(bib, .opts = list(), start = 1, end = length(bib))

Citep(bib, ..., before = NULL, after = NULL, .opts = list())

AutoCite(bib, ..., before = NULL, after = NULL, .opts = list())

Citet(bib, ..., before = NULL, after = NULL, .opts = list())

TextCite(bib, ..., before = NULL, after = NULL, .opts = list())

NoCite(bib, ..., .opts = list())
```

## Arguments

- bib:

  a `BibEntry` or `bibentry` object

- ...:

  passed to
  [`SearchBib`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md)
  for indexing into bib. A character vector of keys, for example.

- textual:

  logical; if TRUE, a “textual” citation is produced, i.e. what is
  produced by \citet in `natbib` and \textcite in `BibLaTeX`; otherwise,
  a parenthetical citation as \citep and \autocite.

- before:

  string; optional text to display before the citation.

- after:

  string; optional text to display after the citation.

- .opts:

  list; See the relevant section in
  [`BibOptions`](https://docs.ropensci.org/RefManageR/reference/BibOptions.md)
  for a description of all valid options for these functions.

- start:

  Integer; specifying the index of the first citation to print. Useful
  for printing long bibliographies on multiple pages/slides.

- end:

  Integer; specifying the index of the last citation to print. Useful
  for printing long bibliographies on multiple pages/slides.

## Value

For the cite functions: a character string containing the citation

PrintBibliography: The formatted list of references.

NoCite: no return value; invoked for its side-effect.

## Details

See the package vignettes and execute the examples below.

If `bib.style = "alphabetic"` or `bib.style = "numeric"`, then sorting
needs to be done at the start of the document prior to using a cite
function as sorting is not done by the `PrintBibliography` function for
those styles (specifying `sorting` in `.opts` is ignored in this case).
If no sorting is done, the references are listed in the order they were
cited in for those two styles.

If the `...` argument to NoCite is identical to “\*”, then all
references in `bib` are added to the bibliography without citations.

## See also

[`print.BibEntry`](https://docs.ropensci.org/RefManageR/reference/print.BibEntry.md),
[`BibOptions`](https://docs.ropensci.org/RefManageR/reference/BibOptions.md),
[`citeNatbib`](https://rdrr.io/r/utils/cite.html), the package vignettes
bib \<-

## Examples

``` r
if (requireNamespace("bibtex")) {
    file <- system.file("Bib", "biblatexExamples.bib", package = "RefManageR")
    BibOptions(check.entries = FALSE)
    bib <- ReadBib(file)
    Citet(bib, 12)
    NoCite(bib, title = "Alkanethiolate")
    PrintBibliography(bib, .opts = list(style = "latex",
                      bib.style = "authoryear"))
}
#> Herrmann, W. A., K. Öfele, S. K. Schneider, et al.
#> (2006).
#> ``A carbocyclic carbene as an efficient catalyst ligand for C--C
#> coupling reactions''.
#> In: \emph{Angew.\textasciitilde{}Chem. Int.\textasciitilde{}Ed.} 45.23, pp. 3859-3862.
#> 
#> Hostetler, M. J., J. E. Wingate, C. Zhong, et al.
#> (1998).
#> ``Alkanethiolate gold cluster molecules with core diameters from
#> 1.5 to 5.2\textasciitilde{}nm''.
#> In: \emph{Langmuir} 14.1, pp. 17-30.
if (FALSE) { # \dontrun{
  if (requireNamespace("bibtex")){
    Citep(bib, c("loh", "geer"), .opts = list(cite.style = "numeric"),
          before = "see e.g., ")
    Citet(bib, "loh", .opts = list(cite.style = "numeric", super = TRUE))
    AutoCite(bib, eprinttype = "arxiv", .opts = list(cite.style = "authoryear"))
    AutoCite(bib, eprinttype = "arxiv", .opts = list(cite.style = "pandoc"))
    Citep(bib, author = "kant")
    ## shorthand field in both entries gets used for numeric and alphabetic labels
    TextCite(bib, author = "kant", .opts = list(cite.style = "alphabetic"))
    TextCite(bib, author = "kant", .opts = list(cite.style = "numeric"))
    TextCite(bib, author = "kant", .opts = list(cite.style = "alphabetic",
             style = "html"))
    punct <- unlist(BibOptions("bibpunct"))
    punct[3:4] <- c("(", ")")
    TextCite(bib, 33, .opts = list(bibpunct = punct, cite.style = "alphabetic"))

    BibOptions(restore.defaults = TRUE)
  }
} # }
if (FALSE) { # \dontrun{
library(knitr)
## See also TestNumeric.Rmd and TestAlphabetic.Rmd for more examples
old.dir <- setwd(tdir <- tempdir())
doc <- system.file("Rmd", "TestRmd.Rmd", package = "RefManageR")
file.show(doc)
tmpfile <- tempfile(fileext = ".html", tmpdir = tdir)
knit2html(doc, tmpfile)
browseURL(tmpfile)

doc <- system.file("Rhtml", "TestAuthorYear.Rhtml", package = "RefManageR")
file.show(doc)
tmpfile <- tempfile(fileext = ".html", tmpdir = tdir)
knit2html(doc, tmpfile)
browseURL(tmpfile)
setwd(old.dir)
unlink(tdir)
} # }
```
