# Enhanced Bibliographic Entries

Provides a new class `BibEntry` which builds on
[`bibentry`](https://rdrr.io/r/utils/bibentry.html) to provide enhanced
functionality for representing, manipulating, importing, etc.
bibliographic information in BibTeX or BibLaTeX style.

## Usage

``` r
BibEntry(
  bibtype,
  textVersion = NULL,
  header = NULL,
  footer = NULL,
  key = NULL,
  ...,
  other = list(),
  mheader = NULL,
  mfooter = NULL
)
```

## Arguments

- bibtype:

  a character string with a BibTeX entry type. See Entry Types for
  details.

- textVersion:

  a character string with a text representation of the reference to
  optionally be employed for printing.

- header:

  a character string with optional header text.

- footer:

  a character string with optional footer text.

- key:

  a character string giving the citation key for the entry.

- ...:

  arguments of the form `tag = value` giving the fields of the entry,
  with `tag` and `value` the name and value of the field, respectively.
  Arguments with empty values are dropped. See Entry Fields for details.

- other:

  list; additional way to specify fields and their values

- mheader:

  string; optional “outer” header text

- mfooter:

  string; optional “outer” footer text

## Value

an object of class BibEntry

## Details

The BibEntry objects created by BibEntry can represent an arbitrary
positive number of references, as with `bibentry`, but many additional
methods are defined for building and manipulating a database of
references.

## Note

Date fields are parsed using the locale specified by
`Sys.getlocale("LC_TIME")` (relevant when specifying a character ‘month’
field, instead of the recommended integer format)

Name list fields (author, editor, etc.) should be specified as they
would be for BibTeX/BibLaTeX; e.g.
`author = "Doe, Jane and Smith, Bob A."`.

## Entry Types

bibentry creates "bibentry" objects, which are modeled after BibLaTeX
and BibTeX entries. The entry should be a valid BibLaTeX or BibTeX entry
type. For a list of valid BibTeX entry types, see
[`bibentry`](https://rdrr.io/r/utils/bibentry.html). BibLaTeX supports
all entry types from BibTeX for backwards compatibility. BibLaTeX
defines following entry types '

- *article* - An article in a journal, magazine, newspaper, or other
  periodical which forms a self-contained unit with its own title.
  Required fields: author, title, journal/journaltitle, year/date.

- *book* - A single-volume book with one or more authors where the
  authors share credit for the work as a whole. Required fields: author,
  title, year/date. (Also covers BibTeX @inbook).

- *mvbook* - A multi-volume *book*. For backwards compatibility,
  multi-volume books are also supported by the entry type @book.
  Required fields: author, title, year/date.

- *inbook* - A part of a book which forms a self-contained unit with its
  own title. Note that the profile of this entry type is different from
  standard BibTeX. Required fields: author, title, booktitle, year/date

- *bookinbook* This type is similar to *inbook* but intended for works
  originally published as a stand-alone book.

- *suppbook* - Supplemental material in a *book*. This type is closely
  related to the *inbook* entry type.

- *booklet* - A book-like work without a formal publisher or sponsoring
  institution. Required fields: author/editor, title, year/date.

- *collection* - A single-volume collection with multiple,
  self-contained contributions by distinct authors which have their own
  title. Required fields: editor, title, year/date.

- *mvcollection* - A multi-volume *collection*. Also supported by
  *collection*. Required fields: editor, title, year/date.

- *incollection* - A contribution to a collection which forms a
  self-contained unit with a distinct author and title. Required fields:
  author, editor, title, booktitle, year/date.

- *suppcollection* - Supplemental material in a *collection*.

- *manual* - Technical or other documentation, not necessarily in
  printed form. Required fields: author/editor, title, year/date

- *misc* - A fallback type for entries which do not fit into any other
  category. Required fields: author/editor, title, year/date

- *online* - An online resource. Required fields: author, title, number,
  year/date.

- *patent* - A patent or patent request. Required fields: author, title,
  number, year/date.

- *periodical* - A complete issue of a periodical, such as a special
  issue of a journal. Required fields: editor, title, year/date

- *suppperiodical* - Supplemental material in a *periodical*.

- *proceedings* - A single-volume conference proceedings. Required
  fields: editor, title, year/date.

- *mvproceedings* - A multi-volume @proceedings entry. Required fields:
  editor, title, year/date.

- *inproceedings* - An article in a conference proceedings. Required
  fields: author, editor, title, booktitle, year/date.

- *reference* - A single-volume work of reference such as an
  encyclopedia or a dictionary. Alias for *collection* in standard
  styles.

- *mvreference* - A multi-volume *reference* entry.

- *inreference* - An article in a work of reference. Alias for
  *incollection* in most styles.

- *report* - A technical report, research report, or white paper
  published by a university or some other institution. Required fields:
  author, title, type, institution, year/date.

- *set* - An entry set. This entry type is special, see BibLaTeX manual.

- *thesis* - A thesis written for an educational institution to satisfy
  the requirements for a degree. Use the type field to specify the type
  of thesis. Required fields: author, title, type, institution,
  year/date.

- *unpublished* A work with an author and a title which has not been
  formally published, such as a manuscript or the script of a talk.
  Required fields: author, title, year/date.

- *xdata* - This entry type is special. *xdata* entries hold data which
  may be inherited by other entries. (Biber only.)

- *custom\[a-f\]* Custom types (up to five) for special bibliography
  styles. Not used by the standard styles.

## References

BibLaTeX manual
<http://mirrors.ibiblio.org/CTAN/macros/latex/contrib/biblatex/doc/biblatex.pdf>

## See also

[`bibentry`](https://rdrr.io/r/utils/bibentry.html)

## Author

McLean, M. W. <mathew.w.mclean@gmail.com>

## Examples

``` r
BibEntry(bibtype = "Article", key = "mclean2014", title = "An Article Title",
  author = "McLean, Mathew W. and Wand, Matt P.", journaltitle = "The Journal Title",
  date = "2014-02-06", pubstate = "forthcoming")
#> [1] M. W. McLean and M. P. Wand. “An Article Title”. In: _The Journal
#> Title_ (Feb. 06, 2014). Forthcoming.
bib <- BibEntry(bibtype = "XData", key = "arxiv_data", eprinttype = "arxiv",
eprintclass = "stat.ME", year = 2013, urldate = "2014-02-01", pubstate = "submitted")
bib <- c(bib, BibEntry(bibtype = "Misc", key = "mclean2014b",
  title = "Something On the {arXiv}", author = "Mathew W. McLean", eprint = "1312.9999",
  xdata = "arxiv_data", url = "https://arxiv.org/abs/1310.5811"))
bib
#> XData: arxiv_data
#> 
#> [1] M. W. McLean. _Something On the arXiv_. 2013. arXiv: 1312.9999
#> [stat.ME]. <https://arxiv.org/abs/1310.5811> (visited on 02/01/2014).
#> Submitted.
toBiblatex(bib)
#> @XData{arxiv_data,
#>   eprinttype = {arxiv},
#>   eprintclass = {stat.ME},
#>   year = {2013},
#>   urldate = {2014-02-01},
#>   pubstate = {submitted},
#> }
#> 
#> @Misc{mclean2014b,
#>   title = {Something On the {arXiv}},
#>   author = {Mathew W. McLean},
#>   eprint = {1312.9999},
#>   xdata = {arxiv_data},
#>   url = {https://arxiv.org/abs/1310.5811},
#> }
```
