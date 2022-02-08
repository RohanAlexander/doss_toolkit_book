


# names, rbind and cbind

*Written by Isaac Ehrlich and last updated on 7 October 2021.*

## Introduction

For certain tasks, you may need to combine data frames and find information about them.

In this lesson, you will learn how to

* Use `names()` to find the column names of data frames
* Use `rbind()` to combine two or more data frames (or matrices) by row
* Use `cbind()` to combine two or more data frames (or matrices) by column

Prerequisites:

* Understanding how to data frames and their basic principles

## Arguments

### `names()`

The primary purpose of `names()` is to return the column names of a data frame. The only argument that `names()` takes is the data frame. `colnames()` is a similar function which outputs the same information, and works for matrices as well.


```r
head(starwars)
#> # A tibble: 6 × 14
#>   name          height  mass hair_color skin_color eye_color
#>   <chr>          <int> <dbl> <chr>      <chr>      <chr>    
#> 1 Luke Skywalk…    172    77 blond      fair       blue     
#> 2 C-3PO            167    75 <NA>       gold       yellow   
#> 3 R2-D2             96    32 <NA>       white, bl… red      
#> 4 Darth Vader      202   136 none       white      yellow   
#> 5 Leia Organa      150    49 brown      light      brown    
#> 6 Owen Lars        178   120 brown, gr… light      blue     
#> # … with 8 more variables: birth_year <dbl>, sex <chr>,
#> #   gender <chr>, homeworld <chr>, species <chr>,
#> #   films <list>, vehicles <list>, starships <list>
names(starwars)
#>  [1] "name"       "height"     "mass"       "hair_color"
#>  [5] "skin_color" "eye_color"  "birth_year" "sex"       
#>  [9] "gender"     "homeworld"  "species"    "films"     
#> [13] "vehicles"   "starships"
table(colnames(starwars) == names(starwars))
#> 
#> TRUE 
#>   14
```

Using indexing, `names()` can also be used to change the column names of a data frame.


```r
# Change the homeworld column name (the tenth column) to home-planet
names(starwars)[10] <- "home-planet"
names(starwars)
#>  [1] "name"        "height"      "mass"        "hair_color" 
#>  [5] "skin_color"  "eye_color"   "birth_year"  "sex"        
#>  [9] "gender"      "home-planet" "species"     "films"      
#> [13] "vehicles"    "starships"
```

The tidyverse `rename()` function can also be used to change column names, and avoids indexing by specifying the column to rename, using the syntax `new_name = old_name`.


```r
# Change the starships column name to spaceships
starwars <- 
  starwars %>% 
  rename(spaceships = starships)
names(starwars)
#>  [1] "name"        "height"      "mass"        "hair_color" 
#>  [5] "skin_color"  "eye_color"   "birth_year"  "sex"        
#>  [9] "gender"      "home-planet" "species"     "films"      
#> [13] "vehicles"    "spaceships"
```
 

### `rbind()`

The purpose of `rbind()` is to combine two (or more) data frames by row. The arguments to `rbind()` are two (or more) data frames. These data frames must have the same number of columns, and must have the same column names as well. `rbind()` can also be used to combine matrices which match the same requirements.


```r
letter_df <- data.frame(numbers = 1:26, strings = letters)
words_df <- data.frame(numbers = 27:1006, strings = words)

character_df <- rbind(letter_df, words_df)
names(character_df)
#> [1] "numbers" "strings"
dim(character_df) # shows the number of rows and columns
#> [1] 1006    2
```

### `cbind()`

The purpose of `cbind()` is to combine two (or more) data frames by column. The arguments to `cbind()` are two (or more) data frames. These data frames must have the same number of rows, or the number of rows must be multiples of one another. `cbind()` can also be used to combine matrices which match the same requirements. 

Note, in the case that the number of rows are multiples, the rows in the smaller data frame are repeated so they match the longer data frame.


```r
index_df <- data.frame(numbers = 1:5, letters = c("a", "b", "c", "d", "e"))
names_df <- data.frame(vegetables = c("arugula", "broccoli", "cauliflower", "dill", "endive"),
                       fruits = c("apricot", "banana", "cherry", "date", "elderberry"),
                       flowers = c("aster", "begonia", "crocus", "daffodil", "echium"))

combined_df <- cbind(index_df, names_df)
names(combined_df)
#> [1] "numbers"    "letters"    "vegetables" "fruits"    
#> [5] "flowers"
dim(combined_df) # shows the number of rows and columns
#> [1] 5 5
```


## Questions and Exercises

### Question 1

Using the `presidential` data frame, save the column names, and then change the name of the second column to `inauguration-date`.


```
#> [1] "name"  "start" "end"   "party"
```


```r
presidential_col_names <- names(presidential)

names(presidential)[2] <- "inauguration-date"
```


### Question 2




<!-- ```{r rbind-q2, echo = FALSE} -->
<!-- question("If you were to rbind() a data frame to itself, ", -->
<!-- answer("the number of columns would double"), -->
<!-- answer("the number of rows would double", correct = TRUE), -->
<!-- answer("both the number of rows and the number of columns would double"), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

<!-- #### Question 3 -->

<!-- ```{r rbind-q3, echo = FALSE} -->
<!-- question("Select the following true statements about rbind() arguments", -->
<!-- answer("The data frames must have the same number of columns", correct = TRUE), -->
<!-- answer("The data frames must have the same number of rows"), -->
<!-- answer("The column names of the data frames must be the same", correct = TRUE), -->
<!-- answer("The data frames must have the same name"), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

<!-- #### Question 4 -->

<!-- Bind the `presidential` data set to itself using `rbind()`. -->

<!-- ```{r rbind-q4, echo = FALSE, exercise = TRUE} -->
<!-- # Enter your code below -->

<!-- # double_presidential <-  -->

<!-- dim(presidential) -->
<!-- # dim(double_presidential) -->
<!-- ``` -->

<!-- ```{r rbind-q4-solution} -->
<!-- double_presidential <- rbind(presidential, presidential) -->
<!-- ``` -->


<!-- #### Question 5 -->

<!-- ```{r cbind-q5, echo = FALSE} -->
<!-- question("If you were to cbind() a data frame to itself, ", -->
<!-- answer("the number of columns would double", correct = TRUE), -->
<!-- answer("the number of rows would double"), -->
<!-- answer("both the number of rows and the number of columns would double"), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

<!-- #### Question 6 -->

<!-- Bind the `presidential` data set to itself using `cbind()`. -->

<!-- ```{r cbind-q6, echo = FALSE, exercise = TRUE} -->
<!-- # Enter your code below -->

<!-- double_presidential <- -->

<!-- dim(presidential) -->
<!-- # dim(double_presidential) -->
<!-- ``` -->

<!-- ```{r cbind-q6-solution} -->
<!-- double_presidential <- cbind(presidential, presidential) -->
<!-- ``` -->

## Special Cases & Common Mistakes

The most common error with `rbind()` and `cbind()` occurs when the data frames do not meet the requirements (e.g. data frames have different number of columns for `rbind()` or different number of rows for `cbind()`). These will result in error messages such as "numbers of columns of arguments do not match" or "arguments imply differing number of rows". 

Similarly, if the names of the columns do not match, `rbind()` will give a "names do not match previous names" error. You can use `names()` to check against this error.


## Overview & Next Steps

`names()` will return the column names of data frames and can be used to change column names as well. `rbind()` and `cbind()` combine data frames either by row or by column.

In the next section, we will continue learning how to manipulate data frames.



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
