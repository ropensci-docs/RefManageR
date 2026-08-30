# Convert BibEntry objects to BibTeX or BibLaTeX

toBiblatex converts a BibEntry object to character vectors with BibLaTeX
markup. toBibtex will convert a BibEntry object to character vectors
with BibTeX markup, converting some BibLaTeX fields and all entry types
that are not supported by BibTeX to ones that are supported.

## Usage

``` r
toBiblatex(object, encoded.names.to.latex = TRUE, ...)

# S3 method for class 'BibEntry'
toBibtex(
  object,
  note.replace.field = c("urldate", "pubsate", "addendum"),
  extra.fields = NULL,
  encoded.names.to.latex = TRUE,
  ...
)
```

## Arguments

- object:

  an object of class BibEntry to be converted

- encoded.names.to.latex:

  if `TRUE` (the default) then name list fields such as ‘author’ and
  ‘editor’ will have non-ASCII characters translated to LaTeX escape
  sequences.

- ...:

  ignored

- note.replace.field:

  a character vector of BibLaTeX fields. When converting an entry to
  BibTeX, the first field in the entry that matches one specified in
  this vector will be added to the note field, *if* the note field is
  not already present

- extra.fields:

  character vector; fields that are not supported in standard BibTeX
  styles are by default dropped in the result return by the toBibtex
  function. Any fields specified in extra.fields will *not* be dropped
  if present in an entry.

## Value

an object of class “Bibtex” - character vectors where each element holds
one line of a BibTeX or BibLaTeX file

## Details

toBiblatex converts the BibEntry object to a vector containing the
corresponding BibLaTeX file, it ensures the name list fields (e.g.
author and editor) are formatted properly to be read by bibtex and biber
and otherwise prints all fields as is, thus it is similar to `toBibtex`.

toBibtex will attempt to convert BibLaTeX entries to a format that can
be read by bibtex. Any fields not supported by bibtex are dropped unless
they are specified in `extra.fields`. The fields below, if they are
present, are converted as described and added to a bibtex supported
field, unless that field is already present.

- date - The `date` field, if present will be truncated to a year and
  added to the `year` field, if it is not already present. If a month is
  specified with the date, it will be added to the `month` field.

- journaltitle - Will be changed to journal, if it is not already
  present

- location - Will be changed to address

- institution - Converted to `school` for thesis entries

- sortkey - Converted to `key`

- maintitle - Converted to `series`

- issuetitle - Converted to `booktitle`

- eventtitle - Converted to `booktitle`

- eprinttype - Converted to `archiveprefix` (for arXiv references)

- eprintclass - Converted to `primaryclass` (for arXiv references)

If no `note` field is present, the note.replace.field can be used to
specified BibLaTeX fields that can be looked for and added to the note
field if they are present.

BibLaTeX entry types that are not supported by bibtex are converted by
toBibtex as follows "mvbook" = "Book", "bookinbook" = "InBook",
"suppbook" = "InBook",

- MvBook,Collection,MvCollection,Reference,MvReference,Proceedings,MvProceedings,Periodical -
  to Book

- BookInBook,SuppBook,InReference,SuppPeriodical - to InBook

- report,patent - to TechReport

- SuppCollection - to InCollection

- thesis - to MastersThesis if `type = mathesis`, else to PhdThesis

- *rest* - to Misc

## See also

`toBibtex`,
[`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md),
[`print.BibEntry`](https://docs.ropensci.org/RefManageR/reference/print.BibEntry.md)

## Author

McLean, M. W. <mathew.w.mclean@gmail.com>, Andy Bunn for code for
translating non-ASCII characters to LaTeX.

## Examples

``` r
if (requireNamespace("bibtex")) {
    file.name <- system.file("Bib", "biblatexExamples.bib", package="RefManageR")
    bib <- suppressMessages(ReadBib(file.name))
    toBiblatex(bib[70:72])
    toBibtex(bib[70:72])
}
#> @inbook{kant:kpv,
#>   title = {Kritik der praktischen Vernunft},
#>   author = {Immanuel Kant},
#>   booktitle = {Kritik der praktischen Vernunft. Kritik der Urtheilskraft},
#>   volume = {5},
#>   publisher = {Walter de Gruyter},
#>   pages = {1-163},
#>   address = {Berlin},
#>   year = {1968},
#>   series = {Kants Werke. Akademie Textausgabe},
#> }
#> 
#> @inbook{kant:ku,
#>   title = {Kritik der Urtheilskraft},
#>   author = {Immanuel Kant},
#>   booktitle = {Kritik der praktischen Vernunft. Kritik der Urtheilskraft},
#>   volume = {5},
#>   publisher = {Walter de Gruyter},
#>   pages = {165-485},
#>   address = {Berlin},
#>   year = {1968},
#>   series = {Kants Werke. Akademie Textausgabe},
#> }
#> 
#> @inbook{nietzsche:historie,
#>   title = {Unzeitgem{\"a}sse Betrachtungen. Zweites St{\"u}ck},
#>   author = {Friedrich Nietzsche},
#>   booktitle = {Die Geburt der Trag{\"o}die. Unzeitgem{\"a}{\ss}e
#>                   Betrachtungen I--IV. Nachgelassene Schriften 1870--1973},
#>   editor = {Giorgio Colli and Mazzino Montinari},
#>   volume = {1},
#>   publisher = {dtv # { and Walter de Gruyter},
#>   pages = {243-334},
#>   address = {M{\"u}nchen and Berlin and New York},
#>   year = {1988},
#>   series = {S{\"a}mtliche Werke},
#> }
```
