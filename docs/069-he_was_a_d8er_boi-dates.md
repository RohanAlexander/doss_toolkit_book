


# Working with dates

*Written by Mariam Walaa and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- Work with dates using the `lubridate` library

Prerequisite skills include:

- Installing and loading packages
- Using `mutate()` and `summarise()`

Highlights:

- Loading the `lubridate` library separately from `tidyverse`
- Using the `today()` and `now()` functions
- Learning how to extract information from a date-time column


## Overview

Let's start by loading the `tidyverse`.


```r
library(tidyverse)
```

Notice that `lubridate` is not listed as one of the libraries loaded into your R session
when you load `tidyverse` (which you can view in your output on your own RStudio), and
this is because it is not part of the core `tidyverse` so it will need to be loaded
separately.


```r
library(lubridate)
#> 
#> Attaching package: 'lubridate'
#> The following objects are masked from 'package:base':
#> 
#>     date, intersect, setdiff, union
```

Two of the functions the `lubridate` library will give us is `today()` and `now()`, which
we can immediately start to use, without data or parameters.


```r
today()
#> [1] "2022-02-08"
```


```r
now()
#> [1] "2022-02-08 12:33:47 EST"
```

You may want to use these functions today() and now() for various reasons, such as 
including the date and time in a file name. You can do that as follows.


```r
paste0(today(), "_datafile.csv")
#> [1] "2022-02-08_datafile.csv"
```

### Example

We will look at Caribou data from Alex Cooksons dataset repository for this tutorial.




```r
glimpse(caribou)
#> Rows: 249,450
#> Columns: 7
#> $ event_id   <dbl> 2259197332, 2259197333, 2259197334, 225…
#> $ animal_id  <chr> "GR_C01", "GR_C01", "GR_C01", "GR_C01",…
#> $ study_site <chr> "Graham", "Graham", "Graham", "Graham",…
#> $ season     <chr> "Winter", "Winter", "Winter", "Winter",…
#> $ timestamp  <dttm> 2001-02-21 05:00:00, 2001-02-21 09:00:…
#> $ longitude  <dbl> -122.5200, -122.5224, -122.5232, -122.5…
#> $ latitude   <dbl> 56.23950, 56.23985, 56.24000, 56.23187,…
```

We can see that the timestamp column has an associated data type 'dttm.' This stands for
datetime. Given that this is already the correct data type, we can extract a lot of
information from it using `lubridate` functions.


```r
# extracting year
caribou %>% mutate(year = year(timestamp))
#> # A tibble: 249,450 × 8
#>     event_id animal_id study_site season timestamp          
#>        <dbl> <chr>     <chr>      <chr>  <dttm>             
#>  1    2.26e9 GR_C01    Graham     Winter 2001-02-21 05:00:00
#>  2    2.26e9 GR_C01    Graham     Winter 2001-02-21 09:00:00
#>  3    2.26e9 GR_C01    Graham     Winter 2001-02-21 13:00:00
#>  4    2.26e9 GR_C01    Graham     Winter 2001-02-21 17:01:00
#>  5    2.26e9 GR_C01    Graham     Winter 2001-02-21 21:00:00
#>  6    2.26e9 GR_C01    Graham     Winter 2001-02-22 01:00:00
#>  7    2.26e9 GR_C01    Graham     Winter 2001-02-22 05:00:00
#>  8    2.26e9 GR_C01    Graham     Winter 2001-02-22 09:00:00
#>  9    2.26e9 GR_C01    Graham     Winter 2001-02-22 13:00:00
#> 10    2.26e9 GR_C01    Graham     Winter 2001-02-22 17:00:00
#> # … with 249,440 more rows, and 3 more variables:
#> #   longitude <dbl>, latitude <dbl>, year <dbl>

# extracting week day
caribou %>% mutate(week_day = wday(timestamp))
#> # A tibble: 249,450 × 8
#>     event_id animal_id study_site season timestamp          
#>        <dbl> <chr>     <chr>      <chr>  <dttm>             
#>  1    2.26e9 GR_C01    Graham     Winter 2001-02-21 05:00:00
#>  2    2.26e9 GR_C01    Graham     Winter 2001-02-21 09:00:00
#>  3    2.26e9 GR_C01    Graham     Winter 2001-02-21 13:00:00
#>  4    2.26e9 GR_C01    Graham     Winter 2001-02-21 17:01:00
#>  5    2.26e9 GR_C01    Graham     Winter 2001-02-21 21:00:00
#>  6    2.26e9 GR_C01    Graham     Winter 2001-02-22 01:00:00
#>  7    2.26e9 GR_C01    Graham     Winter 2001-02-22 05:00:00
#>  8    2.26e9 GR_C01    Graham     Winter 2001-02-22 09:00:00
#>  9    2.26e9 GR_C01    Graham     Winter 2001-02-22 13:00:00
#> 10    2.26e9 GR_C01    Graham     Winter 2001-02-22 17:00:00
#> # … with 249,440 more rows, and 3 more variables:
#> #   longitude <dbl>, latitude <dbl>, week_day <dbl>

# extracting whether it's a leap year!
caribou %>% mutate(leap_year = leap_year(timestamp))
#> # A tibble: 249,450 × 8
#>     event_id animal_id study_site season timestamp          
#>        <dbl> <chr>     <chr>      <chr>  <dttm>             
#>  1    2.26e9 GR_C01    Graham     Winter 2001-02-21 05:00:00
#>  2    2.26e9 GR_C01    Graham     Winter 2001-02-21 09:00:00
#>  3    2.26e9 GR_C01    Graham     Winter 2001-02-21 13:00:00
#>  4    2.26e9 GR_C01    Graham     Winter 2001-02-21 17:01:00
#>  5    2.26e9 GR_C01    Graham     Winter 2001-02-21 21:00:00
#>  6    2.26e9 GR_C01    Graham     Winter 2001-02-22 01:00:00
#>  7    2.26e9 GR_C01    Graham     Winter 2001-02-22 05:00:00
#>  8    2.26e9 GR_C01    Graham     Winter 2001-02-22 09:00:00
#>  9    2.26e9 GR_C01    Graham     Winter 2001-02-22 13:00:00
#> 10    2.26e9 GR_C01    Graham     Winter 2001-02-22 17:00:00
#> # … with 249,440 more rows, and 3 more variables:
#> #   longitude <dbl>, latitude <dbl>, leap_year <lgl>
```

You can see there are many additional variables we can extract with the `lubridate` 
package. You can check out the [lubridate
cheatsheet](https://raw.githubusercontent.com/rstudio/cheatsheets/master/lubridate.pdf) to
learn more.

## Exercises

### Exercise 1

Extract month, day, and year into separate columns at the same time using mutate.






### Exercise 2

Find the earliest and latest dates in the timestamp column.






**Hint**: Remember the summary functions you learned in `summarize()` tutorial!

## Common Mistakes & Errors

- You might try to apply `lubridate` functions on to a column that looks like a timestamp
column, but it may still not be of the appropriate data type, which is either 'dt', 'tm',
or 'dttm'. Be sure to convert to the proper data type first!

## Next Steps

If you would like to learn more about handling dates and times in R, as well as the
`lubridate` package, please read the following:

- [R For Data Science:  16 Dates and times](https://r4ds.had.co.nz/dates-and-times.html)
- [Lubridate Package Documentation](https://lubridate.tidyverse.org/)




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
