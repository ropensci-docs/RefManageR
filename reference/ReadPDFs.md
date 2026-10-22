# Create bibliographic information from PDF Metadata.

This function creates bibliographic information by reading the Metadata
and text of PDFs stored in a user specified directory using Poppler
(<https://poppler.freedesktop.org/>). IF requested, the function first
searches for DOIs and downloads `BibTeX` entries from
[`ReadCrossRef`](https://docs.ropensci.org/RefManageR/reference/ReadCrossRef.md)
if DOIs are found. If this is not requested or a DOI is not found for an
entry, an attempt is made to build a BibTeX entry from the metadata and
text.

## Usage

``` r
ReadPDFs(
  path,
  .enc = "UTF-8",
  recursive = TRUE,
  use.crossref = TRUE,
  use.metadata = TRUE,
  progress = FALSE
)
```

## Arguments

- path:

  character; path to directory containing pdfs or filename of one pdf.
  `normalizePath` is used on the specified path

- .enc:

  character; text encoding to use for reading pdf and creating BibEntry
  object. Available encodings for Poppler can be found using
  `system("pdfinfo -listenc")`. The encoding must also be listed in
  [`iconvlist()`](https://rdrr.io/r/base/iconv.html).

- recursive:

  logical; same as
  [`list.files`](https://rdrr.io/r/base/list.files.html). Should pdfs in
  subdirectories of path be used?

- use.crossref:

  logical; should an attempt be made to download bibliographic
  information from CrossRef if any Document Object Identifiers (DOIs)
  are found? This is only supported if the Suggeseted package `bibtex`
  is found.

- use.metadata:

  logical; should the PDF metadata also be used to help create entries?

- progress:

  logical; should progress bar be generated when fetching from CrossRef?

## Value

An object of class BibEntry.

## Details

This function requires that the `pdfinfo` utility from Poppler PDF
<https://poppler.freedesktop.org/> be installed.

This function will create only `Article` or `Misc` `BibTeX` entries.

The absolute path to each file will be stored in the bib entry in a
field called ‘file’, which is recognized by `BibLaTeX` (though not
printed by any standard style) and can be used by the
[`open.BibEntry`](https://docs.ropensci.org/RefManageR/reference/open.BibEntry.md)
function to open the PDF in the default viewer.

If the keywords metadata field is available, it will be added to the bib
entry in a field ‘keywords’, which is recognized by `BibLaTeX`.

## References

<https://poppler.freedesktop.org/>

## See also

[`ReadCrossRef`](https://docs.ropensci.org/RefManageR/reference/ReadCrossRef.md),
[`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md),
[`open.BibEntry`](https://docs.ropensci.org/RefManageR/reference/open.BibEntry.md)

## Examples

``` r
if (FALSE) { # \dontrun{
path <- system.file("doc", package = "RefManageR")
ReadPDFs(path)
} # }
```
