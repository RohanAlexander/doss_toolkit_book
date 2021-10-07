


# References and Bibtex

*Written by Yena Joo and last updated on 7 October 2021.*

## Introduction

Citation is very important to include in your paper to provide a proper credit to the authors, and to avoid plagiarisms when it is publicly published. Of course we can manually cite and reference using citation maker online and copy and paste them, but we can also use some functions in R Markdown and use BibTeX to cite!    

In this lesson, you will learn how to cite references!

Highlights:  

- BibTeX  
- `citation()`  


## Bibliographies

### BIB file? 
`.bib` file is a text document created by a LaTeX program that contains a list of bibliographic citations in BibTeX formatting. By using this file, it enables bibliographies to be searched and published in your paper.  

By using BibTex, you would need to type each reference only once, and the citations will be automatically formatted consistently. You would first need to use the `bibliography` metadata field in YAML. 

```
---
title: "Title"
author: "Author"
date: "Feb 7, 2021"
output: html_document
bibliography: references.bib
--- 
```

A BibTeX database is a plain text file with an extension `.bib`.          

The manual BibTex database for the citation should look like this: 
```
@Manual{this string is a label when you cite this,
  title = {Title of the reference},
  author = {Author of the literature},
  organization = {Organization},
  address = {address},
  year = {published year (2020)},
  url = {https://www.the website url},
}
```

Here is an example of the citation of a book:  
```
@book{label,
   author = {},
   year = {},
   title = {},
   publisher = {},
   address = {}
}
```
Note that citation of a book must include `author`, `year`, `title`, and `publisher` fields.  

The following is an example of an article citation:   
```
@article{label,
   author = {},
   title = {},
   journal = {},
   volume = {},
   year = {},
   pages = {}
}
```
Note that the citation of an article requires `author`, `title`, `journal`, and `year` fields.  

Also, the order of the fields is not important, and you can create `bib` files that you end up don't use because BibTex will put in the list of references only the ones you used at the end of your paper.   

It might be confusing first, but the BibTex format could be easily converted using various websites and tools available on the internet.  

### Placement
you will want to end your document with an appropriate header:  

```
## Reference
``` 


### Citing R packages using `citation()` function

Not only citing websites or literature you have used for the paper, but you also would want to cite your R packages from a reproducibility perspective, or to acknowledge the work that people spent to create packages. If you choose to cite R packages as well, here is how.  

You need to cite the packages using the `citation("package name")` function. The function returns both text version and a BibTeX entry for it, if a package has more than one reference then only the text versions are shown. You can get the citation information for R packages like this: 


```r
print(citation("knitr"))
#> 
#> To cite the 'knitr' package in publications use:
#> 
#>   Yihui Xie (2021). knitr: A General-Purpose Package
#>   for Dynamic Report Generation in R. R package
#>   version 1.33.
#> 
#>   Yihui Xie (2015) Dynamic Documents with R and
#>   knitr. 2nd edition. Chapman and Hall/CRC. ISBN
#>   978-1498716963
#> 
#>   Yihui Xie (2014) knitr: A Comprehensive Tool for
#>   Reproducible Research in R. In Victoria Stodden,
#>   Friedrich Leisch and Roger D. Peng, editors,
#>   Implementing Reproducible Computational Research.
#>   Chapman and Hall/CRC. ISBN 978-1466561595
#> 
#> To see these entries in BibTeX format, use
#> 'print(<citation>, bibtex=TRUE)', 'toBibtex(.)', or
#> set 'options(citation.bibtex.max=999)'.
```



## Reference

- [Using BibTeX: a short guide](https://www.economics.utoronto.ca/osborne/latex/BIBTEX.HTM)  
- [Bibliographics and Citations](https://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html)  
- [another good resource](https://bookdown.org/yihui/rmarkdown-cookbook/bibliography.html)  


## Exercises

### Question 1

### Question 2

### Question 3

### Question 4

### Question 5

### Question 6

### Question 7

### Question 8

### Question 9

### Question 10


