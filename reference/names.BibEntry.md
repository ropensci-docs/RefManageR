# Names (keys) of a BibEntry object

Functions to get and set the keys of an object of class BibEntry

## Usage

``` r
# S3 method for class 'BibEntry'
names(x) <- value

# S3 method for class 'BibEntry'
names(x)
```

## Arguments

- x:

  an object of class BibEntry

- value:

  character vector of new key values to replace into `x`

## Value

`names<-` the updated BibEntry object.

`names` - character vector of the keys of the BibEntry object.

## Author

McLean, M. W. <mathew.w.mclean@gmail.com>

## Examples

``` r
if (requireNamespace("bibtex")) {
    bib <- ReadBib(system.file("Bib", "test.bib", package = "RefManageR"))
    names(bib)
    names(bib)[1] <- 'newkey'
}
```
