




# Updating packages

Written by Mariam Walaa.

## Introduction

In this lesson, you will learn how to:

- Update a package using `update.packages()`
- Understand what R outputs when you run `update.packages()`

Prerequisite skills include:

- Installing packages
- Loading packages

Highlights:

- Update packages to avoid running into bugs or missing out on updates.
- R updates all packages with new updates if no packages are specified.

## Arguments

The `update.packages()` function takes the following as arguments:

| Argument | Parameter     | Details                                                 |
|----------|---------------|---------------------------------------------------------|
| oldPkgs  | packages      | this updates all packages if no packages are specified* |

*If you want to specify a certain set of packages, pass a vector `c("package1",
"package2", "package3")` to let the function know that these are the packages you'd like
to update.

You can read more about `update.packages()` in the function documentation
[here](https://www.rdocumentation.org/packages/utils/versions/3.6.2/topics/update.packages).

## Overview 

It's important to update packages for the following reasons:

- Stay up-to-date with the most recent version of the package.
- Meet requirements of other packages we are installing.
- Avoid running into bugs or missing out on new features.

You can check if any packages need to be updated in two ways:

1. Go to Tools > Check for Package Updates
2. Run `update.packages()` to get a list of all the packages that have new versions
available.

When you run `update.packages()`, R will ask you if you want to update each of the
packages currently installed one-by-one. Once it's done going through all of your
packages, it will start updating the ones you asked to update. 

<img src="images/20_updating-libraries-1.PNG" width="90%" />

<img src="images/20_updating-libraries-2.PNG" width="90%" />

## Exercises

### Exercise 1

Run this code in your own RStudio.


```r
update.packages()
```

<!-- ```{r updating-packages-exercise-1, echo = FALSE} -->
<!-- question("Which of these are true? Check all true statements.", -->
<!--         answer(paste("When you run `update.packages()`, R lists the current version", -->
<!--         "and the version available to update to."), correct = TRUE), -->
<!--         answer(paste("R lets you know whether a package has been successfully", -->
<!--                      "unpacked (i.e., updated)"), correct = TRUE), -->
<!--         answer("The location of the downloaded packages is provided.", -->
<!--                correct = TRUE), -->
<!--         allow_retry = TRUE, -->
<!--         random_answer_order = TRUE) -->
<!-- ``` -->

### Exercise 2

<!-- ```{r updating-packages-exercise-2, echo = FALSE} -->
<!-- question("Which is the correct way to update `dplyr` and `ggplot2`?", -->
<!--          answer("`update.packages(c('dplyr', 'ggplot2'))`"), -->
<!--          answer("`update.packages(oldPkgs = c('dplyr', 'ggplot2'))`", -->
<!--                 correct = TRUE), -->
<!--          answer("`update.packages(dplyr, ggplot2)`"), -->
<!--          allow_retry = TRUE, -->
<!--          random_answer_order = TRUE -->
<!-- ) -->
<!-- ``` -->

## Common Mistakes & Errors

Below are some common mistakes and errors that you may come across while updating packages:

- You try to update a list of packages without properly specifying that list of packages. 
  * Specifically, you try to pass `c("dplyr", "ggplot2")` to `update.packages()` without
  specifying that `c("dplyr", "ggplot2")` belongs to the argument `oldPkgs` explicitly.
  This needs to be done in order for R to know that this is a list of old packages that
  you want to update.
- You receive a pop-up from R asking you `Update?` and you forget to respond with `Yes`,
`No`, or `Cancel`.
- You try to use a function that has been recently changed in a package update and your
currently installed package is out-of-date.

## Next Steps

If you would like to learn more about updating packages in R, here are some additional
functions you may find helpful:

- You can run `old.packages()` to see which of the packages you have are currently out of date.









