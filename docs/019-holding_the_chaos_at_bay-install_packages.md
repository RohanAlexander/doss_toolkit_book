


# Installing packages

*Written by Haoluan Chen and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to install packages from CRAN.

Prerequisite skills include:

- setup RStudio
- run R code in the console

Highlights:

- What is a package in R
- What is CRAN
- Install package from CRAN using `install.packages("package_name")` or `install.packages('package_name')`
- Install package in RStudio

## What is a package?

R packages are collections of functions or datasets developed by the community. It is shared by the author and allows everyone to re-use. It increases and expands the tools we can use in R for various tasks, including graph generation, data manipulation, and statistical inference.

## What is CRAN?

CRAN stands for Comprehensive R Archive Network. It is the official repository where the packages are located, and you can install them on your computer. All the package in CRAN needs to pass several tests that ensure the package is following CRAN policies. As of June 2019, there were over 14,000 packages available on the CRAN. 

## How to install a package?

To install a package from CRAN, you can either run `install.package("**package_name**")` or manually install it in RStudio. 

## Using code

For example, you may want to install the ggplot2 package. (ggplot2 is a useful data visualization package in r you are likely to use them in the future)

To install, you run the following code in the r chunk or the console:


```r
install.packages("ggplot2")
```

After running this code, you will receive some message on the console, and it will start installing the package (this may take a few minutes depending on your system). Then it will tell you that you have successfully installed the package.

Note that for some package it may ask you to input something in the console to complete the installation. You will see this in the installing package from GitHub tutorial.

<iframe width="560" height="315" src="https://www.youtube.com/embed/c-8qOcLyxN4" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## In RStudio 

<iframe width="560" height="315" src="https://www.youtube.com/embed/D8A3Em5WFwU" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Exercises

### Exercise 1

<!-- ```{r cranex1, echo = FALSE} -->
<!-- question("Which code can install the `tidyverse` package?", -->
<!--           answer("packages(tidyverse)"), -->
<!--           answer("install.packages(tidyverse)"), -->
<!--           answer("install.packages('tidyverse')", correct = TRUE), -->
<!--           answer("install.package('tidyverse')"), -->
<!--           allow_retry = TRUE) -->

<!-- ``` -->



### Exercise 2

Please install the `tidyverse` package on your computer.

<iframe width="560" height="315" src="https://www.youtube.com/embed/COFCB-MGaHw" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## Common mistakes and errors

- You have misspelled the package name.
- You missed the quotation mark around the package name.
- You missed the s in the install_packages function.


## Next steps

For the next step, you can install the package from CRAN and start using them for your projects. 

Here is a list of useful packages you may be using:

- `ggplot2` (create graphics)
- `dplyr` (data manipulation)
- `readr` (read data files)
- `tidyverse` (include packages you are likely to use everyday data analyses. Including all three packages above and more!)
- `tidytext` (text mining package)
- `glmnet` (Regularized generalized linear models)
- `learnr` (create interactive tutorial for R just like this one)

You can also create your own packages! 

## Exercises

### Question 1
What is a package
    a.  Collections of functions or datasets developed by the community
    b. Built in functions or datasets in R
    c. A set of file to store your code 


### Question 2
CRAN is the official repository where the packages are located, and you can install them on your computer.
    a.  True  
    b. False

### Question 3
Why do we want to use packages?
    a. No, we should not use other people's package
    b. It helps us to run R more smoothly
    c.  It increases and expands the tools we can use in R for various tasks
    d. To have better user interface in R-studio
    
### Question 4
Can you install packages in the R-studio console?
    a.  Yes
    b. No

### Question 5
Can you install packages in the packages tab on the right side of R-studio?
    a.  Yes
    b. No
    
### Question 6
Which code can install the `tidyverse` package?
    a. `packages(tidyverse)`
    b. `install.packages(tidyverse)`
    c.  `install.packages('tidyverse')`
    d. `install.package('tidyverse')`   
### Question 7
You can create your own packages
    a.  True
    b. False

### Question 8
`dplyr` is a data visualization package.
    a.  True
    b. False

### Question 9
Does `install.packages("dplyr")` work? 
    a.  Yes
    b. No
    
### Question 10
Does `install.packages(tidyverse)` work?
    a. Yes
    b.  No

