# Extract all fields present in a BibEntry object

These functions return a list of all fields present in a BibEntry
object.

## Usage

``` r
# S3 method for class 'BibEntry'
levels(x)

fields(x)
```

## Arguments

- x:

  a BibEntry object.

## Value

a list with the same length as `x` of character vectors giving the
fields present in each entry of a BibEntry object.

## Note

The only difference between `fields` and `levels` is that `levels`
returns a list with element names corresponding to entry keys.

## Examples

``` r
bib <- as.BibEntry(list(c(bibtype = "Article", key = "mclean2014a", title = "My New Article", 
  author = "Mathew W. McLean", 
  journaltitle = "The Journal", date = "2014-01"), c(bibtype = "Book", key = "mclean2014b", 
  title = "My New Book", editor = "Mathew W. McLean", ISBN = "247123837", date = "2014-02")))       
fields(bib)
#> [[1]]
#> [1] "title"        "author"       "journaltitle" "date"        
#> 
#> [[2]]
#> [1] "title"  "editor" "isbn"   "date"  
#> 
levels(bib)
#> $mclean2014a
#> [1] "title"        "author"       "journaltitle" "date"        
#> 
#> $mclean2014b
#> [1] "title"  "editor" "isbn"   "date"  
#> 
```
