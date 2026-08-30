# RefManageR: Straightforward 'BibTeX' and 'BibLaTeX' Bibliography Management

Provides tools for importing and working with bibliographic references.
It greatly enhances the 'bibentry' class by providing a class 'BibEntry'
which stores 'BibTeX' and 'BibLaTeX' references, supports 'UTF-8'
encoding, and can be easily searched by any field, by date ranges, and
by various formats for name lists (author by last names, translator by
full names, etc.). Entries can be updated, combined, sorted, printed in
a number of styles, and exported. 'BibTeX' and 'BibLaTeX' '.bib' files
can be read into 'R' and converted to 'BibEntry' objects. Interfaces to
'NCBI Entrez', 'CrossRef', and 'Zotero' are provided for importing
references and references can be created from locally stored 'PDF' files
using 'Poppler'. Includes functions for citing and generating a
bibliography with hyperlinks for documents prepared with 'RMarkdown' or
'RHTML'.

## Details

**Importing and Creating References**

BibEntry objects can be created directly using the
[`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md)
function. `.bib` files can be read into R using the
[`ReadBib`](https://docs.ropensci.org/RefManageR/reference/ReadBib.md)
function. Tools are provided for importing references from Crossref,
Zotero, Google Scholar, and PDFs and looking up PubMed ID's and DOIs.
See
[`ReadPDFs`](https://docs.ropensci.org/RefManageR/reference/ReadPDFs.md),
[`ReadZotero`](https://docs.ropensci.org/RefManageR/reference/ReadZotero.md),
[`ReadCrossRef`](https://docs.ropensci.org/RefManageR/reference/ReadCrossRef.md),
[`ReadGS`](https://docs.ropensci.org/RefManageR/reference/ReadGS.md),
[`ReadPubMed`](https://docs.ropensci.org/RefManageR/reference/ReadPubMed.md),
[`GetPubMedByID`](https://docs.ropensci.org/RefManageR/reference/GetPubMedByID.md),
[`GetPubMedRelated`](https://docs.ropensci.org/RefManageR/reference/GetPubMedRelated.md).

**Manipulating BibEntry objects**

BibEntry objects may be searched and indexed by field values, name
lists, keys, dates, date ranges, etc. See
[`[.BibEntry`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md),
`[<-.BibEntry`,
[`[[.BibEntry`](https://docs.ropensci.org/RefManageR/reference/sub-sub-.BibEntry.md),
[`$.BibEntry`](https://docs.ropensci.org/RefManageR/reference/cash-.BibEntry.md).

**Printing and Exporting Bibliographies**

The
[`print.BibEntry`](https://docs.ropensci.org/RefManageR/reference/print.BibEntry.md)
function can print in a number of formats (e.g. text, html) and most of
the base bibliography styles available with BibLaTeX (e.g. alphabetic,
numeric, authortitle, and authoryear).
[`toBibtex.BibEntry`](https://docs.ropensci.org/RefManageR/reference/toBiblatex.md)
will convert a BibEntry object to a character vector containing lines of
a BibTeX file, converting fields, entry types and expanding
crossreferences as needed to coerce BibLaTeX entries to BibTeX.
[`toBiblatex`](https://docs.ropensci.org/RefManageR/reference/toBiblatex.md)
converts the BibEntry object to a character vector containing lines of
the corresponding BibLaTeX file. The results can be written to a file
using
[`WriteBib`](https://docs.ropensci.org/RefManageR/reference/WriteBib.md).

Citations can be generated in a number of styles using one of the
available functions for citations. A list of references can be printed
based on the works the user has cited thus far in their document. See
[`Cite`](https://docs.ropensci.org/RefManageR/reference/Cite.md). The
citations and bibliography can be printed including hyperlinks using
either the R Markdown or R HTML formats.

**Additional features**

All sorting methods for bibliographies available in the BibLaTeX LaTeX
package have been implemented see
[`sort.BibEntry`](https://docs.ropensci.org/RefManageR/reference/sort.BibEntry.md)
and the references.

Using
[`open.BibEntry`](https://docs.ropensci.org/RefManageR/reference/open.BibEntry.md)
electronic copies of references can be opened in a PDF viewer or web
browser.

The convenience function
[`BibOptions`](https://docs.ropensci.org/RefManageR/reference/BibOptions.md)
is provided for setting defaults for commonly used functions such as
[`print.BibEntry`](https://docs.ropensci.org/RefManageR/reference/print.BibEntry.md),
[`[.BibEntry`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md),
and [`Cite`](https://docs.ropensci.org/RefManageR/reference/Cite.md).
Its interface is similar to
[`options`](https://rdrr.io/r/base/options.html).

## References

McLean, M. W. (2014). Straightforward Bibliography Management in R Using
the RefManageR Package. [arXiv: 1403.2036
\[cs.DL\]](https://arxiv.org/abs/1403.2036).

Kime, P., M. Wemheuer, and P. Lehman (2022). The biblatex Package.
<http://mirrors.ibiblio.org/CTAN/macros/latex/contrib/biblatex/doc/biblatex.pdf>.

Hornik, K., D. Murdoch, and A. Zeileis (2012). Who Did What? The Roles
of R Package Authors and How to Refer to Them. The R Journal **4**, 1.
<https://journal.r-project.org/archive/2012-1/RJournal_2012-1_Hornik~et~al.pdf>

Patashnik, O (1988). Bibtexing.
<https://tug.org/texmf-docs/bibtex/btxdoc.pdf>.

## See also

Useful links:

- <https://github.com/ropensci/RefManageR/>

- Report bugs at <https://github.com/ropensci/RefManageR/issues>

## Author

**Maintainer**: Mathew W. McLean <mathew.w.mclean@gmail.com>
([ORCID](https://orcid.org/0000-0002-7891-9645))

Other contributors:

- Andy Bunn <bunna@wwu.edu> (function latexify used by toBiblatex)
  \[contributor\]

McLean, M. W. <mathew.w.mclean@gmail.com>
