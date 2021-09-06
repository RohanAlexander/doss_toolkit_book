



# Calling packages

Written by Mariam Walaa.


## Introduction

In this lesson, you will learn how to:

- Load an R package with the correct syntax
- Understand R's output when you call a package
- Understand what R does when multiple packages use the same function name

Prerequisite skills include:

- Installing packages 

Highlights:

- An R package needs to be loaded in order to use its functions.
- An R package needs to be loaded using the appropriate syntax.
- R provides important details about a package when you load it.
- R has a way of handling packages using the same function name.

## Arguments

## library()

The `library()` function takes the following as arguments:

| Argument       | Parameter    | Details                                             |
|----------------|--------------|-----------------------------------------------------|
| package*       | package name | this takes package name in or not in quotations     |
| help           | package name | this displays the help for the specified package    |
| logical.return | Boolean      | this returns a Boolean on whether package is loaded |
| quietly        | Boolean      | this suppresses confirmations if set to True        |
| verbose        | Boolean      | this suppresses diagnostics if set to False         |

*This is a required argument.

Note that you if you want to load the help using `library()`, you may need to pass the
'help' parameter alone without the others. If you would like more information about the
arguments, please visit the R documentation for this function
[here](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/library).

## Overview

Loading packages properly is a necessary aspect of running code in R. Loading a package is
needed in order to be able to use functions in that package.

Here is what loading a package looks like.


```r
library(ggplot2)
```

Note that some functions are already provided in base R and do not belong to specific
packages. You will see in future tutorials that this is the case for the functions `lm()`
and `summary()`.

Besides knowing how to load packages and which packages to load, it's important to 
understand what R does when multiple packages use the same function name. This may be the 
cause of many errors you have in your code. There are two common scenarios that may lead 
to errors related to this issue in your code:

1. You don't load a package you need to use a function, but the function name exists in
base R, so R tries to use the base R function but gets into issues since you
probably don't have the appropriate parameters for that function.

2. You load the package you need to use a function, but you load another package after,
and that package contains the same function name and masks* the initial package.

*When R _masks_ a package with another package for a specific function, it is deciding to
use the function belonging to the package that has masked the other package.

The best way to avoid running into this issue is to change the order in which you are
calling the packages so that the package whose functions you need is last, or to let R
know which package you want to use a function from. For example, if you want to use
`select()` from dplyr and not some other package, you can specify `dplyr::select()`.

Here is a visualization to help you understand when to use the different package-related
functions. Please note that it is a lot more common to use `library()` over `require()`. 
You can use `require()` if you want your code to continue running even if the package did 
not load correctly. You can learn more about `require()` in its documentation 
[here](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/library).

<img src="images/17_packages.png" width="90%" />

### Citing R 

When we use R in a formal setting (such as, when writing a paper), we will want to cite R.
This can be done with some guidance from the `citation()` function.


```r
citation()
#> 
#> To cite R in publications use:
#> 
#>   R Core Team (2020). R: A language and environment
#>   for statistical computing. R Foundation for
#>   Statistical Computing, Vienna, Austria. URL
#>   https://www.R-project.org/.
#> 
#> A BibTeX entry for LaTeX users is
#> 
#>   @Manual{,
#>     title = {R: A Language and Environment for Statistical Computing},
#>     author = {{R Core Team}},
#>     organization = {R Foundation for Statistical Computing},
#>     address = {Vienna, Austria},
#>     year = {2020},
#>     url = {https://www.R-project.org/},
#>   }
#> 
#> We have invested a lot of time and effort in creating
#> R, please cite it when using it for data analysis.
#> See also 'citation("pkgname")' for citing R packages.
```

Please refer to the References and Bibtex section in the toolkit for more information on 
why it is important to cite R and R packages.

## Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/d_Ro31Ml5fM"
frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media;
gyroscope; picture-in-picture" allowfullscreen></iframe>

## Exercises

### Exercise 1

Inspect the output provided when loading `tidyverse` below.


```r
library(tidyverse)
```


<!-- ```{r loading-packages-exercise-1, echo = FALSE} -->
<!-- question("Which of these are true? Check all true statements.", -->
<!--           answer(paste("Running `library(tidyverse)` prints out two sections: ", -->
<!--           "Attaching packages and Conflicts."), correct = TRUE), -->
<!--           answer(paste("Under `Attaching packages`, R lists the packages that get ", -->
<!--           "attached (i.e., loaded) to your session when you load tidyverse."),  -->
<!--           correct = TRUE), -->
<!--           answer(paste("Under `Conflicts`, R lists any function names that are used", -->
<!--           " in multiple packages."), correct = TRUE), -->
<!--           answer(paste("Under `Conflicts`, R also tells you which package 'masks'", -->
<!--           " another package. The masked package is the package that R uses whenever", -->
<!--           " you call that function."), message = paste("The masked package is the ", -->
<!--           "package that R does _not_ use whenever you call the function.",  -->
<!--           " The package that masks another package is the package that R uses ", -->
<!--           "when you call a function without specifying which package it comes from.")), -->
<!--           allow_retry = TRUE) -->
<!-- ``` -->

### Exercise 2

Inspect the output when loading `dplyr` below.



```r
library(dplyr)
#> 
#> Attaching package: 'dplyr'
#> The following objects are masked from 'package:stats':
#> 
#>     filter, lag
#> The following objects are masked from 'package:base':
#> 
#>     intersect, setdiff, setequal, union
```


<!-- ```{r loading-packages-exercise-2, echo = FALSE} -->
<!-- question("Which of these are true? Check all true statements.", -->
<!--           answer(paste("Running `library(dplyr)` returned a list of function names ", -->
<!--           "within each masked package."), correct = TRUE), -->
<!--           answer(paste("The functions listed for a masked package (i.e., `stats`, ", -->
<!--           "`base`) will not be used by R. R uses the functions from `dplyr` instead."), -->
<!--           correct = TRUE), -->
<!--           answer(paste("If the loaded package includes functions with the same ", -->
<!--           "name as functions from another package, the output will list the name ", -->
<!--           "of the package that shares those functions."), correct = TRUE), -->
<!--           answer(paste("This output does not specify which packages have shared ", -->
<!--           "function names."), message = paste("The output does specify the ", -->
<!--           "functions that have the same name, along with the package they belong to.")), -->
<!--           allow_retry = TRUE) -->
<!-- ``` -->

### Exercise 3

Correct the code in order to successfully call the package: `library("tidyverse')`

<!-- ```{r loading-packages-exercise-3, exercise = TRUE, exercise.eval = TRUE} -->

<!-- ``` -->

<!-- ```{r loading-packages-exercise-3-sol, echo = FALSE} -->
<!-- ex3_sol <- library("tidyverse") -->
<!-- ``` -->


<!-- ```{r loading-packages-exercise-3-check} -->
<!-- ?grade_result(pass_if(~identical(.result, ex3_sol))) -->
<!-- ``` -->


### Exercise 4

Select all the true statements about the `library()` function and calling libraries.

<!-- ```{r loading-packages-exercise-4, echo = FALSE} -->
<!-- question("Which of these are true? Check all true statements.", -->
<!--        answer(paste("When using `library()`, we can pass the package name with or ", -->
<!--        "without quotes and the function will work."), correct = TRUE), -->
<!--        answer(paste("Calling `library(tidyverse)` will load all the packages associated ", -->
<!--        "with it: `ggplot2`, `tibble`, `tidyr`, `readr`, `purrr`, `dplyr`, `stringr`", -->
<!--        ", and `forcats`."), correct = TRUE), -->
<!--        answer(paste("We need to load the `dplyr` package in addition to tidyverse if we ", -->
<!--        "want to use it along with tidyverse."), message = paste("When we load tidyverse, ", -->
<!--        "the dplyr package will be loaded along with tidyverse and we do not need to load ", -->
<!--        "it if we have already loaded the tidyverse package.")), -->
<!--        answer(paste("We can use functions from a library without loading the library ", -->
<!--        "first, as long as we have already installed it."), message = paste("A library ", -->
<!--        "needs to be installed and _then_ loaded in order to use its functions.")), -->
<!--        answer(paste("We should only load libraries whose functions we'll need in our ", -->
<!--        "code. Loading libraries we don't need wastes memory."), correct = TRUE), -->
<!--        answer(paste("When we load a package into an R session, R will always provide ", -->
<!--        "some output about the package."), message = paste("When we load a package into ", -->
<!--        "an R session, R may not provide any output for some packages, which is fine. ", -->
<!--        "The package will still have loaded.")), -->
<!--        answer(paste("Even if we fail to load a library using `library()` while running a", -->
<!--        " chunk of code, the remaining code chunk not associated with that library will ", -->
<!--        "run successfully."), message = paste("If we fail to load a library using ", -->
<!--        "`library()` while running a chunk of code, the code chunk will stop at that ", -->
<!--        "line of code and nothing else will run. To run the remaining code even if we ", -->
<!--        "fail to load a library, we can use `require()` instead.")), -->
<!--        answer(paste("If we call a function with a name that exists in multiple packages, ", -->
<!--        "R will assume you want to use the function in that package that you loaded."), -->
<!--               correct = TRUE), -->
<!--        allow_retry = TRUE, -->
<!--        random_answer_order = TRUE) -->
<!-- ``` -->

## Common Mistakes & Errors

Here are some common mistakes and errors you may come across:

- You try to load a package that has not been installed yet.
- You try to use a function from a package that has not been loaded yet.
- You try to load a package but you receive the following error message: `Error in
library(...) : there is no package called ‘...’`. This is most likely due to a typo:
  * You have misspelled the package name (i.e. "tdyverse" instead of "tidyverse")
  * You have not used the correct casing (i.e. "Tidyverse" instead of "tidyverse")

If you run into other issues while trying to load packages, try to restart R, re-install
the package, and load the package again.

## Next Steps

If you would like to learn more about functions for packages, here are some additional
functions you may find helpful:

- You can run `search()` to see currently attached packages.
- You can run `library()` to see currently installed packages.
- You can run `library(help = 'package_name') ` to see package help in RStudio. 
  + This may be faster than searching it up and possibly more up-to-date with the most
  recent version of the package.
- You can run `detach("package:_")` with the package name to detach a package from session.

If you would like to read more about packages, here are some additional resources you may
find helpful:

- Hands-On Programming with R 
  * [Chapter 3: Packages and Help
  Pages](https://rstudio-education.github.io/hopr/packages.html)
  * [Appendix B: R
  Packages](https://rstudio-education.github.io/hopr/packages2.html#packages2)
- CRAN: An Introduction to R
  * [Packages](https://cran.r-project.org/doc/manuals/R-intro.html#Packages)












