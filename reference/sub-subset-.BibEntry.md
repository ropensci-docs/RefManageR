# Assign a BibEntry entry to another BibEntry object

Replace one entry in a BibEntry object with another

## Usage

``` r
# S3 method for class 'BibEntry'
x[[i]] <- value
```

## Arguments

- x:

  \- a BibEntry object

- i:

  \- a numeric index or a string entry key

- value:

  \- a single entry BibEntry object or an object that can be coerced to
  BibEntry using
  [`as.BibEntry`](https://docs.ropensci.org/RefManageR/reference/as.BibEntry.md)

## Value

an object of class BibEntry

## Details

This function will replace the specified entry in `x` with the entry
given by `value`. To replace multiple entries see `[<-.BibEntry`.

## See also

Other operators:
[`$.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/cash-.BibEntry.md),
`$<-.BibEntry()`,
[`+.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/merge.BibEntry.md),
[`[.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/SearchBib.md),
`[<-.BibEntry()`,
[`[[.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/sub-sub-.BibEntry.md),
[`c.BibEntry()`](https://docs.ropensci.org/RefManageR/reference/c.BibEntry.md)
