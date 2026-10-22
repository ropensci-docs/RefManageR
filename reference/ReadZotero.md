# Get Bibliography Information From a Zotero Library.

Get Bibliography Information From a Zotero Library.

## Usage

``` r
ReadZotero(
  user,
  group,
  .params,
  temp.file = tempfile(fileext = ".bib"),
  delete.file = TRUE
)
```

## Arguments

- user:

  Zotero userID for use in calls to the Zotero API. This is not the same
  as your Zotero username. The userID for accessing user-owned libraries
  can be found at `https://www.zotero.org/settings/keys` after logging
  in.

- group:

  Zotero groupID for use in calls to the Zotero API. Only one of `user`
  and `group` should be specified; `group` will be ignored if both are
  specified.

- .params:

  A *named* list of parameters to use in requests to the Zotero API with
  possible values

  - q - Search string to use to search the library

  - qmode - Search mode. Default is "titleCreatorYear". Use "everything"
    to include full-text content in search.

  - key - API key. This must be specified to access non-public
    libraries.

  - collection - name of a specific collection within the library to
    search

  - itemType - type of entry to search for; e.g., "book" or
    "journalArticle"

  - tag - name of tag to search for in library

  - limit - maximum number of entries to return

  - start - index of first entry to return

- temp.file:

  character; file name where the BibTeX data returned by Zotero will be
  temporarily written.

- delete.file:

  boolean; should `temp.file` be removed on exit?

## Value

An object of class BibEntry

## References

`https://www.zotero.org/support/dev/server_api/v2/read_requests`

## See also

[`BibEntry`](https://docs.ropensci.org/RefManageR/reference/BibEntry.md)

## Examples

``` r
if (FALSE) { # \dontrun{
## first two entries in library with bayesian in title
ReadZotero(user = "1648676", .params = list(q = "bayesian",
  key = "7lhgvcwVq60CDi7E68FyE3br", limit=2))

## Search specific collection
## collection key can be found by reading uri when collection is selected in Zotero
ReadZotero(user = "1648676", .params=list(q = "yu", key = "7lhgvcwVq60CDi7E68FyE3br",
  collection = "3STEQRNU"))

## Search by tag
## Notice the issue with how Zotero uses a TechReport entry for arXiv manuscripts
## This is one instance where the added fields of BibLaTeX are useful
ReadZotero(user = "1648676", .params=list(key = "7lhgvcwVq60CDi7E68FyE3br",
  tag = "Statistics - Machine Learning"))

## To read these in you must set check.entries to FALSE or "warn"
old.opts <- BibOptions(check.entries = FALSE)
length(ReadZotero(user = "1648676", .params = list(key = "7lhgvcwVq60CDi7E68FyE3br",
  tag = "Statistics - Machine Learning")))

## Example using groups
ReadZotero(group = "13495", .params = list(q = "Schmidhuber",
  collection = "QU23T27Q"))
BibOptions(old.opts)
} # }
```
