


# Conditional mutating and summarising

*Written by Mariam Walaa and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- Use `across()` with `summarise()` 
- Use `mutate_if()` 
- Use `if_else()` and `na_if()` 

Prerequisite skills include:

- Familiarity with `summarize()` and `mutate()`
- Familiarity with conditional statements `if_else()`

Highlights:

- Use `across()` to summarize across a defined selection of columns
- Mutate column types based on conditions using `mutate_if()`
- Mutate columns based on conditions using `if_else()` and `na_if()` within `mutate()`

## Overview

This section will demonstrate how to use the `summarise()` function with `across()` to 
summarize variables and groups within a variable in a data set. We will be looking at a
data set of Broadway shows with variables about the performances, attendance, and revenue
for theaters that are part of The Broadway League. You can learn more about the data set
provided by Alex Cookson in [the dataset repository](https://github.com/tacookson/data) as
well as this corresponding [blog
post](https://www.alexcookson.com/post/most-successful-broadway-show-of-all-time/).

### Video

![](https://youtu.be/3mmbPjgzzeY)

## Questions

Lets start with loading the tidyverse and looking at the data.


```r
library(tidyverse)
```


```r
broadway
#> # A tibble: 47,524 × 8
#>    week_ending show   theatre  weekly_gross avg_ticket_price
#>    <date>      <chr>  <chr>           <dbl>            <dbl>
#>  1 1985-06-09  42nd … St. Jam…       282368             30.4
#>  2 1985-06-09  A Cho… Sam S. …       222584             27.2
#>  3 1985-06-09  Aren'… Brooks …       249272             33.8
#>  4 1985-06-09  Arms … Circle …        95688             20.9
#>  5 1985-06-09  As Is  Lyceum …        61059             20.8
#>  6 1985-06-09  Big R… Eugene …       255386             32.0
#>  7 1985-06-09  Bilox… Neil Si…       306839             28.3
#>  8 1985-06-09  Brigh… 46th St…       107392             18.9
#>  9 1985-06-09  Cats   Winter …       461880             38.4
#> 10 1985-06-09  Doubl… Ritz Th…        47452             17.5
#> # … with 47,514 more rows, and 3 more variables:
#> #   top_ticket_price <dbl>, performances <dbl>,
#> #   previews <dbl>
```

### Question 1

What is the minimum and maximum number of performances _and_ previews per week? We can use
`across()` to select specific columns to summarize them with multiple summary functions.



<pre><code class='language-r'><code>broadway %>%<br>&nbsp;&nbsp;group_by(week_ending) %>%<br>&nbsp;&nbsp;summarise(<span style='color:blue'>across</span>(<span style='color:deeppink'>.cols</span> = c("performances", "previews"),<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style='color:orange'>.fns</span> = list(min = min, max = max)),<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.groups = 'drop')<br>#> # A tibble: 1,812 × 5<br>#> &nbsp;&nbsp;&nbsp;week_ending performances_min performances_max<br>#> &nbsp;&nbsp;&nbsp;<date> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<dbl> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<dbl><br>#> &nbsp;1 1985-06-09 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> &nbsp;2 1985-06-16 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8<br>#> &nbsp;3 1985-06-23 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> &nbsp;4 1985-06-30 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> &nbsp;5 1985-07-07 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;7 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> &nbsp;6 1985-07-14 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> &nbsp;7 1985-07-21 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> &nbsp;8 1985-07-28 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> &nbsp;9 1985-08-04 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> 10 1985-08-11 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> # … with 1,802 more rows, and 2 more variables:<br>#> # &nbsp;&nbsp;previews_min <dbl>, previews_max <dbl></code></code></pre>

Here is what the above chunk of code does:

* Groups the data by week using `group_by()` 
* Selects columns to summarize by passing a vector to `.cols` in `across()` (Highlighted in pink) 
* Defines summary functions by passing a list to `.fns` in `across()` (Highlighted in orange)

You can also learn more about `across()` by running `?across` in your console.

### Question 2

How do we provide a numeric summary for every show happening in a particular week?


```r
broadway %>%
  group_by(week_ending, show) %>%
  summarise(across(where(is.numeric), mean, na.rm = TRUE),
            .groups = 'drop')
#> # A tibble: 47,524 × 7
#>    week_ending show                   weekly_gross avg_ticket_price
#>    <date>      <chr>                         <dbl>            <dbl>
#>  1 1985-06-09  42nd Street                  282368             30.4
#>  2 1985-06-09  A Chorus Line                222584             27.2
#>  3 1985-06-09  Aren't We All?               249272             33.8
#>  4 1985-06-09  Arms and the Man              95688             20.9
#>  5 1985-06-09  As Is                         61059             20.8
#>  6 1985-06-09  Big River                    255386             32.0
#>  7 1985-06-09  Biloxi Blues                 306839             28.3
#>  8 1985-06-09  Brighton Beach Memoirs       107392             18.9
#>  9 1985-06-09  Cats                         461880             38.4
#> 10 1985-06-09  Doubles                       47452             17.5
#> # … with 47,514 more rows, and 3 more variables:
#> #   top_ticket_price <dbl>, performances <dbl>,
#> #   previews <dbl>
```

This chunk of code summarizes every show happening in some particular week by every
numeric variable that is available in the data set. This helps us compute things like
the average ticket price and the number of performances each show had in a particular
week.

### Question 3

We can use mutate() and if_else() to change values within a column. For example, here
is what we would write if we wanted to change all rows with theatre Studio 54 to be 
called Studio 54 Theatre.


```r
broadway %>% 
    mutate(theatre = if_else(theatre == "Studio 54", "Studio 54 Theatre", theatre))
#> # A tibble: 47,524 × 8
#>    week_ending show   theatre  weekly_gross avg_ticket_price
#>    <date>      <chr>  <chr>           <dbl>            <dbl>
#>  1 1985-06-09  42nd … St. Jam…       282368             30.4
#>  2 1985-06-09  A Cho… Sam S. …       222584             27.2
#>  3 1985-06-09  Aren'… Brooks …       249272             33.8
#>  4 1985-06-09  Arms … Circle …        95688             20.9
#>  5 1985-06-09  As Is  Lyceum …        61059             20.8
#>  6 1985-06-09  Big R… Eugene …       255386             32.0
#>  7 1985-06-09  Bilox… Neil Si…       306839             28.3
#>  8 1985-06-09  Brigh… 46th St…       107392             18.9
#>  9 1985-06-09  Cats   Winter …       461880             38.4
#> 10 1985-06-09  Doubl… Ritz Th…        47452             17.5
#> # … with 47,514 more rows, and 3 more variables:
#> #   top_ticket_price <dbl>, performances <dbl>,
#> #   previews <dbl>
```

We can confirm this by filtering for these theatre names.


```r
broadway %>%
  mutate(theatre = if_else(theatre == "Studio 54", "Studio 54 Theatre", theatre)) %>%
  filter(theatre %in% c("Studio 54", "Studio 54 Theatre"))
#> # A tibble: 787 × 8
#>    week_ending show    theatre weekly_gross avg_ticket_price
#>    <date>      <chr>   <chr>          <dbl>            <dbl>
#>  1 1998-02-15  Cabaret Studio…        48008             58.4
#>  2 1998-02-22  Cabaret Studio…       172373             51.5
#>  3 1998-03-01  Cabaret Studio…       174178             50.8
#>  4 1998-03-08  Cabaret Studio…       177623             49.3
#>  5 1998-03-15  Cabaret Studio…       147752             48.3
#>  6 1998-03-22  Cabaret Studio…       151753             49.1
#>  7 1998-03-29  Cabaret Studio…       183802             48.7
#>  8 1998-04-05  Cabaret Studio…       194515             50.8
#>  9 1998-04-12  Cabaret Studio…       219786             54.2
#> 10 1998-04-19  Cabaret Studio…       196320             48.1
#> # … with 777 more rows, and 3 more variables:
#> #   top_ticket_price <dbl>, performances <dbl>,
#> #   previews <dbl>
```

Notice that we did not save the initial modified data frame. We are also using a new
operator %in% which checks for the value Studio 54 in a vector of values including
Studio 54 and Studio 54 Theatre.

## Arguments

### `across()`

The `across()` function takes the following as arguments:

| Argument | Parameter | Details                                           |
| -------- | --------- | ------------------------------------------------- |
| .fns     |           | can pass a list of functions or a single function |
| .cols    | vector    | vector with column names to apply functions to    |

You can read more about the arguments in the `across()` function documentation
[here](https://dplyr.tidyverse.org/reference/across.html). Please note that the arguments 
for across() will also depend on your use case.

### `mutate_if()`

The `mutate_if()` function takes the following as arguments:

| Argument  | Details                                            |
| --------- | -------------------------------------------------- |
| selection | selection of variables by type, i.e., is.character |
| function  |  function to apply to the selection of variables   |

You can read more about the arguments in the `mutate_if()` function documentation
[here](https://dplyr.tidyverse.org/reference/mutate_all.html). 

### `na_if()`

The `na_if()` function takes the following as arguments:

| Argument  | Details                                            |
| --------- | -------------------------------------------------- |
| vector    | vector to look for values we want to change        |
| value     | value in the vector that we want to change to NA   |

You can read more about the arguments in the `na_if()` function documentation
[here](https://dplyr.tidyverse.org/reference/na_if.html).

You can read more about `if_else()` in the corresponding tutorial on conditional
statements.

## Exercises

### Exercise 1

Count the number of distinct shows and distinct theatres using summarise() and across().
As a tip, try to use the data type for shows and theatres columns.





### Exercise 2

Use the mutate_if() function to select all the variables of type double and convert them
to character.





### Exercise 3

There are some shows with a value of [title of show] under the show column. Use the
na_if() conditional statement within mutate() to convert this to NA.






## Next Steps

If you would like to learn more about the functions in this tutorial, you may find the
following resource helpful:

- [dplyr: Apply a function (or functions) across multiple
columns](https://dplyr.tidyverse.org/reference/across.html)
- [Mutate multiple columns](https://dplyr.tidyverse.org/reference/mutate_all.html)
- [Convert values to NA](https://dplyr.tidyverse.org/reference/na_if.html)



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
