# Set options/hooks for RefManageR

This function is used to access and set package options for RefManageR,
similar to [`options`](https://rdrr.io/r/base/options.html). The options
are listed in the details

## Usage

``` r
BibOptions(..., restore.defaults = FALSE)
```

## Arguments

- ...:

  a character vector or strings specifying option names to access; or to
  set options values, a named list or vector of option values or options
  specified in name=value pairs.

- restore.defaults:

  logical; if TRUE, `...`'s are ignored and all package options are
  restored to their defaults.

## Value

if a vector of option names is supplied, the current value of the
requested options, or if `...` is missing, all current option values;
otherwise, when setting options the old values of the changed options
are (invisibly) returned as a list.

## Details

The following are valid package options.

**Options for searching/indexing a BibEntry object. See
[`[.BibEntry`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md)
and `[<-.BibEntry`**

1.  `match.author` - string; controls how name list fields (author,
    editor, translator, etc.) are matched when searching for names.
    “family.with.initials” require family names and given name initials
    to match, “exact” requires names to match exactly, and any other
    value results in only family names being compared (the default).

2.  `match.date` - string; controls how date fields are matched when
    searching. If “year.only” (the default), only years are checked for
    equality when comparing dates, otherwise months and days will also
    be compared, if they are available.

3.  `use.regex` - logical; if `TRUE`, regular expressions are used when
    searching non-date fields; otherwise, exact matching is used.

4.  `ignore.case` - logical; if `TRUE`, case is ignored when searching.

5.  `return.ind` - logical; if `TRUE` the return value of
    [`SearchBib`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md)
    and the operators
    [`[.BibEntry`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md),
    will be the indices of any matches; otherwise, a `BibEntry` object
    is returned.

**Options for Printing with
[`print.BibEntry`](https://docs.ropensci.org/RefManageR/reference/print.BibEntry.md)
and
[`PrintBibliography`](https://docs.ropensci.org/RefManageR/reference/Cite.md)**

1.  `bib.style` - string; Biblatex bibliography style to use when
    printing and formatting a BibEntry object. Possible values are
    “numeric” (default), “authoryear”, “authortitle”, “alphabetic”,
    “draft”.

2.  `first.inits` - logical; if `TRUE`, only given name initials are
    displayed when printing; otherwise, full names are used.

3.  `dashed` - logical; if `TRUE` and `bib.style = "authoryear"` or
    `bib.style = "authortitle"`, recurring author and editor names are
    replaced with “—” when printing.

4.  `sorting` - string; controls how BibEntry objects are sorted.
    Possible values are “nty”, “nyt”, “nyvt”, “anyt”, “anyvt”, “ynt”,
    “ydnt”, “none”, “debug”; see
    [`sort.BibEntry`](https://docs.ropensci.org/RefManageR/reference/sort.BibEntry.md)

5.  `max.names` - numeric; maximum number of names to display before
    using “et al.” when formatting and printing name list fields. This
    is also the minimum number of names that will be displayed if “et
    al.” is used (corresponding to the ‘minnames’ package option in
    Biblatex). See below and option `longnamesfirst` when using this
    argument with the citation functions
    ([`Citet`](https://docs.ropensci.org/RefManageR/reference/Cite.md),
    etc.).

6.  `no.print.fields` character vector; fields that should not be
    printed, e.g., doi, url, isbn, etc.

7.  `style` - character string naming the printing style. Possible
    values are plain text (style “text”), BibTeX (“Bibtex”), BibLaTeX
    (“Biblatex”), a mixture of plain text and BibTeX as traditionally
    used for citations (“citation”), HTML (“html”), LaTeX (“latex”),
    “markdown”, “yaml”, R code (“R”), and a simple copy of the
    textVersion elements (style “textVersion”, see
    [`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md))

**Options for the
[`Cite`](https://docs.ropensci.org/RefManageR/reference/Cite.md)
functions**

1.  `cite.style` - character string; bibliography style to use to
    generate citations.

2.  `style` - as above, but used to format the citations.

3.  `hyperlink` - character string or logical; for use with
    `style = "markdown"` and `style = "html"` (ignored otherwise). If
    `FALSE`, no hyperlink will be generated for the citation or in the
    bibliography when printing. If set equal to `"to.bib"`, then
    hyperlinks will be generated linking the citation and bibliography.
    The default value, `"to.doc"`, will try to create the hyperlink
    using the `url`, `doi`, or `eprint` fields of entry. If these fields
    are not available, the hyperlink will point to the bibliography. See
    also
    [`open.BibEntry`](https://docs.ropensci.org/RefManageR/reference/open.BibEntry.md).

4.  `super` - logical; should superscripts be used for numeric
    citations? Ignored if `cite.style != "numeric"`.

5.  `max.names` - numeric; same as above, except for citations. Note,
    that the first time a reference is cited, this option will be
    ignored if `longfirstnames` is `TRUE`.

6.  `longnamesfirst` logical; should the first time a citation appears
    in the text not be truncated at `max.names`?

7.  `bibpunct` - character vector; punctuation to use in a citation. The
    entries in `bibpunct` are as follows

    1.  The left delimiter for non-alphabetic and non-numeric citation
        styles

    2.  The right delimiter for non-alphabetic and non-numeric citation
        styles

    3.  The left delimiter for alphabetic and numeric citation styles

    4.  The right delimiter for alphabetic and numeric citation styles

    5.  The separator between references in a citation.

    6.  Punctuation to go between the author and year.

**Other**

1.  `check.entries` - string or `FALSE`; if `FALSE` entries are not
    checked to ensure that they have all the required fields for the
    type of entry; if “warn” then entries are checked, but only a
    warning is issued and the entry is processed anyway; otherwise an
    error is produced if an entry does not have the required fields
    (default). Note that the majority of fields listed as required for a
    particular entry type in the Biblatex manual are not actually
    required for Biblatex to produce an entry.

2.  `merge.fields.to.check` - character vector; for
    [`merge.BibEntry`](https://docs.ropensci.org/RefManageR/reference/merge.BibEntry.md)
    and the operator
    [`+.BibEntry`](https://docs.ropensci.org/RefManageR/reference/merge.BibEntry.md),
    the fields that should be checked when comparing entries for
    equality when merging BibEntry objects. Specifying “all” results in
    all fields be checked with
    [`duplicated`](https://rdrr.io/r/base/duplicated.html). The default
    is “key” to only check for duplicated keys.

## Note

If `...` is missing and `restore.defaults = FALSE`, all options and
their current values will be returned as a list.

## See also

[`print.BibEntry`](https://docs.ropensci.org/RefManageR/reference/print.BibEntry.md),
[`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md),
[`options`](https://rdrr.io/r/base/options.html)

## Examples

``` r
BibOptions()
#> $match.author
#> [1] "family.name"
#> 
#> $match.date
#> [1] "year.only"
#> 
#> $return.ind
#> [1] FALSE
#> 
#> $merge.fields.to.check
#> [1] "key"
#> 
#> $bib.style
#> [1] "numeric"
#> 
#> $first.inits
#> [1] TRUE
#> 
#> $dashed
#> [1] TRUE
#> 
#> $sorting
#> NULL
#> 
#> $check.entries
#> [1] "error"
#> 
#> $use.regex
#> [1] TRUE
#> 
#> $ignore.case
#> [1] TRUE
#> 
#> $max.names
#> [1] 3
#> 
#> $cite.style
#> [1] "authoryear"
#> 
#> $longnamesfirst
#> [1] TRUE
#> 
#> $hyperlink
#> [1] "to.doc"
#> 
#> $style
#> [1] "text"
#> 
#> $super
#> [1] FALSE
#> 
#> $bibpunct
#> [1] "(" ")" "[" "]" ";" ","
#> 
#> $no.print.fields
#> character(0)
#> 
BibOptions("first.inits", "bib.style")
#> $first.inits
#> [1] TRUE
#> 
#> $bib.style
#> [1] "numeric"
#> 

oldopts <- BibOptions(first.inits = FALSE, bib.style = "authoryear")
oldopts
#> $first.inits
#> [1] TRUE
#> 
#> $bib.style
#> [1] "numeric"
#> 
BibOptions(oldopts)

BibOptions(restore.defaults = TRUE)
```
