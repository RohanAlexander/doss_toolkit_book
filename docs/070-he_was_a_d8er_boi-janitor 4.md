


# janitor

*Written by Mariam Walaa and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- Tidy up variable names that are in your dataset
- Deal with duplicate or partially duplicate data

Prerequisite skills include:

- Installing and loading packages
- Understanding duplicate data
- Working with column names, such as `names()` and `rename()`

Highlights:

- You can make column names cleaner using janitors clean_names() function
- You can handle duplicate or partially duplicate data using janitors get_dupes() function

## Overview

> "The [janitor](https://garthtarr.github.io/meatR/janitor.html) package is a R package
that has simple functions for examining and cleaning dirty data. The main janitor
functions: perfectly format data frame column names; isolate partially-duplicate records;
and provide quick tabulations (i.e., frequency tables and crosstabs)."

As the description says, the `janitor` package will help you with cleaning your data. 
It is not part of the `tidyverse` so you will have to install it and then load it 
separately as follows.


```r
library(janitor)
#> 
#> Attaching package: 'janitor'
#> The following objects are masked from 'package:stats':
#> 
#>     chisq.test, fisher.test
```

In data analysis, you will frequently across across the issue of duplication, as well as 
the issue of having difficult column names to work with. One way to deal with difficult
column names is to rename them using `rename()` but you can also use the janitor package
to perform multiple cleaning steps on the column names.

## Arguments

## `clean_names()`

The `clean_names()` function takes the following as arguments:

| Argument | Parameter            | Details                                        |
| -------- | -------------------- | ---------------------------------------------- |
| dat*     | input data frame     |                                                |
| case     | 'title' for big caps | default is 'snake'; see to_any_case for detail |

You can read more about the arguments in the `clean_names()` function documentation
[here](https://garthtarr.github.io/meatR/janitor.html#clean_names()).

## `get_dupes()`

The `get_dupes()` function takes the following as arguments:

| Argument | Parameter        | Details                                         |
| -------- | ---------------- | ----------------------------------------------- |
| dat*     | input data frame |                                                 |
| …        | vector           | vector containing column names we want to check |

You can read more about the arguments in the `get_dupes()` function documentation
[here](https://garthtarr.github.io/meatR/janitor.html#get_dupes()).

## Exercises

Lets start by loading `tidyverse` since we will be using the pipe %>% operator and more.


```r
library(tidyverse)
```



Consider this small dataset of grades.


```r
grades
#> # A tibble: 5 × 4
#>   `Student Initials` `Grade Midterm 1` `Grade Midterm 2`
#>   <chr>                          <dbl>             <dbl>
#> 1 AH                               100                90
#> 2 AE                                86                83
#> 3 HS                                90                79
#> 4 ES                                64                64
#> 5 BT                               100                90
#> # … with 1 more variable: Final Grade % <dbl>
```

Using the `clean_names()` function from janitor, we get:


```r
grades %>% clean_names()
#> # A tibble: 5 × 4
#>   student_initials grade_midterm_1 grade_midterm_2
#>   <chr>                      <dbl>           <dbl>
#> 1 AH                           100              90
#> 2 AE                            86              83
#> 3 HS                            90              79
#> 4 ES                            64              64
#> 5 BT                           100              90
#> # … with 1 more variable: final_grade_percent <dbl>
```

Notice how now everything is lowercased with _ as a separator, and any special characters
like % are converted to words to retain their meaning. `clean_names()` would also handle
column names that are duplicated, but that is not demonstrated here since we already had
unique columns.

### Exercise 1

If, for some reason, you wanted to preserve some existing columns from being cleaned, how
would you use the `clean_names()` function on only the columns you want to clean? For
example, supposed you wanted to keep the Final Grade % column as is. As a hint, you will
need to use functions outside of the janitor package to help with this. Remember the
`dplyr` functions.




```r
grades %>%
  select(-`Final Grade %`) %>%
  clean_names()
#> # A tibble: 5 × 3
#>   student_initials grade_midterm_1 grade_midterm_2
#>   <chr>                      <dbl>           <dbl>
#> 1 AH                           100              90
#> 2 AE                            86              83
#> 3 HS                            90              79
#> 4 ES                            64              64
#> 5 BT                           100              90
```


### Exercise 2

If you wanted to restore the upper casing for some columns, how would you do that? As a
tip, take a look at the Arguments section and see what you can use. Make sure you store
the cleaned data from above in an object called clean, and then apply the new cleaning
step to it.

<!-- ```{r janitor-exercise-2, exercise = TRUE} -->
<!-- clean <-  -->
<!-- clean %>% -->
<!-- ``` -->

<!-- ```{r janitor-exercise-2-solution, exercise = FALSE} -->
<!-- clean <- grades %>% clean_names() -->
<!-- clean %>% clean_names(case = "title") -->
<!-- ``` -->


### Exercise 3

Try using the `get_dupes()` function to get duplicate rows from the cleaned grades data
`clean`.



<!-- ```{r janitor-exercise-3, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r janitor-exercise-3-solution, exercise = FALSE} -->
<!-- clean %>% get_dupes() -->
<!-- ``` -->

What was the result? Did you get anything?

### Exercise 4

Look at the data above and try to see why you did not get anything even though it looks
like two rows are very similar. How can you modify the function call so that you get the
_partially_ duplicate data?

<!-- ```{r janitor-exercise-4, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r janitor-exercise-4-solution, exercise = FALSE} -->
<!-- clean %>% get_dupes(c("grade_midterm_1", "grade_midterm_2", "final_grade_percent")) -->
<!-- ``` -->



## Next Steps

If you would like to learn more, please read about the janitor package in its
documentation [here](https://garthtarr.github.io/meatR/janitor.html).




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
