# Retrieve PubMed ID's for a BibEntry object

Uses the NCBI E-utilities to to search for PubMed ID's for citations
stored in a BibEntry object.

## Usage

``` r
LookupPubMedID(bib, index)
```

## Arguments

- bib:

  a bibentry object

- index:

  indices specifying which entries of `bib` will be searched for. If
  `missing`, all entries are searched for.

## Value

a BibEntry object - `bib` with additional eprinttype and eprint fields
when the search is successful for an entry.

## Details

For each entry a citation string is created using the fields
journaltitle/journal, date/year, volume, pages, and author; and these
strings are then used to search the NCBI database for PubMed ID's.

If an ID is found for an entry, the entry is updated so that the
eprinttype field is assigned the value “pubmed” and the eprint field is
assigned the ID.

## See also

Other pubmed:
[`GetPubMedByID()`](https://docs.ropensci.org/RefManageR/reference/GetPubMedByID.md),
[`GetPubMedRelated()`](https://docs.ropensci.org/RefManageR/reference/GetPubMedRelated.md),
[`ReadCrossRef()`](https://docs.ropensci.org/RefManageR/reference/ReadCrossRef.md),
[`ReadPubMed()`](https://docs.ropensci.org/RefManageR/reference/ReadPubMed.md)

## Examples

``` r
if (interactive() && !httr::http_error("https://eutils.ncbi.nlm.nih.gov/")){
  file.name <- system.file("Bib", "RJC.bib", package = "RefManageR")
  bib <- ReadBib(file.name)
  LookupPubMedID(bib[[101:102]])
}
```
