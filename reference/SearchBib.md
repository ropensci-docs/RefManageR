# Search BibEntry objects by field

Allows for searching and indexing a BibEntry object by fields, including
names and dates. The extraction operator and the `SearchBib` function
simply provide different interfaces to the same search functionality.

## Usage

``` r
# S3 method for class 'BibEntry'
x[i, j, ..., drop = FALSE]

SearchBib(x, .opts = list(), ...)
```

## Arguments

- x:

  an object of class BibEntry

- i:

  A named list or character vector of search terms with names
  corresponding to the field to search for the search term.
  Alternatively, a vector of entry key values or numeric or logical
  indices specifying which entries to extract.

- j:

  A named list or character vector, as `i`. Entries matching the search
  specified by i *OR* matching the query specified by `j` will be return

- ...:

  arguments in the form `bib.field = search.term`, or as `j` list*s* or
  character vector*s* for additional searches. For `SearchBib`, can
  alternatively have same form as `i`.

- drop:

  logical, should attributes besides class be dropped from result?

- .opts:

  list of search options with `name = value` entries. Any option
  described in
  [`BibOptions`](https://docs.ropensci.org/RefManageR/reference/BibOptions.md)
  is valid, with the following being the most relevant ones

  - `use.regex` - logical; are the search terms regular expressions or
    should exact matching be used?

  - `ignore.case` - logical; should case be ignored when comparing
    strings?

  - `match.date` - how should the date fields date, urldate, eventdate,
    and origdate. Default is “year.only”, so that months and days in
    dates are ignored when comparing. Currently, specifying any other
    value results the full date being used. See the Note section.

  - `match.author` - character string; how should name fields be
    searched? If “family.only”, only family names are compared; if
    “family.with.initials”, family name and given name initials are
    used; if “exact”, full names are used.

  - `return.ind` - logical; if TRUE the returned object is numeric
    indices of match locations; otherwise, a BibEntry object is returned

## Value

an object of class BibEntry (the results of the search/indexing), *or*
if `BibOptions()$return.ind=TRUE`, the indices in `x` that match the
search terms.

## Note

The arguments to the SearchBib function that control certain search
features can also be changed for the extraction operator by changing the
corresponding option in the .BibOptions object; see
[`BibOptions`](https://docs.ropensci.org/RefManageR/reference/BibOptions.md).

## See also

Other operators:
[`$.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/cash-.BibEntry.md),
`$<-.BibEntry()`,
[`+.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/merge.BibEntry.md),
`[<-.BibEntry()`,
[`[[.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/sub-sub-.BibEntry.md),
`[[<-.BibEntry()`,
[`c.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/c.BibEntry.md)

## Examples

``` r
file.name <- system.file("Bib", "biblatexExamples.bib", package="RefManageR")
bib <- suppressMessages(ReadBib(file.name))

## author search, default is to use family names only for matching
bib[author = "aristotle"]
#> [1] Aristotle. _De Anima_. Ed. by R. D. Hicks. Cambridge: Cambridge
#> University Press, 1907.
#> 
#> [2] Aristotle. _Physics_. Trans.  by P. H. Wicksteed and F. M.
#> Cornford. New York: G. P. Putnam, 1929.
#> 
#> [3] Aristotle. _Poetics_. Ed. by D. W. Lucas. Clarendon Aristotle.
#> Oxford: Clarendon Press, 1968.
#> 
#> [4] Aristotle. _The Rhetoric of Aristotle with a commentary by the late
#> Edward Meredith Cope_. Ed. by E. M. Cope. With a comment. by E. M.
#> Cope. Vol. 3. 3 vols. Cambridge University Press, 1877.

## Aristotle references before 1925
bib[author="aristotle", date = "/1925"]
#> [1] Aristotle. _De Anima_. Ed. by R. D. Hicks. Cambridge: Cambridge
#> University Press, 1907.
#> 
#> [2] Aristotle. _The Rhetoric of Aristotle with a commentary by the late
#> Edward Meredith Cope_. Ed. by E. M. Cope. With a comment. by E. M.
#> Cope. Vol. 3. 3 vols. Cambridge University Press, 1877.

## Aristotle references before 1925 *OR* references with editor Westfahl
bib[list(author="aristotle", date = "/1925"),list(editor = "westfahl")]
#> [1] Aristotle. _De Anima_. Ed. by R. D. Hicks. Cambridge: Cambridge
#> University Press, 1907.
#> 
#> [2] Aristotle. _The Rhetoric of Aristotle with a commentary by the late
#> Edward Meredith Cope_. Ed. by E. M. Cope. With a comment. by E. M.
#> Cope. Vol. 3. 3 vols. Cambridge University Press, 1877.
#> 
#> [3] G. Westfahl, ed. _Space and Beyond. The Frontier Theme in Science
#> Fiction_. Westport, Conn. and London: Greenwood, 2000.
#> 
#> [4] G. Westfahl. “The True Frontier. Confronting and Avoiding the
#> Realities of Space in American Science Fiction Films”. In: _Space and
#> Beyond. The Frontier Theme in Science Fiction_. Ed. by G. Westfahl.
#> Westport, Conn. and London: Greenwood, 2000, pp. 55-65.

## Change some searching and printing options and search for author
old.opts <- BibOptions(bib.style = "authoryear", match.author = "exact",
                       max.names = 99, first.inits = FALSE)
bib[author="Mart\u00edn, Jacinto and S\u00e1nchez, Alberto"]
#> Almendro, José L., Jacinto Martín, Alberto Sánchez, and Fernando Nozal
#> (1998). “Elektromagnetisches Signalhorn”. EU-29702195U (countryfr and
#> countryuk and countryde).
BibOptions(old.opts)  ## reset options

if (FALSE) { # \dontrun{
  ## Some works of Raymond J. Carroll's
  file.name <- system.file("Bib", "RJC.bib", package="RefManageR")
  bib <- ReadBib(file.name)
  length(bib)

  ## index by key
  bib[c("chen2013using", "carroll1978distributions")]

  ## Papers with someone with family name Wang
  length(SearchBib(bib, author='Wang', .opts = list(match.author = "family")))

  ## Papers with Wang, N.
  length(SearchBib(bib, author='Wang, N.', .opts = list(match.author = "family.with.initials")))

  ## tech reports with Ruppert
  length(bib[author='ruppert',bibtype="report"])

  ##Carroll and Ruppert tech reports at UNC
  length(bib[author='ruppert',bibtype="report",institution="north carolina"])

  ## Carroll and Ruppert papers since leaving UNC
  length(SearchBib(bib, author='ruppert', date="1987-07/",
                   .opts = list(match.date = "exact")))

  ## Carroll and Ruppert papers NOT in the 1990's
 length(SearchBib(bib, author='ruppert', date = "!1990/1999"))
 identical(SearchBib(bib, author='ruppert', date = "!1990/1999"),
          SearchBib(bib, author='ruppert', year = "!1990/1999"))
 table(unlist(SearchBib(bib, author='ruppert', date="!1990/1999")$year))

 ## Carroll + Ruppert + Simpson
 length(bib[author="Carroll, R. J. and Simpson, D. G. and Ruppert, D."])

 ## Carroll + Ruppert OR Carroll + Simpson
 length(bib[author=c("Carroll, R. J. and Ruppert, D.", "Carroll, R. J. and Simpson, D. G.")])

 ## Carroll + Ruppert tech reports at UNC "OR" Carroll and Ruppert JASA papers
 length(bib[list(author='ruppert',bibtype="report",institution="north carolina"),
            list(author="ruppert",journal="journal of the american statistical association")])
} # }
```
