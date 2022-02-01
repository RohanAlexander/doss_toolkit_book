


# Pivoting data from long to wide and vice versa

*Written by Annie Collins and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- Use the function `pivot_wider()` to manipulate a data frame or tibble.
- Use the function `pivot_longer()` to manipulate a data frame or tibble.

This lesson is a yellow level skill and is part of "Tidyverse Essentials". Prerequisite skills include:

- Installing packages
- Calling libraries
- Importing data

## pivot_longer()

`pivot_longer()` takes the inputted dataset and makes it **longer** by rearranging its data to **increase the number of rows** and **decrease the number of columns**. Here, we consider "longer" in the vertical sense -- a "longer" dataset has a larger number of cells from top to bottom than a "shorter" dataset.

### Introductory Example

This dataset (called `games`) contains a list of NBA teams and their win/loss record over the course of 10 games.


```
#>                   teams gm1 gm2 gm3 gm4 gm5
#> 1       Toronto Raptors   l   l   w   w   w
#> 2    Los Angeles Lakers   l   w   w   l   w
#> 3        Boston Celtics   w   l   l   l   w
#> 4 Golden State Warriors   l   w   l   l   w
#> 5            Miami Heat   l   l   w   w   l
```

Observe the effect the following code has on the data set. Take note of the difference in the number of rows and columns between the two tables. This will be visualized and explained in greater detail in the following step.



```r
pivot_longer(games, cols = c(gm1, gm2, gm3, gm4, gm5), names_to = "game number", values_to = "status")
#> # A tibble: 25 × 3
#>    teams              `game number` status
#>    <chr>              <chr>         <chr> 
#>  1 Toronto Raptors    gm1           l     
#>  2 Toronto Raptors    gm2           l     
#>  3 Toronto Raptors    gm3           w     
#>  4 Toronto Raptors    gm4           w     
#>  5 Toronto Raptors    gm5           w     
#>  6 Los Angeles Lakers gm1           l     
#>  7 Los Angeles Lakers gm2           w     
#>  8 Los Angeles Lakers gm3           w     
#>  9 Los Angeles Lakers gm4           l     
#> 10 Los Angeles Lakers gm5           w     
#> # … with 15 more rows
```

## Visualizing pivot_longer()

This video will guide you through the changes that occur when applying `pivot_longer()` to our dataset.

<iframe width="560" height="315" src="https://www.youtube.com/embed/OBsQA0vyxNA" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## pivot_longer() Arguments

Now let's get a bit more specific. 

You just executed the command `pivot_longer(data = games, cols = c(gm1, gm2, gm3, gm4, gm5), names_to = "game number", values_to = "status")`. What do each of the arguments within the brackets mean?

- **data**: the name of our dataframe, in this case `games`.

- **cols**: the names of the columns that will be "pivoting" or changing into a longer format. *In our example, we select all columns representing a single game, which are columns "gm1" through "gm5". We could have also written `!teams` (all columns except "teams") or `starts_with("gm")` (all the columns with a name that starts with "gm")*.

- **names_to**: a new name for the column that will be created from the former column names in **cols**. After pivoting, the former distinct columns are now all stored within one column themselves, and this argument lets you give this adjusted column a descriptive new name. If left blank, the new column name will automatically be set to "names". *In our example, we named the column "game number" since it contains "gm1" through "gm5"*.

- **values_to**: similar to **names_to**, this represents a new name for the column created for the data that was originally stored in each individual cell. If left blank, the new column name will automatically be set to "values". *In our example, we set the name to "status" since the column contains information representing each team's win or loss outcome for a given game*.


## pivot_wider()

`pivot_wider()` takes the inputted dataset and makes it **wider** by rearranging its data to **decrease the number of rows** and **increase the number of columns**. `pivot_wider()` is essentially the inverse of `pivot_longer()` - the two transformations can be used to switch a data frame back and forth between its "longer" and "wider" forms.

### Introductory Example

This is a dataset called `games_long`, a "longer" version of `games` (the result of applying `pivot_longer()` to the original data frame).


```
#> # A tibble: 25 × 3
#>    teams              `game number` status
#>    <chr>              <chr>         <chr> 
#>  1 Toronto Raptors    gm1           l     
#>  2 Toronto Raptors    gm2           l     
#>  3 Toronto Raptors    gm3           w     
#>  4 Toronto Raptors    gm4           w     
#>  5 Toronto Raptors    gm5           w     
#>  6 Los Angeles Lakers gm1           l     
#>  7 Los Angeles Lakers gm2           w     
#>  8 Los Angeles Lakers gm3           w     
#>  9 Los Angeles Lakers gm4           l     
#> 10 Los Angeles Lakers gm5           w     
#> # … with 15 more rows
```

Observe the effect the following code has on the data set. Take note of the difference in the number of rows and columns between the two tables.


```r
pivot_wider(data = games_long, names_from = "game number", values_from = status)
#> # A tibble: 5 × 6
#>   teams                 gm1   gm2   gm3   gm4   gm5  
#>   <chr>                 <chr> <chr> <chr> <chr> <chr>
#> 1 Toronto Raptors       l     l     w     w     w    
#> 2 Los Angeles Lakers    l     w     w     l     w    
#> 3 Boston Celtics        w     l     l     l     w    
#> 4 Golden State Warriors l     w     l     l     w    
#> 5 Miami Heat            l     l     w     w     l
```

## Visualizing pivot_wider()

This video will guide you through the changes that occur when applying `pivot_wider()` to our data frame.

<iframe width="560" height="315" src="https://www.youtube.com/embed/PycHf7Og-sY" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## pivot_wider() Arguments

You just executed the command `pivot_wider(data = games, names_from = "game number", values_from = status)`. What do each of the arguments within the brackets mean?

- **data**: the name of our dataframe, in this case `games`.

- **names_from**: the column containing the names which will be given to the new columns once the data frame is pivoted. *In our example, we use "game number" since we want each column to contain information for a specific game*.

- **values_from**: the name (or names, in a vector) of the column containing values that will be stored at the cell level within each new column once the data frame is pivoted. *In our example, we use "status" since we want each team's win or loss results recorded in the appropriate game's column and the appropriate team's row*.

## Other Optional Arguments

### pivot_longer()
- **names_prefix = "..."**: Removes a the stated common prefix from the beginning of each pivoted column name.
- **values_drop_na = TRUE**: If TRUE, this will remove rows containing only missing (NA) values in the **values_to** column.

### pivot_wider()
- **names_prefix = "..."**: Adds the stated string to the beginning of each new column name from `names from` argument. This may be useful if the data contained in `names_from` is numeric and you wish to add a descriptive prefix.

- **values_fill = "..."**: replaces any missing or NA values in `values_from` with the inputted string or value.

- **names_sort = TRUE**: sorts the columns by name instead of in order of appearance.

- **names_sep = "..."**: if `names_from` or `values_from` contains multiple variables (in the form of a vector), `names_sep` allows you to state a specific string that will be used to join their names together into a single string as a column name (for example, "." or "_").


<!-- ## Exercises -->

<!-- ### pivot_longer() -->

<!-- Original `games` data, for reference. -->

<!-- ```{r gamesref, echo=FALSE} -->
<!-- games -->
<!-- ``` -->

<!-- **Hint**: Unless specified, there are multiple ways to select the columns you wish to pivot. -->

<!-- 1. Pivot the data stored in all columns except "teams". Map column names to a new column called "top five" and data from pivoted columns to a new column called "outcome". -->

<!-- <!-- ```{r longerexample1, exercise=TRUE} -->

<!-- <!-- ``` -->
<!-- <!-- ```{r longerexample1-solution} -->
<!-- <!-- pivot_longer(games, cols = !teams, names_to = "top five", values_to = "outcome") -->
<!-- <!-- ``` -->


<!-- 2. The code in the window below replaces all "l" values in "games" with NA. Run this code, then pivot this table to make it longer while removing all rows with NA values. Assign columns their default names. -->

<!-- <!-- ```{r longerexample2, exercise=TRUE} -->
<!-- <!-- games[games=="l"] <- NA -->
<!-- <!-- games -->
<!-- <!-- ``` -->
<!-- <!-- ```{r longerexample2-solution} -->
<!-- <!-- pivot_longer(data = games, cols = c(gm1, gm2, gm3, gm4, gm5), values_drop_na = TRUE) -->
<!-- <!-- ``` -->


<!-- ### pivot_wider() -->

<!-- Original `games_long` data, for reference. -->

<!-- ```{r games_longref, echo=FALSE} -->
<!-- games_long -->
<!-- ``` -->

<!-- 1. Manipulate `games_long` to look like the original `games` data frame at the top of this page. -->

<!-- ```{r widerexample1, exercise=TRUE} -->

<!-- ``` -->
<!-- ```{r widerexample1-solution} -->
<!-- pivot_wider(data = games_long, names_from = "game number", values_from = "status") -->
<!-- ``` -->

## Common Mistakes & Errors

- If you want to keep your dataframe in its longer or wider version, make sure to assign or reassign it to a variable when you execute `pivot_longer()`. For example, if you wish "games" to now represent the longer version of games instead of the original, you must write `games <- pivot_longer(data=games, ...)`


*Error in UseMethod("pivot_longer") : 
  no applicable method for 'pivot_longer' applied to an object of class "c('matrix', 'array', 'character')"*

- pivot_longer() only works on **dataframes** (not lists, character vectors, etc.). If you are working with something that isn't a dataframe, you can use the function `as.data.frame()` to turn your data from its original format into a dataframe.

## Next Steps

- Try more complicated pivots, like pivoting into multiple new columns at once or combining boolean statements.
- Switch your dataframe between formats using `pivot_longer()` and `pivot_wider()` as inverse functions.


## Exercises

### Question 1

Which of the following is generally a desired effect of executing `pivot_longer()` on a data frame?

  a. Increase number of columns
  b.  Increase number of rows
  c. Decrease number of values
  d. None of the above

### Question 2

Which of the following is generally a desired effect of executing `pivot_wider()` on a data frame?

  a.  Increase number of columns
  b. Increase number of rows
  c. Decrease number of values
  d. None of the above

### Question 3

Please reference this table representing different pizza topping combinations for Questions 3 through 5:

```
#>       type      top1      top2
#> 1  classic    cheese pepperoni
#> 2 hawaiian       ham pineapple
#> 3   veggie mushrooms   peppers
```

If `pivot_longer()` was applied to this dataframe on columns 'top1' and 'top2', how many rows would the output have (not including the header)?

  a. 2
  b. 3
  c.  6
  d. 9

### Question 4
If `pivot_longer()` was applied to this dataframe on columns 'top1' and 'top2', how many times would the word 'pineapple' appear in the outputted dataframe?

  a.  1
  b. 2
  c. 3
  d. 0

### Question 5
If `pivot_longer()` was applied to this dataframe on columns 'top1' and 'top2', what would the fourth row (not including header) of the outputted dataframe contain?

  a. veggie, top1, mushrooms
  b. veggie, top2, peppers
  c. hawaiian, top1, ham
  d.  hawaiian, top2, pineapple  


### Question 6

Please reference the following table representing different pizza topping combinations for Question 6 through 8:

```
#> # A tibble: 6 × 3
#>   type     number topping  
#>   <chr>    <chr>  <chr>    
#> 1 classic  top1   cheese   
#> 2 classic  top2   pepperoni
#> 3 hawaiian top1   ham      
#> 4 hawaiian top2   pineapple
#> 5 veggie   top1   mushrooms
#> 6 veggie   top2   peppers
```

If `pivot_wider()` was applied to this dataframe with names from "number" and values from "topping", how many columns would the output have?

  a. 2
  b.  3
  c. 6
  d. 9


### Question 7
If `pivot_wider()` was applied to this dataframe with names from "number" and values from "topping", how many times would the type "classic" appear in the output?

  a.  1
  b. 2
  c. 3
  d. 0

### Question 8
If `pivot_wider()` was applied to this dataframe with names from "number" and values from "topping", what would the column names be?

  a.  type, top1, top2
  b. classic, hawaiian, veggie
  c. type, number, topping
  d. classic, cheese, pepperoni

### Question 9

Please refer to the following data sets, `games1` and `games2`, for Questions 9 and 10.

```
#>                   teams  gm1  gm2  gm3  gm4  gm5
#> 1       Toronto Raptors <NA> <NA>    w    w    w
#> 2    Los Angeles Lakers <NA>    w    w <NA>    w
#> 3        Boston Celtics    w <NA> <NA> <NA>    w
#> 4 Golden State Warriors <NA>    w <NA> <NA>    w
#> 5            Miami Heat <NA> <NA>    w    w <NA>
```

```
#> # A tibble: 12 × 3
#>    teams                 name  value
#>    <chr>                 <chr> <chr>
#>  1 Toronto Raptors       gm3   w    
#>  2 Toronto Raptors       gm4   w    
#>  3 Toronto Raptors       gm5   w    
#>  4 Los Angeles Lakers    gm2   w    
#>  5 Los Angeles Lakers    gm3   w    
#>  6 Los Angeles Lakers    gm5   w    
#>  7 Boston Celtics        gm1   w    
#>  8 Boston Celtics        gm5   w    
#>  9 Golden State Warriors gm2   w    
#> 10 Golden State Warriors gm5   w    
#> 11 Miami Heat            gm3   w    
#> 12 Miami Heat            gm4   w
```

Which of the following lines of code will convert `games1` to `games2`?

  a. `pivot_wider(games1, cols = teams, values_drop_na = TRUE)`
  b. `pivot_longer(games1, cols = teams, na.rm = TRUE)`
  c. `pivot_longer(games1, cols = c(gm1, gm2, gm3, gm4, gm5), na.rm = TRUE)`
  d.  `pivot_longer(games1, cols = c(gm1, gm2, gm3, gm4, gm5), values_drop_na = TRUE)`

### Question 10

Which of the following lines of code will convert `games2` to the original `games` data set?

  a. `pivot_wider(games2, names_from = name, values_from = value, values_fill = "l", values_sort = TRUE)`
  b. `pivot_wider(games2, names_from = name, values_from = value, values_fill = NA)`
  c. `pivot_longer(games2, names_from = name, values_from = value, values_fill = NA)`
  d.  `pivot_wider(games2, names_from = name, values_from = value, values_fill = "l", names_sort = TRUE)`
