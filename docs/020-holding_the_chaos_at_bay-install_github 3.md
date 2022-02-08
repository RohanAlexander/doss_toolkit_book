


# Install from GitHub

*Written by Haoluan Chen and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to install package from GitHub.

Prerequisite skills include:

- Having RStudio set-up and working.
- Comfort running R code in the console.
- Comfort installing package from CRAN.

## What is GitHub?

GitHub is a popular repository for open-source projects. Many developers can share and collaborate their work with the world. Sometimes, you may need to use the package from GitHub for a specific task.

Note: Unlike the packages from CRAN, there is no review process for GitHub packages, so you may encounter bugs or errors when using them.  

## How to install packages from GitHub?

To install the package from GitHub, you will need the function `install_github()` in the `devtools` package. `devtools` contains tools for package developers to build and test their packages. 

So, you need to first install `devtools` package and load the package in order to use the `install_github` function. However, a faster way to do that is to run the following code in the r chunk or the console: `devtools::install_github("developer name/package name")`. The developer name and package name can be found on the top left side of the GitHub repository

This code means that you want to call the `devtools` package and use the function `install_github()`. This way, you do not have to install and load the `devtools` package.

## Example

https://github.com/sharlagelfand/dmc

The goal of `dmc` package is to allow you to find the closest DMC embroidery floss colour(s) for a given colour, as well as access colour (hex, RGB) information about DMC colours.

You can run the following code on your console to install this package: 


```r
devtools::install_github("sharlagelfand/dmc")
```

After running this code, you will receive some message on the console and it will start installing the package (this may take a few minutes depending on your system). Then it will tell you if you successfully installed the package.

Note: for some packages, it may ask you to input something in the console to complete the installation. For `dmc` package, you will see "These packages have more recent versions available. Which would you like to update?" and "Enter one or more numbers, or an empty line to skip updates:" 

<iframe width="560" height="315" src="https://www.youtube.com/embed/hDQKBBWu98k" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Exercises

### Exercise 1

Please install the following package on your RStudio and answer the question

https://github.com/RohanAlexander/AustralianPoliticians


<!-- ```{r githubex1, echo = FALSE} -->
<!-- question("Which code can install above package?", -->
<!--           answer("devtools::install_github('RohanAlexander/AustralianPoliticians')", correct = TRUE), -->
<!--           answer("devtools::install('RohanAlexander/AustralianPoliticians')"), -->
<!--           answer("install_github('RohanAlexander/AustralianPoliticians')"), -->
<!--           answer("devtools::install_github('AustralianPoliticians')"), -->
<!--           answer("devtools::install_github('RohanAlexander')"), -->
<!--           allow_retry = TRUE) -->

<!-- ``` -->

<iframe width="560" height="315" src="https://www.youtube.com/embed/WlnawRIELzY" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Common mistakes and errors

- Pay attention to R console, it may ask you to input something
- Make sure the repository is a R package
- Make sure the spelling of the developer name and package name are correct
- Make sure spelling of the function is correctly called devtools::install_github("developer name/package name")

## Next steps

For next step, you can install the package from GitHub and start using them for your projects!

In the future, you may want to build your own R package!

R Packages is a book that gives a comprehensive treatment of all common parts of package development and uses `devtools` throughout. The first edition is available at 'http://r-pkgs.had.co.nz', but note that it has grown somewhat out of sync with the current version of `devtools`.

## Exercises

### Question 1
GitHub is a popular repository for open-source projects.
    a.  True
    b. False

### Question 2
What is the difference between packages on github and CRAN?
    a. There is no difference
    b.  There is no review process for GitHub packages
    c. packages on github are easier to install
    d. packages on github are simpler
    

### Question 3
`devtools` is required to install packages from github? 
    a. Yes
    b.  No

### Question 4
`install_github()` is used to install packages from github?
    a.  Yes
    b. No

### Question 5
What is the input to `install_github()`?
    a. "developer name"
    b. "package name"
    c.  "developer name/package name"
    d. "developer name,package name"
    
### Question 6
What does `devtools::install_github()` mean?
    a. Install `devtools` package and use `install_github()` function
    b. Install `devtools` from github
    c.  Call the `devtools` package and use the function `install_github()`
    d. Load the `devtools` package
    
### Question 7
You should make sure the github repository is a R package
    a.  True
    b. False

### Question 8
Does `install_github("sharlagelfand/dmc")` work to install the dmc package?
    a. Yes
    b. No
    c.  Yes, if you loaded the devtools package

    
### Question 9
Does `devtools::install_github("sharlagelfand/dmc")` work to install the dmc package?
    a.  Yes
    b. No
    
### Question 10
https://github.com/RohanAlexander/AustralianPoliticians
Which code can install above package?
    a. `devtools::install('RohanAlexander/AustralianPoliticians')`
    b. `install_github('RohanAlexander/AustralianPoliticians')`
    c. `devtools::install_github('AustralianPoliticians')`
    d.  `devtools::install_github('RohanAlexander/AustralianPoliticians')`
