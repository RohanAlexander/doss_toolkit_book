


# Counting

*Written by Annie Collins and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- Use `count()` to summarize a data set.
- Use `uncount()` to produce a full data set from a table containing values and counts.

This lesson is a yellow level skill and is part of "Tidyverse Essentials". Prerequisite skills include:

- Installing packages
- Calling libraries
- Importing data

## Video Tutorial

<iframe width="560" height="315" src="https://www.youtube.com/embed/zPqeJPjYc48" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## count()

`count()` is a function that can be used to summarize a data set in terms of the number of unique values of a certain variable or combination of variables.

Using `count()` on a data set produces a new table including each unique value or combination of values along with an integer value representing the number of times it appears in the data.

## Using count()

The data set below (`starwars`) contains information on characters in the the *Star Wars* film franchise. There are 30 unique characters in the data with five characteristics/measurements recorded for each.


```
#> # A tibble: 30 × 6
#>    name    hair_color skin_color eye_color homeworld species
#>    <chr>   <chr>      <chr>      <chr>     <chr>     <chr>  
#>  1 Luke S… blond      fair       blue      Tatooine  Human  
#>  2 C-3PO   <NA>       gold       yellow    Tatooine  Droid  
#>  3 R2-D2   <NA>       white, bl… red       Naboo     Droid  
#>  4 Darth … none       white      yellow    Tatooine  Human  
#>  5 Leia O… brown      light      brown     Alderaan  Human  
#>  6 Owen L… brown, gr… light      blue      Tatooine  Human  
#>  7 Beru W… brown      light      blue      Tatooine  Human  
#>  8 R5-D4   <NA>       white, red red       Tatooine  Droid  
#>  9 Biggs … black      light      brown     Tatooine  Human  
#> 10 Anakin… blond      fair       blue      Tatooine  Human  
#> # … with 20 more rows
```

Although each character is unique and only appears once in the data, there are several variables where multiple characters have the same characteristic, and we may want to know how many characters share each characteristic.

For example, we may want to examine how many characters came from each home world.


```r
count(starwars, homeworld)
#> # A tibble: 5 × 2
#>   homeworld     n
#>   <chr>     <int>
#> 1 Alderaan      3
#> 2 Coruscant     3
#> 3 Kamino        3
#> 4 Naboo        11
#> 5 Tatooine     10
```

We can also sort this table to see which home worlds appear in the data most frequently.


```r
count(starwars, homeworld, sort=TRUE)
#> # A tibble: 5 × 2
#>   homeworld     n
#>   <chr>     <int>
#> 1 Naboo        11
#> 2 Tatooine     10
#> 3 Alderaan      3
#> 4 Coruscant     3
#> 5 Kamino        3
```
Here, we see that Naboo is the most common home world, with 11 characters in the data set from this world.

If we wish to get even more specific, we could look at unique species-homeworld combinations amongst characters in the data.


```r
count(starwars, species, homeworld, sort=TRUE)
#> # A tibble: 11 × 3
#>    species    homeworld     n
#>    <chr>      <chr>     <int>
#>  1 Human      Tatooine      8
#>  2 Human      Naboo         5
#>  3 Gungan     Naboo         3
#>  4 Human      Alderaan      3
#>  5 Droid      Tatooine      2
#>  6 Human      Coruscant     2
#>  7 Kaminoan   Kamino        2
#>  8 <NA>       Naboo         2
#>  9 Droid      Naboo         1
#> 10 Human      Kamino        1
#> 11 Tholothian Coruscant     1
```
The outputted table shows that there are eight characters in the `starwars` data set that are humans from Tatooine, five that are humans from Naboo, and so on.

## count() Arguments

`count(data, variables, sort = FALSE, name = NULL)`

- **data**: the data frame you are counting from.
- **variables**: the variables in **data** you are counting, inputted by individual column name. This could be one or multiple variables to be counted in combination. If none are entered, `count()` will return a count of the total number of rows in **data**.
- **sort = ...**: FALSE by default (if omitted). If sort = TRUE, `count()` will sort the outputted table in descending order of the count column, otherwise it will be sorted in alphabetical order by the first column (with NA values last).
- **name = "..."**: NULL (empty) by default. This argument indicates the name you wish to give the column containing the count values, inputted in the form of a string. If omitted, the count column will be titled **n**.

## uncount()

`uncount()` is a function that can be used to produce a full length table from a table containing variables and counts (for example, one that was produced using the `count()` function). The function duplicates each unique variable according to the value in the count column indicated. You may think of it as the inverse of `count()`.

### Arguments

`uncount()` takes two required arguments and two optional arguments:

`uncount(data, weights, .remove = TRUE, .id = NULL)`

- **data**: the data frame containing variables and counts.
- **weights**: the name of the column in **data** containing the counts for each variable(s). You can also use a constant or expression if you wish all variables to be duplicated the same number of times, or if an appropriate column does not exist in **data**.

**Optional**:

- **.remove = ...**: TRUE by default. If **weights** is a column in **data**, this argument indicates whether or not you want the **weights** values to remain in the outputted table. If .remove = TRUE (default), the outputted table will only contain the duplicated variables. If .return = FALSE, the outputted table will contain the duplicated variables along with their total count present in an additional column. If **weights** is a value or expression, then **.remove** does not apply and the column containing counts (if it exists) will be included in the outputted table.
- **.id = "..."**: NULL (empty) by default. This argument allows you to input a string as the title for a new column that will automatically generate a unique ID for each duplicated variable. This may be useful if you still want to distinguish between variables once they have been repeated.

## Using uncount()

To help visualize the use of `uncount()`, we will use this small data set called `colours`.


```
#>   colour n
#> 1    red 1
#> 2 yellow 2
#> 3   blue 3
```
 `colours` indicates that red occurs once, yellow occurs twice, and blue occurs three times in some data, for a total of six observations.

If we want to observe all the data in its uncounted form, we can use `uncount()`.


```r
uncount(colours, n)
#>   colour
#> 1    red
#> 2 yellow
#> 3 yellow
#> 4   blue
#> 5   blue
#> 6   blue
```
Our output includes only one column (no count values) with each colour repeated the number of times indicated in the **n** column in `colours`. `uncount()` also automatically generates a new version of the row number according to the number of times each row was duplicated.

If we wish to duplicate each colour (regardless of the value in column **n**), we can substitute **2** in place of **n** in the function. Note that in the outputted table, the values from **n** are still present since we did not input a column for the **weights** argument.


```r
uncount(colours, 2)
#>   colour n
#> 1    red 1
#> 2    red 1
#> 3 yellow 2
#> 4 yellow 2
#> 5   blue 3
#> 6   blue 3
```
Using the optional arguments **.remove** and **.id**, we can uncount `colours` according to column **n** while still keeping the values from **n** in the output *and* assign a unique ID number to each repeated colour.


```r
uncount(colours, n, .remove = FALSE, .id = "id")
#>   colour n id
#> 1    red 1  1
#> 2 yellow 2  1
#> 3 yellow 2  2
#> 4   blue 3  1
#> 5   blue 3  2
#> 6   blue 3  3
```
Now we can distinguish between different yellow and blue rows in the column (for instance, yellow 1 and yellow 2 according to the **id** column).

Note that this does not change if there are multiple combinations of variables in `colours` we wish to uncount.

Updated `colours`:

```
#>   colour temp n
#> 1    red warm 1
#> 2 yellow warm 2
#> 3   blue cool 3
```

```r
uncount(colours, n, .remove = FALSE, .id = "id")
#>   colour temp n id
#> 1    red warm 1  1
#> 2 yellow warm 2  1
#> 3 yellow warm 2  2
#> 4   blue cool 3  1
#> 5   blue cool 3  2
#> 6   blue cool 3  3
```


## Exercises

Below is the first five rows of output from **Exercise 1**, assigned the name `features`. Please use this data set as reference for the following questions.


```
#> # A tibble: 5 × 3
#>   skin_color eye_color     n
#>   <chr>      <chr>     <int>
#> 1 fair       blue          6
#> 2 light      brown         6
#> 3 dark       brown         2
#> 4 fair       brown         2
#> 5 grey       black         2
```

### Question 1

In the output of `uncount(features, n)`, how many times will the word "brown" appear?

  a. 2
  b. 3
  c. 7
  d.  12

### Question 2

How many rows does the output of `uncount(features, 2)` have (not including the header)?

  a. 5
  b.  10
  c. 21
  d. 42

### Question 3

How many columns does the output of `uncount(features, 2)` have?

  a. 1
  b. 2
  c.  3
  d. 4

For the Question 4 and 5, identify the code used to manipulate the `starwars` data set to match the output displayed. The original is included below for reference.

```
#> # A tibble: 30 × 6
#>    name    hair_color skin_color eye_color homeworld species
#>    <chr>   <chr>      <chr>      <chr>     <chr>     <chr>  
#>  1 Luke S… blond      fair       blue      Tatooine  Human  
#>  2 C-3PO   <NA>       gold       yellow    Tatooine  Droid  
#>  3 R2-D2   <NA>       white, bl… red       Naboo     Droid  
#>  4 Darth … none       white      yellow    Tatooine  Human  
#>  5 Leia O… brown      light      brown     Alderaan  Human  
#>  6 Owen L… brown, gr… light      blue      Tatooine  Human  
#>  7 Beru W… brown      light      blue      Tatooine  Human  
#>  8 R5-D4   <NA>       white, red red       Tatooine  Droid  
#>  9 Biggs … black      light      brown     Tatooine  Human  
#> 10 Anakin… blond      fair       blue      Tatooine  Human  
#> # … with 20 more rows
```

### Question 4

```
#> # A tibble: 16 × 3
#>    skin_color  eye_color     n
#>    <chr>       <chr>     <int>
#>  1 fair        blue          6
#>  2 light       brown         6
#>  3 dark        brown         2
#>  4 fair        brown         2
#>  5 grey        black         2
#>  6 light       blue          2
#>  7 dark        blue          1
#>  8 gold        yellow        1
#>  9 green       orange        1
#> 10 grey        orange        1
#> 11 orange      orange        1
#> 12 pale        yellow        1
#> 13 tan         brown         1
#> 14 white       yellow        1
#> 15 white, blue red           1
#> 16 white, red  red           1
```

  a.  `count(starwars, skin_color, eye_color, sort=TRUE)`
  b. `count(starwars, skin_color, eye_color, sort=FALSE)`
  c. `count(starwars, c(skin_color, eye_color), sort=TRUE)`
  d. `count(starwars, c(skin_color, eye_color), sort=FALSE)`
  
### Question 5

```
#> # A tibble: 30 × 2
#>    name                unique
#>    <chr>                <int>
#>  1 Adi Gallia               1
#>  2 Anakin Skywalker         1
#>  3 Bail Prestor Organa      1
#>  4 Beru Whitesun lars       1
#>  5 Biggs Darklighter        1
#>  6 Boba Fett                1
#>  7 C-3PO                    1
#>  8 Cliegg Lars              1
#>  9 Cordé                    1
#> 10 Darth Vader              1
#> # … with 20 more rows
```

  a. `count(starwars)`
  b. `count(starwars, name, species, .remove = TRUE)`
  c. `count(starwars, name, name="name")`
  d.  `count(starwars, name, name="unique")`
  
### Question 6

What will be the output of the following code: `count(starwars, skin_color) %>% uncount(weights = n)`?

  a. The original `starwars` data frame
  b. A tibble with two columns: one called "skin_color" with each unique skin colour from `starwars` included once, and one called "n" with a count of the number of times that skin colour appears in the data set
  c. A tibble with two columns: one called "skin_color" with each skin colour from `starwars` included the same number of times it appears in the data set, and one called "n" with a count of the number of times that skin colour appears in the data set (repeated for each repeated entry in column "skin_color")
  d.  A tibble with one column called "skin_color" with each skin colour from `starwars` included the same number of times it appears in the data set.

### Question 7

Use the following tibble for Questions 7 through 9:

```
#> # A tibble: 5 × 3
#>   skin_color species       id
#>   <chr>      <chr>      <int>
#> 1 dark       Human          1
#> 2 dark       Tholothian     1
#> 3 dark       <NA>           1
#> 4 fair       Human          1
#> 5 fair       Human          2
```
The tibble above represents the product of manipulating the `starwars` data set using one or more functions. Which of the options below best describes the last function applied in order to produce the given output?

  a. `count()`
  b. `uncount()`
  c. `summarise()`
  d.  Something else

### Question 8
  
True or false: In the first row of the above tibble, the value 1 in the "id" column indicates that there is only one instance of a human with dark skin in the `starwars` data frame.

  a. True
  b.  False

