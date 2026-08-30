# Sort a BibEntry Object

Sorts a `BibEntry` object by specified fields. The possible fields used
for sorting and the order they are used in correspond with the options
available in BibLaTeX.

## Usage

``` r
# S3 method for class 'BibEntry'
sort(
  x,
  decreasing = FALSE,
  sorting = BibOptions()$sorting,
  .bibstyle = BibOptions()$bib.style,
  ...
)
```

## Arguments

- x:

  an object of class BibEntry

- decreasing:

  logical; should the sort be increasing or decreasing?

- sorting:

  sort method to use, see **Details**.

- .bibstyle:

  bibliography style; used when `sort` is called by
  [`print.BibEntry`](https://docs.ropensci.org/RefManageR/reference/print.BibEntry.md)

- ...:

  internal use only

## Value

the sorted BibEntry object

## Details

The possible values for argument `sorting` are

- nty - sort by name, then by title, then by year

- nyt - sort by name, then by year, then title

- nyvt - sort by name, year, volume, title

- anyt - sort by alphabetic label, name, year, title

- anyvt - sort by alphabetic label, name, year, volume, title

- ynt - sort by year, name, title

- ydnt - sort by year (descending), name, title

- debug - sort by keys

- none - no sorting is performed

All sorting methods first consider the field presort, if available.
Entries with no presort field are assigned presort value “mm”. Next the
sortkey field is used.

When sorting by name, the sortname field is used first. If it is not
present, the author field is used, if that is not present editor is
used, and if that is not present translator is used. All of these fields
are affected by the value of `max.names` in .BibOptions()\$max.names.

When sorting by title, first the field sorttitle is considered.
Similarly, when sorting by year, the field sortyear is first considered.

When sorting by volume, if the field is present it is padded to four
digits with leading zeros; otherwise, the string “0000” is used.

When sorting by alphabetic label, the labels that would be generating
with the “alphabetic” bibstyle are used. First the shorthand field is
considered, then label, then shortauthor, shorteditor, author, editor,
and translator. Refer to the BibLaTeX manual Sections 3.1.2.1 and 3.5
and Appendix C.2 for more information.

## References

Lehman, Philipp and Kime, Philip and Boruvka, Audrey and Wright, J.
(2013). The biblatex Package.
<http://mirrors.ibiblio.org/CTAN/macros/latex/contrib/biblatex/doc/biblatex.pdf>.

## See also

[`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md),
[`print.BibEntry`](https://docs.ropensci.org/RefManageR/reference/print.BibEntry.md),
[`order`](https://rdrr.io/r/base/order.html)

## Examples

``` r
if (requireNamespace("bibtex")) {
    file.name <- system.file("Bib", "biblatexExamples.bib", package="RefManageR")
    bib <- suppressMessages(ReadBib(file.name)[[70:73]])
    BibOptions(sorting = "none")
    bib
    sort(bib, sorting = "nyt")
    sort(bib, sorting = "ynt")
    BibOptions(restore.defaults = TRUE)
}
```
