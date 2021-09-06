



# pivoting

Written by Annie Collins.


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

Run the code below and observe the effect it has on the dataset. Take note of the difference in the number of rows and columns between the two tables. This will be visualized and explained in greater detail in the following step.



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

Run the code below and observe the effect it has on the dataset. Take note of the difference in the number of rows and columns between the two tables.


```
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


## Questions

Please reference this dataframe representing different pizza topping combinations for the following three questions:

```
#>       type      top1      top2
#> 1  classic    cheese pepperoni
#> 2 hawaiian       ham pineapple
#> 3   veggie mushrooms   peppers
```

<!-- ```{r longerq1, echo=FALSE} -->
<!-- question("If `pivot_longer()` was applied to this dataframe on columns 'top1' and 'top2', how many rows would the output have (not including the header)?", -->
<!-- answer("2"), -->
<!-- answer("3"), -->
<!-- answer("6", correct=TRUE), -->
<!-- answer("9") -->
<!-- ) -->
<!-- ``` -->

<!-- ```{r longerq2, echo=FALSE} -->
<!-- question("If `pivot_longer()` was applied to this dataframe on columns 'top1' and 'top2', how many times would the word 'pineapple' appear in the outputted dataframe?", -->
<!-- answer("1", correct=TRUE), -->
<!-- answer("2"), -->
<!-- answer("3"), -->
<!-- answer("0") -->
<!-- ) -->
<!-- ``` -->

<!-- ```{r longerq3, echo=FALSE} -->
<!-- question("If `pivot_longer()` was applied to this dataframe on columns 'top1' and 'top2', what would the fourth row (not including header) of the outputted dataframe contain?", -->
<!-- answer("veggie, top1, mushrooms"), -->
<!-- answer("veggie, top2, peppers"), -->
<!-- answer("hawaiian, top1, ham"), -->
<!-- answer("hawaiian, top2, pineapple", correct = TRUE) -->
<!-- ) -->
<!-- ``` -->


<!-- Please reference this dataframe representing different pizza topping combinations for the following three questions: -->
<!-- ```{r questionframe2, echo=FALSE} -->
<!-- pivot_longer(pizza, cols=starts_with("top"), names_to = "number", values_to = "topping") -->
<!-- ``` -->
<!-- ```{r widerq1, echo=FALSE} -->
<!-- question("If `pivot_wider()` was applied to this dataframe with names from \"number\" and values from \"topping\", how many columns would the output have?", -->
<!-- answer("2"), -->
<!-- answer("3", correct=TRUE), -->
<!-- answer("6"), -->
<!-- answer("9") -->
<!-- ) -->
<!-- ``` -->

<!-- ```{r widerq2, echo=FALSE} -->
<!-- question("If `pivot_wider()` was applied to this dataframe with names from \"number\" and values from \"topping\", how many times would the type \"classic\" appear in the output?", -->
<!-- answer("1", correct = TRUE), -->
<!-- answer("2"), -->
<!-- answer("3"), -->
<!-- answer("0") -->
<!-- ) -->
<!-- ``` -->

<!-- ```{r widerq3, echo=FALSE} -->
<!-- question("If `pivot_wider()` was applied to this dataframe with names from \"number\" and values from \"topping\", what would the column names be?", -->
<!-- answer("type, top1, top2", correct = TRUE), -->
<!-- answer("classic, hawaiian, veggie"), -->
<!-- answer("type, number, topping"), -->
<!-- answer("classic, cheese, pepperoni") -->
<!-- ) -->
<!-- ``` -->

## Exercises

### pivot_longer()

Original `games` data, for reference.


```
#>                   teams gm1 gm2 gm3 gm4 gm5
#> 1       Toronto Raptors   l   l   w   w   w
#> 2    Los Angeles Lakers   l   w   w   l   w
#> 3        Boston Celtics   w   l   l   l   w
#> 4 Golden State Warriors   l   w   l   l   w
#> 5            Miami Heat   l   l   w   w   l
```

**Hint**: Unless specified, there are multiple ways to select the columns you wish to pivot.

1. Pivot the data stored in all columns except "teams". Map column names to a new column called "top five" and data from pivoted columns to a new column called "outcome".

<!-- ```{r longerexample1, exercise=TRUE} -->

<!-- ``` -->
<!-- ```{r longerexample1-solution} -->
<!-- pivot_longer(games, cols = !teams, names_to = "top five", values_to = "outcome") -->
<!-- ``` -->


2. The code in the window below replaces all "l" values in "games" with NA. Run this code, then pivot this table to make it longer while removing all rows with NA values. Assign columns their default names.

<!-- ```{r longerexample2, exercise=TRUE} -->
<!-- games[games=="l"] <- NA -->
<!-- games -->
<!-- ``` -->
<!-- ```{r longerexample2-solution} -->
<!-- pivot_longer(data = games, cols = c(gm1, gm2, gm3, gm4, gm5), values_drop_na = TRUE) -->
<!-- ``` -->


### pivot_wider()

Original `games_long` data, for reference.


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

1. Manipulate `games_long` to look like the original `games` data frame at the top of this page.

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














