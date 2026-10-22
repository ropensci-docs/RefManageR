# Rename a field in a BibEntry object.

This function will rename a field, in every entry where it is present,
in a BibEntry object.

## Usage

``` r
UpdateFieldName(x, old.field, new.field)
```

## Arguments

- x:

  \- a BibEntry object

- old.field:

  \- string; the current name of the field to be renamed

- new.field:

  \- string; the new name to replace `old.field`

## Value

`x`, with the renamed field.

## Examples

``` r
bib <- as.BibEntry(list(c(bibtype = "article", key = "mclean2014a", title = "My New Article", 
  author = "Mathew W. McLean", journal = "The Journal", date = "2014-01"), 
  c(bibtype = "article", key = "mclean2014b", title = "My Newer Article", 
    author = "Mathew W. McLean", journal = "The Journal", date = "2014-02")))       
bib <- UpdateFieldName(bib, "journal", "journaltitle")
toBiblatex(bib)   
#> @Article{mclean2014a,
#>   title = {My New Article},
#>   author = {Mathew W. McLean},
#>   journaltitle = {The Journal},
#>   date = {2014-01},
#> }
#> 
#> @Article{mclean2014b,
#>   title = {My Newer Article},
#>   author = {Mathew W. McLean},
#>   journaltitle = {The Journal},
#>   date = {2014-02},
#> }
```
