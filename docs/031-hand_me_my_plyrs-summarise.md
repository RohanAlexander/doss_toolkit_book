


# summarise

*Written by Mariam Walaa and last updated on 7 October 2021.*


## Introduction

In this lesson, you will learn how to:

- Summarize a variable using `summarise()`
- Summarize groups of observations within a variable using `group_by()`

Prerequisite skills include:

- Using `group_by()`
- Using summary functions like `sum()`, `min()`, `max()`

Highlights:

- `summarise()` is often used with `group_by()`
- There are many summary functions you can use within `summarise()`
- You can also define your own functions to use within `summarise()`

![Source: https://github.com/allisonhorst/stats-illustrations Credits: Allison
Horst](https://github.com/allisonhorst/stats-illustrations/blob/master/other-stats-artwork/summary_statistics.png?raw=true){#id
.class width=750 height=500px}

## Arguments

The `summarise()` function takes the following as arguments:

| Argument         | Parameter        | Details                                                    |
|------------------|------------------|------------------------------------------------------------|
| .data            | data frame       | a data frame containing variables we want to summarize     |
| name-value pairs | name-value pairs | this takes the name of the column and the summary function |

You can read more about the arguments in the `summarise()` function documentation
[here](https://www.rdocumentation.org/packages/dplyr/versions/0.7.8/topics/summarise).

## Overview

This section will demonstrate how to use the `summarise()` function to summarize variables
and groups within a variable in a data set. We will be looking at a data set of Broadway
shows with variables about the performances, attendance, and revenue for theaters that are
part of The Broadway League. You can learn more about the data set provided by Alex
Cookson in [the data repository](https://github.com/tacookson/data) provided on GitHub, as
well as this corresponding [blog
post](https://www.alexcookson.com/post/most-successful-broadway-show-of-all-time/).


```r
glimpse(broadway)
#> Rows: 47,524
#> Columns: 8
#> $ week_ending      <date> 1985-06-09, 1985-06-09, 1985-06-…
#> $ show             <chr> "42nd Street", "A Chorus Line", "…
#> $ theatre          <chr> "St. James Theatre", "Sam S. Shub…
#> $ weekly_gross     <dbl> 282368, 222584, 249272, 95688, 61…
#> $ avg_ticket_price <dbl> 30.42, 27.25, 33.75, 20.87, 20.78…
#> $ top_ticket_price <dbl> NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ performances     <dbl> 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, …
#> $ previews         <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
```

You will notice that there are 47,524 rows and 8 columns. Each row uniquely represents a
show that occurred on a specific week. Each column contains information about a
show that occurred in a specific week in a specific theater.

### Question 1

How many performances occurred in total?


```r
broadway %>%
  summarise(total_performances = sum(performances))
#> # A tibble: 1 × 1
#>   total_performances
#>                <dbl>
#> 1             343967
```

### Question 2

How many performances occurred per week?


```r
broadway %>%
  group_by(week_ending) %>%
  summarise(total_num_performances = sum(performances), 
            .groups = 'drop')
#> # A tibble: 1,812 × 2
#>    week_ending total_num_performances
#>    <date>                       <dbl>
#>  1 1985-06-09                     137
#>  2 1985-06-16                     139
#>  3 1985-06-23                     134
#>  4 1985-06-30                     137
#>  5 1985-07-07                     136
#>  6 1985-07-14                     137
#>  7 1985-07-21                     137
#>  8 1985-07-28                     121
#>  9 1985-08-04                     121
#> 10 1985-08-11                     121
#> # … with 1,802 more rows
```

The code for answering this second question is similar to the first question, except that
we need to group by the week_ending variable which describes each distinct week. After
grouping by the week, we use the summarise function to sum up all the performances for
each week.

### Question 3

How many performances _and_ previews occurred per week?


```r
broadway %>%
  group_by(week_ending) %>%
  summarise(total_num_performances = sum(performances),
            total_num_previews = sum(previews),
            .groups = 'drop')
#> # A tibble: 1,812 × 3
#>    week_ending total_num_performances total_num_previews
#>    <date>                       <dbl>              <dbl>
#>  1 1985-06-09                     137                 16
#>  2 1985-06-16                     139                  9
#>  3 1985-06-23                     134                  6
#>  4 1985-06-30                     137                  8
#>  5 1985-07-07                     136                  1
#>  6 1985-07-14                     137                  0
#>  7 1985-07-21                     137                  0
#>  8 1985-07-28                     121                  0
#>  9 1985-08-04                     121                  0
#> 10 1985-08-11                     121                  0
#> # … with 1,802 more rows
```

Here, we are taking two sums, the sum of performances and the sum of previews, for each
distinct week.

### Question 4

How many performances occurred _per theatre_ within each week?



<pre><code class='language-r'><code>broadway %>%<br>&nbsp;&nbsp;group_by(week_ending, theatre) %>%<br>&nbsp;&nbsp;summarise(total_num_performances = sum(performances),<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style='color:red'>.groups = 'drop'</span>)<br>#> # A tibble: 45,776 × 3<br>#> &nbsp;&nbsp;&nbsp;week_ending theatre &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;total_num_perfo…<br>#> &nbsp;&nbsp;&nbsp;<date> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<chr> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<dbl><br>#> &nbsp;1 1985-06-09 &nbsp;46th Street Theatre &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8<br>#> &nbsp;2 1985-06-09 &nbsp;Ambassador Theatre &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8<br>#> &nbsp;3 1985-06-09 &nbsp;Booth Theatre &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8<br>#> &nbsp;4 1985-06-09 &nbsp;Broadhurst Theatre &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0<br>#> &nbsp;5 1985-06-09 &nbsp;Broadway Theatre &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8<br>#> &nbsp;6 1985-06-09 &nbsp;Brooks Atkinson Theatre &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8<br>#> &nbsp;7 1985-06-09 &nbsp;Circle in the Square Theatre &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8<br>#> &nbsp;8 1985-06-09 &nbsp;Edison Theatre &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> &nbsp;9 1985-06-09 &nbsp;Eugene O'Neill Theatre &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8<br>#> 10 1985-06-09 &nbsp;Gershwin Theatre &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0<br>#> # … with 45,766 more rows</code></code></pre>

This is similar to the second question, except we are grouping by two variables this time.
This means we first group the distinct weeks, and then for each week, we group by the
theatres and sum up the performances for each theatre by week. For example, for Week 1,
there were X performances for Theatre A, Y performances for Theatre B, and Z performances
for Theatre C.

Notice that we include the `.groups` argument within each `summarise()` function call
(highlighted in red). We mostly do this to keep the output clean, but you can learn more
about this argument by running`?summarise` in your console.

## Exercises

This section will ask you to complete exercises based on what you've learned from the
previous section.

### Exercise 1

How many theaters do we have in this data set?




```r
n_distinct()
#> [1] 0
```

```r
# Try naming it something simple and clear, like n_theatres
```




<!-- ```{r summarise-exercise-1-check} -->
<!-- grade_result(pass_if(~identical(.result, summarise_ex1_sol))) -->
<!-- ``` -->


### Exercise 2

How many shows occurred per week?




```r
n_distinct()
#> [1] 0
```

```r
# Try naming it something brief, like n_shows
```




<!-- ```{r summarise-exercise-2-check} -->
<!-- grade_result(pass_if(~identical(.result, summarise_ex2_sol))) -->
<!-- ``` -->

### Exercise 3

What is the average number of performances across all theatres per week?




```r
# Try naming it something descriptive, like avg_num_performances
```




<!-- ```{r summarise-exercise-3-check} -->
<!-- grade_result(pass_if(~identical(.result, summarise_ex3_sol))) -->
<!-- ``` -->


### Exercise 4

What is the minimum and maximum number of performances per week?




```r
# Try across()
```




<!-- ```{r summarise-exercise-4-check} -->
<!-- grade_result(pass_if(~identical(.result, summarise_ex4_sol))) -->
<!-- ``` -->

### Exercise 5

What is the average top ticket price? 




```r
# Try na.rm = TRUE
```




### Exercise 6

Which weeks did shows have no performances or previews?




```r
# Try arrange()
```





### Exercise 7

Select all the true statements about the `summarise()` function from dplyr.

<!-- ```{r summarise-exercise-7, echo = FALSE} -->
<!-- question("Which of these are true? Check all true statements.", -->
<!--          answer("summarise() can be used to summarize a variable into a single number.", -->
<!--                 correct = TRUE), -->
<!--          answer("summarise() can only use the same statistics as summary().", -->
<!--                 message = paste("summarise() does NOT use the same statistics as summary().", -->
<!--                 "We can use many more summary functions, and we can even define our own!")), -->
<!--          answer("summarise() can be applied on a group-level when used in combination with group_by().", -->
<!--                 correct = TRUE), -->
<!--          answer("summarise() and summarize() are two different functions.", -->
<!--                 message = "summarise() and summarize() are the same function within dplyr."), -->
<!--          answer("summarise() can only use summary functions that output a single number.", -->
<!--                 message = paste("summarise() cannot only output a single number summary.", -->
<!--                 "We can use functions like quantile() which outputs multiple numbers.")), -->
<!--          allow_retry = TRUE, -->
<!--          random_answer_order = TRUE) -->
<!-- ``` -->

## Common Mistakes & Errors

Below are some common mistakes and errors you may come across:

* You try to summarize a column that has NA values. Remember to include `na.rm = TRUE`.
* You try to summarize a column that is not available in the data set (i.e., you
misspelled the column name, or it's simply not in the data set).

## Next Steps

If you would like to read more about the `summarise()` function, here are some additional
resources you may find helpful:

- [R 4 Data Science: **Chapter 5.6** Grouped summaries with
summarise](https://r4ds.had.co.nz/transform.html#grouped-summaries-with-summarise).
- [R 4 Data Science: 5.6.4 Useful summary functions](https://r4ds.had.co.nz/transform.html#summarise-funs)














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
