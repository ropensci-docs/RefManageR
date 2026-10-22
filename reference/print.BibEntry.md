# Print BibLaTeX bibliography Entries

Prints bibliographic information stored in BibEntry objects in BibLaTeX
style

## Usage

``` r
# S3 method for class 'BibEntry'
print(x, .opts = list(), ...)
```

## Arguments

- x:

  a BibEntry object

- .opts:

  a list of formatting options from
  [`BibOptions`](https://docs.ropensci.org/RefManageR/reference/BibOptions.md).
  Possible options are

  - `style` - character string naming the printing style. Possible
    values are plain text (style “text”), BibTeX (“Bibtex”), BibLaTeX
    (“Biblatex”), a mixture of plain text and BibTeX as traditionally
    used for citations (“citation”), HTML (“html”), LaTeX (“latex”),
    “markdown”, “yaml”, R code (“R”), and a simple copy of the
    textVersion elements (style “textVersion”, see
    [`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md))

  - `bib.style` - character string specifying BibLaTeX style to use for
    formatting references. Possible values are “numeric” (default),
    “authoryear”, “authortitle”, “alphabetic”, “draft”. See section
    3.3.2 of the BibLaTeX manual.

  - `sorting` - how should the entries in `x` be sorted? See
    [`sort.BibEntry`](https://docs.ropensci.org/RefManageR/reference/sort.BibEntry.md).

  - `max.names` - maximum number of names to display for name list
    fields before truncation with “et al.”.

  - `first.inits` - logical; if true only initials of given names are
    printed, otherwise full names are used.

  - `dashed` - logical; for `.bibstyle = "authoryear"` or
    `.bibstyle = "authoryear"` only, if `TRUE` duplicate author and
    editor lists are replaced with “—” when printed.

  - `no.print.fields` character vector; fields that should not be
    printed, e.g., doi, url, isbn, etc.

- ...:

  extra parameters to pass to the renderer.

## Note

setting max.names to `value` is equivalent to setting `maxnames=value`
and `minnames=value` in BibLaTeX.

Custom BibLaTeX styles may be defined using the function `bibstyle`. To
fully support BibLaTeX, the created environment must have functions for
formatting each of the entry types described in
[`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md).

## References

Lehman, Philipp and Kime, Philip and Boruvka, Audrey and Wright, J.
(2013). The biblatex Package.
<http://mirrors.ibiblio.org/CTAN/macros/latex/contrib/biblatex/doc/biblatex.pdf>.

## See also

[`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md),
[`ReadBib`](https://docs.ropensci.org/RefManageR/reference/ReadBib.md),
[`sort.BibEntry`](https://docs.ropensci.org/RefManageR/reference/sort.BibEntry.md)

## Examples

``` r
if (requireNamespace("bibtex")) {
    file.name <- system.file("Bib", "biblatexExamples.bib", package="RefManageR")
    bib <- suppressMessages(ReadBib(file.name))
    print(bib[author="aristotle"], .opts = list(bib.style = "numeric"))
    print(bib[55:57], .opts = list(bib.style = "authortitle", first.inits = FALSE))
    print(bib[80:88], .opts = list(bib.style = "alphabetic", max.names = 1,
          no.print.fields = "issn"))
    print(bib[32:36], .opts = list(bib.style = "draft"))
    oldopts <- BibOptions(bib.style = "authoryear", dashed = TRUE, sorting = "ydnt")
    bib[editor = "westfahl"]
    BibOptions(oldopts)
}
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
#> Warning: nietzsche:ksa1: unexpected END_OF_INPUT ' and Walter de Gruyter, 1988.
#> '
#> Nietzsche, Friedrich. _Sämtliche Werke. Kritische Studienausgabe_. Vol.
#> 1: _Die Geburt der Tragödie. Unzeitgemäße Betrachtungen I-IV.
#> Nachgelassene Schriften 1870-1973_. Ed. by Giorgio Colli and Mazzino
#> Montinari. 2nd ed. München and Berlin and New York: dtv # and Walter de
#> Gruyter, 1988.
#> 
#> Nussbaum, Martha. _Aristotle's “De Motu Animalium”_. Princeton:
#> Princeton University Press, 1978.
#> 
#> Piccato, Pablo. _City of Suspects. Crime in Mexico City, 1900-1931_.
#> Durham and London: Duke University Press, 2001.
#> [11] _Computers and Graphics_. 35.4 (2011): _Semantic 3D Media and
#> Content_.
#> 
#> [Alm+98] J. L. Almendro et al. “Elektromagnetisches Signalhorn”.
#> EU-29702195U (countryfr and countryuk and countryde). 1998.
#> 
#> [CTAN06] _CTAN. The Comprehensive TeX Archive Network_. 2006.
#> <https://www.ctan.org> (visited on 10/01/2006).
#> 
#> [Itz96] N. Itzhaki. _Some remarks on 't Hooft's S-matrix for black
#> holes_. Mar. 11, 1996. arXiv: hep-th/9603067.
#> 
#> [KI95] F. Kowalik et al. “Estimateur d'un défaut de fonctionnement d'un
#> modulateur en quadrature et étage de modulation l'utilisant”. patreqfr
#> 9500261. Jan. 11, 1995.
#> 
#> [Lau+06] X. Laufenberg et al. “Elektrische Einrichtung und
#> Betriebsverfahren”. patenteu 1700367. Robert Bosch GmbH, Daimler
#> Chrysler AG and Bayerische Motoren Werke AG. Sep. 13, 2006.
#> 
#> [Mar05] N. Markey. _Tame the BeaST. The B to X of BibTeX_. Oct. 16,
#> 2005.
#> <http://tug.ctan.org/tex-archive/info/bibtex/tamethebeast/ttb_en.pdf>
#> (visited on 10/01/2006).
#> 
#> [SRV97] R. E. Sorace et al. “High-Speed Digital-to-RF Converter”.
#> patentus 5668842. Hughes Aircraft Company. Sep. 16, 1997.
#> 
#> [WS10] J. Wassenberg et al. _Faster Radix Sort via Virtual Memory and
#> Write-Combining_. Aug. 17, 2010. arXiv: 1008.2849v1 [cs.DS].
#> *coleridge* S. T. Coleridge. _The collected works of Samuel Taylor
#> Coleridge_. Vol. 7.2: _Biographia literaria, or Biographical sketches
#> of my literary life and opinions_. Ed. by K. Coburn, J. Engell and W.
#> J. Bate. Bollingen Series 75. London: Routledge and Kegan Paul, 1983.
#> 
#> *companion* M. Goossens, F. Mittelbach, and A. Samarin. _The LaTeX
#> Companion_. 1st ed. Reading, Mass.: Addison-Wesley, 1994. 528 pp.
#> 
#> *cotton* F. A. Cotton, G. Wilkinson, C. A. Murillio, et al. _Advanced
#> inorganic chemistry_. 6th ed. Chichester: Wiley, 1999.
#> 
#> *gerhardt* M. J. Gerhardt. _The Federal Appointments Process. A
#> Constitutional and Historical Analysis_. Durham and London: Duke
#> University Press, 2000.
#> 
#> *gonzalez* R. Gonzalez. _The Ghost of John Wayne and Other Stories_.
#> Tucson: The University of Arizona Press, 2001. ISBN: 0-816-52066-6.
```
