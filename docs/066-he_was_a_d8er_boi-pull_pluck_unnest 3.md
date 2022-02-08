


# pull, pluck and unnest

*Written by Isaac Ehrlich and last updated on 7 October 2021.*

## Introduction

Indexing, manipulating, or handling data frames and tibbles can be messy and tricky, especially when these objects are organized in complex data structures. Tidyverse functions `pull()`, `pluck()`, and, `unnest()` can make dealing with these data structures easier and neater. 

In this lesson, you will learn how to:

- Use `pull()` to access a single column of a data frame
- Use `pluck()` for deep indexing and to access elements of data structures
- Use `unnest()` to flatten data frames


Prerequisite skills include:

- Knowledge of tibbles and other data structures
- Knowledge of indexing using special characters such as `[]` and `$`


## pull()
`pull()` is essentially the `$` indexing operator formatted as a function, allowing for neat indexing of data frames. As input, `pull()` takes the data frame, as well as `var`, which is information on the element you want to extract. `var` can either be the name of the column or an index. If the index is negative, `pull()` will count the indices from the right side (i.e. `var = 1` will pull the first column and `var = -1` will pull the last).

Let's take a look at some examples using a Caribou Location Tracking data set.

### Examples

```r
# Load csv file
locations <- read_csv("https://raw.githubusercontent.com/tacookson/data/master/caribou-location-tracking/locations.csv", n_max = 1000)

# Extract the 'event_id' column
event_id_col <- locations %>% pull(var = "event_id")

# We can do this with positive and negative indexing as well
# event_id is the first column out of 7
event_id_pos_idx <- locations %>% pull(var = 1)
event_id_neg_idx <- locations %>% pull(var = -7)

# Verify positive and negative indexing returned the same column using 'table()'
table(event_id_pos_idx == event_id_neg_idx)
#> 
#> TRUE 
#> 1000
```


## pluck()
`pluck()` is similar to `pull()`, but is more robust, and can handle complex data structures, such as lists of data frames. While `pull()` takes only one input to specify a column, `pluck()` can accept multiple, and therefore also allows for neat and flexible indexing of deep data structures. Similar to `pull()`, the output of `pluck` can also be achieved using traditional indexing, but `pluck()` is often simpler to use, and may make your code more readable.

The main arguments of `pluck()` are the data structure that contains the elements you want to access, and then the elements themselves. If the element does not exist, `pluck()` by default will return `NULL`, though this can be changed by adjusting the `.default` argument.

Let's take a look at some examples using multiple data sets on Broadway Weekly Grosses. 

### Examples

The simplest use of `pluck()` is in place of `pull()` - to extract a single column from a data frame object. Without using `pull()`, `[]`, or `$` to index, let's extract the `weekly_gross` column from the following file.

```r
# Load data
grosses <- read_csv("https://raw.githubusercontent.com/tacookson/data/master/broadway-grosses/grosses.csv", n_max = 1000)

# Use 'pluck()' to access a single column
weekly_gross_col <- grosses %>% pluck("weekly_gross")

# This can also be done using indices rather than column names
weekly_gross_idx <- grosses %>% pluck(6)

# Use 'table()' to verify the outputs are the same
table(weekly_gross_col == weekly_gross_idx)
#> 
#> TRUE 
#> 1000
```

`pluck()` can similarly use indices to grab elements of vectors and lists.

```r
# Create list and grab the fourth element
letters <- list("a", "b", "c", "d", "e")
element <- letters %>% pluck(4)
element
#> [1] "d"
```


However, because `pluck()` can take multiple arguments, it is also capable extracting columns from more complex data structures, such as a list of data frames. This is often referred to as "deep indexing" - indexing that requires multiple index calls, brackets, or elements. Let's download a few more data frames and see how this works.

```r
# Load data
grosses <- read_csv("https://raw.githubusercontent.com/tacookson/data/master/broadway-grosses/grosses.csv", n_max = 1000)
early_starts <- read_csv("https://raw.githubusercontent.com/tacookson/data/master/broadway-grosses/pre-1985-starts.csv", n_max = 1000)
synopses <- read_csv("https://raw.githubusercontent.com/tacookson/data/master/broadway-grosses/synopses.csv", n_max = 1000)

# Create list of data frames
broadway_data <- list(grosses, early_starts, synopses)

# Select `synopsis` column from `synopses` table
synopsis_col <- broadway_data %>% pluck(3, "synopsis")

# Use table() to verify the output is correct
table(synopsis_col == broadway_data[[3]][,2])
#> 
#> TRUE 
#>  835
```
Similarly, `pluck()` can be used for other data structures like lists of lists as well.

## `unnest()`
The main purpose of `unnest()` is to flatten existing data frames. Like `pluck()`, `unnest()` handles complex data structures, but these complex structures are now made up of lists (or other structures) contained within a single data frame (known as list-columns). In other words, if a column of a data frame contains other data structures, such as other tibbles, `unnest()` can flatten the data frame to remove these structures.

The arguments that `unnest()` takes are the data frame, as well as the columns to flatten, or unnest. For additional arguments, see documentation. 

Let's construct some toy data frames and take look at some examples.

### Examples
Even without nesting tibbles within tibbles, `unnest()` can be used in cases such as flattening long strings using `strsplit()` or other functions.

```r
# Create toy data
# Even though the 'color' and 'shades' column are of the same length, we can see that two entries in the 'shades' column contain elements separated by a comma
color_shades <- tibble(color = c("red", "orange", "yellow"), shades = c("red,cherry,scarlet", "orange,apricot", "yellow"))
head(color_shades)
#> # A tibble: 3 × 2
#>   color  shades            
#>   <chr>  <chr>             
#> 1 red    red,cherry,scarlet
#> 2 orange orange,apricot    
#> 3 yellow yellow


# We can use 'strsplit()' to unnest the elements in the shades column
color_shades <- color_shades %>% unnest(shades = strsplit(shades, ","))
head(color_shades)
#> # A tibble: 6 × 2
#>   color  shades 
#>   <chr>  <chr>  
#> 1 red    red    
#> 2 red    cherry 
#> 3 red    scarlet
#> 4 orange orange 
#> 5 orange apricot
#> 6 yellow yellow
```


However, `unnest()` is typically meant to be used with lists-columns held within data frames.

```r
# Create toy data
# 'rgb' column is a list of tibbles containing rgb values
color_rgb <- tibble(
  color = c("red", "orange", "yellow"),
  rgb = list(
    tibble(r = 255, g = 0, b = 0),
    tibble(r = 255, g = 70, b = 0),
    tibble(r = 255, g = 255, b = 0)
  )
)
head(color_rgb)
#> # A tibble: 3 × 2
#>   color  rgb             
#>   <chr>  <list>          
#> 1 red    <tibble [1 × 3]>
#> 2 orange <tibble [1 × 3]>
#> 3 yellow <tibble [1 × 3]>

# Flatten the 'rgb' column to create a column for each color component
color_rgb <- color_rgb %>% unnest(rgb)
head(color_rgb)
#> # A tibble: 3 × 4
#>   color      r     g     b
#>   <chr>  <dbl> <dbl> <dbl>
#> 1 red      255     0     0
#> 2 orange   255    70     0
#> 3 yellow   255   255     0
```
We can see that once the rgb column is unnested, it is easier to read and grab each component individually.

## Practice questions


<!-- ```{r pullq1, echo = FALSE} -->
<!-- question("Using a negative index in 'pull()' will", -->
<!-- answer("return an error"), -->
<!-- answer("create a new column"), -->
<!-- answer("return NULL"), -->
<!-- answer("index from the right side instead of the left", correct = TRUE), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

<!-- ```{r pullq2, echo = FALSE} -->
<!-- question("'pull()' and 'pluck()' perform functions no other operators in R are capable of", -->
<!-- answer("True", message = "Remember there are many ways to index!"), -->
<!-- answer("False", correct = TRUE, message = "Correct! Using 'pull()' and 'pluck()' is mostly a stylistic choice, but they are great for pipes and can definitely make your code neater!"), -->
<!-- allow_retry = TRUE) -->

<!-- ``` -->

<!-- ```{r pullq3, echo = FALSE} -->
<!-- question("Which of the following are true?", -->
<!-- answer("'pluck()' is a robust alternative to 'pull()' - it can handle complex data structures", correct = TRUE), -->
<!-- answer("'pull()' is a robust alternative to 'pluck()' - it can handle complex data structures"), -->
<!-- answer("'pull()' takes in one index argument ('var') as input", correct = TRUE), -->
<!-- answer("'pluck()' can take multiple index arguments as input", correct = TRUE), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

## Practice coding
It's your turn to try! In the code below, we've created a complex data structure, where `colors` is a list of the data frames `red`, `orange`, and `yellow`, where `yellow` also has nested data frames. See if you can complete the following questions!

```r
red <- tibble(shade = c("brick", "bright", "burgundy", "cardinal", "cherry"),
              r = c(170, 238, 128, 196, 210),
              g = c(74, 75, 0, 30, 4),
              b = c(68, 43, 32, 58, 45))
orange <- tibble(shade = c("papaya", "coral", "dark", "apricot", "topaz"),
              r = c(255, 255, 255, 251, 255),
              g = c(239, 127, 140, 206, 200),
              b = c(213, 80, 0, 177, 124))
yellow <- tibble(shade = c("amber", "brass", "bright", "canary", "cream"),
                 rgb = list(tibble(r = 255, g = 191, b = 0),
                            tibble(r = 225, g = 193, b = 110),
                            tibble(r = 255, g = 234, b = 0),
                            tibble(r = 255, g = 255, b = 143),
                            tibble(r = 255, g = 253, b = 208)))


colors <- list(red, orange, yellow)
```

**1. Use `pull()` to extract the `shade` column from the `red` data frame**

<!-- ```{r pull-coding1, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r pull-coding1-solution} -->
<!-- red %>% pull(shade) -->
<!-- # OR -->
<!-- red %>% pull(1) -->
<!-- # OR -->
<!-- red %>% pull(-4) -->
<!-- ``` -->

<!-- **2. Use `pluck()` to extract the `shade` column from the `red` data frame from within the `colors` list** -->
<!-- ```{r pull-coding2, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r pull-coding2-solution} -->
<!-- colors %>% pluck(1, "shade") -->
<!-- ``` -->

<!-- **3. Use `pluck()` to extract the yellow data frame, and then use `pull()` to grab just the `b` column. Remember that the `yellow` data frame has a nested tibble so you may have to use `unnest()`! -->
<!-- ```{r pull-coding3, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r pull-coding3-solution} -->
<!-- colors %>% pluck(3) %>% unnest(rgb) %>% pull(b) -->
<!-- ``` -->

## Overview and Next Steps
- `pull()` allows for a simple way to extract single columns from data frames
- `pluck()` performs similar functions as `pull()` but is also capable of handling complex data structures, such as lists of data frames (and lists of lists of data frames, and lists of lists of lists of data frames and...) 
- Although the use of `pull()` and `pluck()` is generally a stylistic choice, these functions let you avoid multiple special characters like `[[]]` and `$` and can make your code neater too!
- `unnest()` flattens data frames that contain other lists or data frames (known as list-columns)

In the next lesson, we will continue looking into different ways of storing and handling data in R - this time with factors!



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
