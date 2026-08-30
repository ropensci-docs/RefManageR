# Import book and article references from a public Google Scholar profile by ID.

This function will create a BibEntry object for up to 100 references
from a provided Google Scholar ID, if the profile is public. The number
of citations for each entry will also be imported.

## Usage

``` r
ReadGS(
  scholar.id,
  start = 0,
  limit = 100,
  sort.by.date = FALSE,
  .Encoding = "UTF-8",
  check.entries = BibOptions()$check.entries
)
```

## Arguments

- scholar.id:

  character; the Google Scholar ID from which citations will be
  imported. The ID can by found by visiting an author's Google Scholar
  profile and noting the value in the uri for the “user” parameter.

- start:

  numeric; index of first citation to include.

- limit:

  numeric; maximum number of results to return. Cannot exceed 100.

- sort.by.date:

  boolean; if true, newest citations are imported first; otherwise, most
  cited works are imported first.

- .Encoding:

  character; text encoding to use for importing the results and creating
  the bib entries.

- check.entries:

  What should be done with incomplete entries (those containing “...”
  due to long fields)? Either `FALSE` to add them anyway, `"warn"` to
  add with a warning, or any other value to drop the entry with a
  message and continue processing the remaining entries.

## Value

An object of class BibEntry. If the entry has any citations, the number
of citations is stored in a field ‘cites’.

## Details

This function creates `BibTeX` entries from an author's Google Scholar
page. If the function finds numbers corresponding to volume/number/pages
of a journal article, an ‘Article’ entry is created. If an arXiv
identifier is found, a ‘Misc’ entry is created with `eprint`,
`eprinttype`, and `url` fields. Otherwise, a ‘TechReport’ entry is
created; unless the entry has more than ten citations, in which case a
‘Book’ entry is created.

Long author lists, long titles, and long journal/publisher names can all
lead to these fields being incomplete for a particular entry. When this
occurs, these entries are either dropped or added with a warning
depending on the value of the `check.entries` argument.

## Note

Read Google's Terms of Service before using.

It is not possible to automatically import BibTeX entries directly from
Google Scholar as no API is available and this violates their Terms of
Service.

## See also

[`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md)

## Examples

``` r
if (interactive() && !httr::http_error("https://scholar.google.com")){
  ## R. J. Carroll's ten newest publications
  ReadGS(scholar.id = "CJOHNoQAAAAJ", limit = 10, sort.by.date = TRUE)

  ## Matthias Katzfu\ss
  BibOptions(check.entries = "warn")
  kat.bib <- ReadGS(scholar.id = "vqW0UqUAAAAJ")

  ## retrieve GS citation counts stored in field 'cites'
  kat.bib$cites
}
```
