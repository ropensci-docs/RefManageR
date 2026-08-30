# Search CrossRef for citations.

Provides an interface to the CrossRef API, searching for citations given
a string query. Results are written to a bib file, read back into `R`
using
[`WriteBib`](https://docs.ropensci.org/RefManageR/reference/WriteBib.md),
and returned as a BibEntry object.

## Usage

``` r
ReadCrossRef(
  query = "",
  filter = list(),
  limit = 5,
  offset = 0,
  sort = "relevance",
  year = NULL,
  min.relevance = 2,
  temp.file = tempfile(fileext = ".bib"),
  delete.file = TRUE,
  verbose = FALSE,
  use.old.api = FALSE
)
```

## Arguments

- query:

  string; search term

- filter:

  named list of possible filters; see `Details` and `References`;
  ignored if `use.old.api = TRUE`

- limit:

  numeric; maximum number of entries to return

- offset:

  numeric; CrossRef will not return the first `offset` results (default
  0); ignored if `use.old.api = TRUE`

- sort:

  string; how specifying how the results from CrossRef should be sorted.
  Possible values when `use.old.api = FALSE` are `"score"` (default;
  same as `"relevance"`), `"updated"`, `"deposited"`, `"indexed"`, or
  `"published"`; see the references

- year:

  numeric; if specified, only results from this year will be returned.

- min.relevance:

  numeric; only results with a CrossRef-assigned relevance score at
  least this high will be returned.

- temp.file:

  string; file name to use for storing Bibtex information returned by
  CrossRef.

- delete.file:

  boolean; should the bib file be deleted on exit?

- verbose:

  boolean; if `TRUE`, additional messages are output regarding the
  results of the query.

- use.old.api:

  boolean; should the older CrossRef API be used for the search? NO
  LONGER SUPPORTED, all queries need to use the new API.

## Value

An object of class `BibEntry`.

## Details

When `use.old.api = TRUE`, the query HTTP request only returns DOIs,
which are then used to make HTTP requests for the corresponding BibTeX
entries from CrossRef; when `use.old.api = FALSE`, the query HTTP
request is parsed to create the `BibEntry` object (i.e. there are less
HTTP requests when using the new API).

CrossRef assigns a score between 0 and 100 based on how relevant a
reference seems to be to your query. The *old* API documentation warns
that while false negatives are unlikely, the search can be prone to
false positives. Hence, setting `min.revelance` to a high value may be
necessary if `use.old.api = TRUE`. In some instances with the old API,
no score is returned, if this happens, the entries are added with a
message indicating that no score was available.

Possible values for the *names* in `filter` are `"has-funder"`,
`"funder"`, `"prefix"`, `"member"`, `"from-index-date"`,
`"until-index-date"`, `"from-deposit-date"`, `"until-deposit-date"`,
`"from-update-date"`, `"until-update-date"`, `"from-created-date"`,
`"until-created-date"`, `"from-pub-date"`, `"until-pub-date"`,
`"has-license"`, `"license.url"`, `"license.version"`,
`"license.delay"`, `"has-full-text"`, `"full-text.version"`,
`"full-text.type"`, `"public-references"`, `"has-references"`,
`"has-archive"`, `"archive"`, `"has-orcid"`, `"orcid"`, `"issn"`,
`"type"`, `"directory"`, `"doi"`, `"updates"`, `"is-update"`,
`"has-update-policy"`, `"container-title"`, `"publisher-name"`,
`"category-name"`, `"type-name"`, `"award.number"`, `"award.funder"`,
`"assertion-group"`, `"assertion"`, `"affiliation"`,
`"has-affiliation"`, `"alternative-id"`, and `"article-number"`. See the
first reference for a description of their meanings.

## Note

The entries returned by Crossref are frequently missing fields required
by BibTeX, if you want the entries to be returned anyway, set
`BibOptions()$check.entries` to `FALSE` or `"warn"`

Fields `"score"` (the relevancy score) and `"license"` will be returned
when `use.old.api = FALSE`.

## References

Newer API:
<https://github.com/CrossRef/rest-api-doc/blob/master/rest_api.md>,
Older API: <https://search.crossref.org/help/api>

## See also

[`ReadZotero`](https://docs.ropensci.org/RefManageR/reference/ReadZotero.md),
[`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md),
package `rcrossref` for larger queries and deep paging

Other pubmed:
[`GetPubMedByID()`](https://docs.ropensci.org/RefManageR/reference/GetPubMedByID.md),
[`GetPubMedRelated()`](https://docs.ropensci.org/RefManageR/reference/GetPubMedRelated.md),
[`LookupPubMedID()`](https://docs.ropensci.org/RefManageR/reference/LookupPubMedID.md),
[`ReadPubMed()`](https://docs.ropensci.org/RefManageR/reference/ReadPubMed.md)

## Examples

``` r
if (interactive() && !httr::http_error("https://search.crossref.org/")){
  BibOptions(check.entries = FALSE)
  ## 3 results from the American Statistical Association involving "regression"
  ReadCrossRef("regression", filter = list(prefix="10.1198"), limit = 3)

  ## Some JRSS-B papers published in 2010 or later, note the quotes for filter
  ##   names with hypens
  ReadCrossRef(filter = list(issn = "1467-9868", "from-pub-date" = 2010),
               limit = 2, min.relevance = 0)

  ## Articles published by Institute of Mathematical Statistics
  ReadCrossRef(filter = list(prefix = "10.1214"), limit = 5, min.relevance = 0)

  ## old API
  ReadCrossRef(query = 'rj carroll measurement error', limit = 2, sort = "relevance",
    min.relevance = 80, use.old.api = TRUE)

  ReadCrossRef(query = 'carroll journal of the american statistical association',
    year = 2012, limit = 2, use.old.api = TRUE)
}
```
