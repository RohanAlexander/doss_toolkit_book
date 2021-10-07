


# rename

*Written by Mariam Walaa and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- Rename columns in a data frame

Prerequisite skills include:

- Using the pipe %>% operator

Highlights:

- We can rename multiple columns in a dataframe at once using `rename()`.
- It is helpful to rename columns into something simpler and clearer.
- We can name columns that do not already have a name using `rename()`.

## Arguments

The `rename()` function takes the following as arguments:

| Argument | Parameter | Details                                                           |
|----------|-----------|-------------------------------------------------------------------|
| x        | object    | this is the data with variables to rename (typically a data frame)|
| replace  | vector    | this takes a vector as c(new_name = old_name)                     |

You can read more about the arguments in the `rename()` function documentation
[here](https://www.rdocumentation.org/packages/plyr/versions/1.8.6/topics/rename).

## Overview

Sometimes we have to work with data sets with columns that are difficult to understand or
work with. In this case, we can rename the columns using the `rename()` function.
In this tutorial, we will be using a data set about fictional character personalities for
reference. This data set already consists of simple, clear, and well-named variables, but
we are going to try to simplify them even further using `rename()`.

We will start by loading the data from GitHub.


```r
library(tidyverse)
```

We will also load the personalities dataset.



```r
personalities <- read_tsv(
  "https://raw.githubusercontent.com/tacookson/data/master/fictional-character-personalities/personalities.txt")
#> Rows: 213600 Columns: 11
#> ── Column specification ────────────────────────────────────
#> Delimiter: "\t"
#> chr (7): character_code, fictional_work, character_name,...
#> dbl (3): mean, ratings, sd
#> lgl (1): is_emoji
#> 
#> ℹ Use `spec()` to retrieve the full column specification for this data.
#> ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


Here is the dataset. This data consists of 213,600 rows, each representing a fictional 
character, and 11 columns describing the character and their personality.


```r
glimpse(personalities)
#> Rows: 213,600
#> Columns: 11
#> $ character_code <chr> "A/4", "A/4", "A/4", "A/4", "A/4", …
#> $ fictional_work <chr> "Alien", "Alien", "Alien", "Alien",…
#> $ character_name <chr> "Ash", "Ash", "Ash", "Ash", "Ash", …
#> $ gender         <chr> "male", "male", "male", "male", "ma…
#> $ spectrum       <chr> "BAP1", "BAP2", "BAP3", "BAP4", "BA…
#> $ spectrum_low   <chr> "playful", "shy", "cheery", "mascul…
#> $ spectrum_high  <chr> "serious", "bold", "sorrowful", "fe…
#> $ is_emoji       <lgl> FALSE, FALSE, FALSE, FALSE, FALSE, …
#> $ mean           <dbl> 41.4, 11.1, 22.4, -16.9, 23.1, 3.8,…
#> $ ratings        <dbl> 51, 63, 78, 71, 72, 60, 76, 74, 72,…
#> $ sd             <dbl> 10.9, 27.3, 14.0, 22.3, 25.2, 32.9,…
```

We can see that the first three columns are about the character unique ID, the fictional
work that they are from, and their name. To demonstrate the use of the rename function, 
we will rename each of these three variables to one word each.


```r
personalities <- personalities %>%
  rename(id = character_code,
         work = fictional_work,
         name = character_name)
```

We have renamed 3 columns in the data frame and re-assigned it to `personalities`.


```r
glimpse(personalities)
#> Rows: 213,600
#> Columns: 11
#> $ id            <chr> "A/4", "A/4", "A/4", "A/4", "A/4", "…
#> $ work          <chr> "Alien", "Alien", "Alien", "Alien", …
#> $ name          <chr> "Ash", "Ash", "Ash", "Ash", "Ash", "…
#> $ gender        <chr> "male", "male", "male", "male", "mal…
#> $ spectrum      <chr> "BAP1", "BAP2", "BAP3", "BAP4", "BAP…
#> $ spectrum_low  <chr> "playful", "shy", "cheery", "masculi…
#> $ spectrum_high <chr> "serious", "bold", "sorrowful", "fem…
#> $ is_emoji      <lgl> FALSE, FALSE, FALSE, FALSE, FALSE, F…
#> $ mean          <dbl> 41.4, 11.1, 22.4, -16.9, 23.1, 3.8, …
#> $ ratings       <dbl> 51, 63, 78, 71, 72, 60, 76, 74, 72, …
#> $ sd            <dbl> 10.9, 27.3, 14.0, 22.3, 25.2, 32.9, …
```

Now we have a data frame with renamed columns.

What if we have a column that does not have a name? We can still name it by indexing the
column using base R function `names()`.


```r
personalities %>%
  rename(fictional_work = names(.)[2])
#> # A tibble: 213,600 × 11
#>    id    fictional_work name  gender spectrum spectrum_low
#>    <chr> <chr>          <chr> <chr>  <chr>    <chr>       
#>  1 A/4   Alien          Ash   male   BAP1     playful     
#>  2 A/4   Alien          Ash   male   BAP2     shy         
#>  3 A/4   Alien          Ash   male   BAP3     cheery      
#>  4 A/4   Alien          Ash   male   BAP4     masculine   
#>  5 A/4   Alien          Ash   male   BAP5     charming    
#>  6 A/4   Alien          Ash   male   BAP6     lewd        
#>  7 A/4   Alien          Ash   male   BAP7     intellectual
#>  8 A/4   Alien          Ash   male   BAP8     strict      
#>  9 A/4   Alien          Ash   male   BAP9     refined     
#> 10 A/4   Alien          Ash   male   BAP10    trusting    
#> # … with 213,590 more rows, and 5 more variables:
#> #   spectrum_high <chr>, is_emoji <lgl>, mean <dbl>,
#> #   ratings <dbl>, sd <dbl>
```

Here, we change the work column back to fictional_work simply by indexing the second
column in the personalities data frame. This column already had a name, but if it did not,
this method would have still successfully named it to fictional_work.

## Exercises

### Exercise 1

Rename the `personalities` data back to its original column names.

<!-- ```{r rename-exercise-1, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r rename-exercise-1-hint-1} -->
<!-- # You don't have to assign it to an object -->
<!-- ``` -->

<!-- ```{r rename-exercise-1-sol, echo = FALSE} -->
<!-- rename_ex_sol <- personalities %>% -->
<!--   rename(character_code = id, -->
<!--          fictional_work = work, -->
<!--          character_name = name) -->
<!-- ``` -->


<!-- ```{r rename-exercise-1-check} -->
<!-- grade_result(pass_if(~identical(.result, rename_ex_sol))) -->
<!-- ``` -->

### Exercise 2

<!-- ```{r rename-exercise-2, echo = FALSE} -->
<!-- question("Which of these are true? Check all true statements.", -->
<!--          answer("You can rename multiple columns using `rename()`.", correct = TRUE), -->
<!--          answer(paste("When you use `rename()`, you pass column name pairs as follows: ", -->
<!--          "`c(old_name = new_name)`"), message = "You pass the new column name first."), -->
<!--          answer("The `rename()` function is used to rename data frames.", -->
<!--                 message = "The `rename()` function is used to rename columns in a data frame."), -->
<!--          answer("The `rename()` function renames columns by name.", correct = TRUE), -->
<!--          allow_retry = TRUE, -->
<!--          random_answer_order = TRUE) -->
<!-- ``` -->

## Common Mistakes & Errors

Below are some common mistakes and errors you may come across:

- You pass the old name first instead of the new name. The syntax requires passing the new 
column name, followed by an equal sign, and then the old column name.
- You are not correctly typing the name.
- You are not using the correct quotation marks. For example, if you have whitespace 
between words in the column name, you need to use `` as opposed to the other quotation
marks.

If you have other issues, check that you have loaded tidyverse or dplyr into your session!
Remember that a lot of issues can come from not loading the required packages.

## Next Steps

If you would like to read more about the `rename()` function, here are some additional
resources you may find helpful:

- [R Documentation for
`rename()`](https://www.rdocumentation.org/packages/plyr/versions/1.8.6/topics/rename)


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
