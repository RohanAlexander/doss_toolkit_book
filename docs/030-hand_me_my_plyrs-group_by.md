


# group and ungroup

*Written by Matthew Wankiewicz and last updated on 7 October 2021.*


## Introduction

In this lesson, you will learn how to:

- Use the `group_by()` function in R
- Use the `group_by()` function with other functions in R.

Prerequisite skills include:

- Having R installed on your computer/Having RStudio Cloud.
- Having `tidyverse` installed on R.

Highlights:

- The `group_by` function allows you to group datasets by variables you choose.
- `group_by` works best when paired with other dplyr functions, either counting the number of items in a group or making new variables from groups.

![Image Source:https://github.com/allisonhorst/stats-illustrations/raw/master/rstats-artwork/group_by_ungroup.png, Allison Horst](https://github.com/allisonhorst/stats-illustrations/raw/master/rstats-artwork/group_by_ungroup.png){width=400 height=300}

## The content

A major part of data analysis is seeing how your data looks using particular groups and the `group_by` function is very helpful with this. The `group_by` function takes a data frame and allows you to use other functions to get an idea of what these groups look like. 

The `group_by` function is useful for conducting operations on your dataset when you want to break up the points by group. For example, if you have a data frame with the heights and weights of different animals, the `group_by` function is useful for finding things like the mean weight of each type of animal in the data frame. The function `ungroup` is used to remove the grouping done by the `group_by` function.

Normally, the `group_by` function is paired with other dplyr functions in order to conduct your analysis.

The `ungroup` function takes one argument, a grouped data frame that you want to ungroup. This is useful for ungrouping your data after you have run your analysis and want to work with the whole data frame again.

Brief Overview of the `group_by()` and `ungroup()` functions:

<iframe width="560" height="315" src="https://www.youtube.com/embed/011h7uREXAU" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Arguments

- **`group_by()`**: The two main arguments for `group_by` are the data you plan to analyze and variables you want to group. When you enter in the data you plan to analyze, it will be the first argument. You can either write the name of the dataset as the first argument or pipe it into the `group_by()` function. Once you have your dataset in the function, you then have to write in the variable names you plan to group. You can write as many variables as you want when using `group_by()`.

- **`ungroup()`**: The `ungroup()` function takes one argument, the grouped data that you want to ungroup. This is useful for ungrouping your data after you have run your analysis and want to work with the whole data frame again.


## Other Optional Arguments

- **`group_by()`**: The two optional arguments are .add and .drop. .add determines whether or not the function makes new groups in the data. .drop drops groups that were formed before-hand which we may not see in the data.

## Questions


```r
penguins_grouped <- penguins %>% 
  group_by(species)
head(penguins_grouped)
#> # A tibble: 6 × 8
#> # Groups:   species [1]
#>   species island    bill_length_mm bill_depth_mm
#>   <fct>   <fct>              <dbl>         <dbl>
#> 1 Adelie  Torgersen           39.1          18.7
#> 2 Adelie  Torgersen           39.5          17.4
#> 3 Adelie  Torgersen           40.3          18  
#> 4 Adelie  Torgersen           NA            NA  
#> 5 Adelie  Torgersen           36.7          19.3
#> 6 Adelie  Torgersen           39.3          20.6
#> # … with 4 more variables: flipper_length_mm <int>,
#> #   body_mass_g <int>, sex <fct>, year <int>
```

As you can see above, using the `group_by` function does not appear to do anything when it is done on its own. When you have a grouped data frame, you usually pair it with another function to get the data you want.


```r
penguins %>% 
  count()
#> # A tibble: 1 × 1
#>       n
#>   <int>
#> 1   344
```

The chunk above takes the penguins data frame and counts how many observations are included. The output is only one number which represent all of the penguins. In the chunk below, we will use the `group_by` function to see the number of penguins of each species present in the data frame.


```r
penguins %>% 
  group_by(species) %>% 
  count()
#> # A tibble: 3 × 2
#> # Groups:   species [3]
#>   species       n
#>   <fct>     <int>
#> 1 Adelie      152
#> 2 Chinstrap    68
#> 3 Gentoo      124
```

In the chunk above, I used the grouped data frame that was created in the chunk before and ran it with the `count` function. This allows us to see how many penguins of each species are present in the data frame.



```r
penguins %>% 
  group_by(species) %>% 
  # use na.rm to remove missing values
  summarise(average_weight = mean(body_mass_g, na.rm = T))
#> # A tibble: 3 × 2
#>   species   average_weight
#>   <fct>              <dbl>
#> 1 Adelie             3701.
#> 2 Chinstrap          3733.
#> 3 Gentoo             5076.
```

This chunk shows how we can use the `group_by` function with the `summarise` function to get summary statistics for each species. To do this, you can either take the grouped data frame and pipe it into the `summarise` function or you can use the `group_by` function on the initial data frame and then pipe that into the `summarise` function.



```r
penguins %>% 
  group_by(species) %>% 
  summarise(average_weight = mean(body_mass_g, na.rm = T),
            average_flipper_length = mean(flipper_length_mm, na.rm = T))
#> # A tibble: 3 × 3
#>   species   average_weight average_flipper_length
#>   <fct>              <dbl>                  <dbl>
#> 1 Adelie             3701.                   190.
#> 2 Chinstrap          3733.                   196.
#> 3 Gentoo             5076.                   217.
```

This is an example of using the `group_by` function and the `summarise` function after piping in your initial data frame. As you can see, there is another column present in the output, compared to the chart above. This was done by adding in another argument to the `summarise` function which now gives us the average flipper length of each species of penguin.


```r
penguins %>% 
  group_by(species, sex) %>% 
  summarise(average_weight = mean(body_mass_g, na.rm = T))
#> `summarise()` has grouped output by 'species'. You can override using the `.groups` argument.
#> # A tibble: 8 × 3
#> # Groups:   species [3]
#>   species   sex    average_weight
#>   <fct>     <fct>           <dbl>
#> 1 Adelie    female          3369.
#> 2 Adelie    male            4043.
#> 3 Adelie    <NA>            3540 
#> 4 Chinstrap female          3527.
#> 5 Chinstrap male            3939.
#> 6 Gentoo    female          4680.
#> 7 Gentoo    male            5485.
#> 8 Gentoo    <NA>            4588.
```
The `group_by` function can also be used with multiple variables. This is an example of using two variables to group our data, this time we will use species and sex. Once again, we can see that visually, the data doesn't look different but when we apply other functions to it, the data will appear differently. 


```r
penguins %>% 
  group_by(species, sex, year) %>% 
  summarise(average_weight = mean(body_mass_g, na.rm = T))
#> `summarise()` has grouped output by 'species', 'sex'. You can override using the `.groups` argument.
#> # A tibble: 22 × 4
#> # Groups:   species, sex [8]
#>    species   sex     year average_weight
#>    <fct>     <fct>  <int>          <dbl>
#>  1 Adelie    female  2007          3390.
#>  2 Adelie    female  2008          3386 
#>  3 Adelie    female  2009          3335.
#>  4 Adelie    male    2007          4039.
#>  5 Adelie    male    2008          4098 
#>  6 Adelie    male    2009          3995.
#>  7 Adelie    <NA>    2007          3540 
#>  8 Chinstrap female  2007          3569.
#>  9 Chinstrap female  2008          3472.
#> 10 Chinstrap female  2009          3523.
#> # … with 12 more rows
```

This output shows us the average weights of the penguins, when grouped by species and sex. We can see that there are levels for each of the three species (Adelie, Chinstrap and Gentoo) and the three gender levels present (Male, Female and NA).


```r
penguins %>% 
  group_by(species, sex) %>% 
  filter(body_mass_g == max(body_mass_g))
#> # A tibble: 7 × 8
#> # Groups:   species, sex [6]
#>   species   island bill_length_mm bill_depth_mm
#>   <fct>     <fct>           <dbl>         <dbl>
#> 1 Adelie    Biscoe           43.2          19  
#> 2 Adelie    Biscoe           39.6          20.7
#> 3 Gentoo    Biscoe           49.2          15.2
#> 4 Gentoo    Biscoe           46.5          14.8
#> 5 Gentoo    Biscoe           45.2          14.8
#> 6 Chinstrap Dream            46            18.9
#> 7 Chinstrap Dream            52            20.7
#> # … with 4 more variables: flipper_length_mm <int>,
#> #   body_mass_g <int>, sex <fct>, year <int>
```

The `group_by` function also works with the `filter` function. The chunk above gives us the penguins with the largest body mass for each of the groups we created. 


```r
penguins %>% 
  group_by(species) %>% 
  count()
#> # A tibble: 3 × 2
#> # Groups:   species [3]
#>   species       n
#>   <fct>     <int>
#> 1 Adelie      152
#> 2 Chinstrap    68
#> 3 Gentoo      124

penguins %>% 
  group_by(species) %>% 
  ungroup() %>% 
  count()
#> # A tibble: 1 × 1
#>       n
#>   <int>
#> 1   344
```

This chunk demonstrates the `ungroup` function. The output of the first code is the same as one of the previous examples, it gives us the number of penguins present for each species. 

The second group of code shows us what `ungroup` does. The `ungroup` function was placed just before the `count` function so instead of giving us the number of penguins in each species, we get the number of penguins in the whole data frame.

**Brief Overview of the `group_by()` and `ungroup()` functions**:

<iframe width="560" height="315" src="https://www.youtube.com/embed/011h7uREXAU" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Exercises

**1.** Use the group_by function to count how many penguins were studied each year and also group them by their sex. Remember the data frame is called "penguins" and the year variable is called "year", sex is called "sex".



```r
## FINAL SOLUTION ## 
penguins %>% 
  group_by(year, sex) %>% 
  count()
#> # A tibble: 9 × 3
#> # Groups:   year, sex [9]
#>    year sex        n
#>   <int> <fct>  <int>
#> 1  2007 female    51
#> 2  2007 male      52
#> 3  2007 <NA>       7
#> 4  2008 female    56
#> 5  2008 male      57
#> 6  2008 <NA>       1
#> 7  2009 female    58
#> 8  2009 male      59
#> 9  2009 <NA>       3

## OR ##

penguins %>% 
  group_by(year, sex) %>% 
  summarise(n = n())
#> `summarise()` has grouped output by 'year'. You can override using the `.groups` argument.
#> # A tibble: 9 × 3
#> # Groups:   year [3]
#>    year sex        n
#>   <int> <fct>  <int>
#> 1  2007 female    51
#> 2  2007 male      52
#> 3  2007 <NA>       7
#> 4  2008 female    56
#> 5  2008 male      57
#> 6  2008 <NA>       1
#> 7  2009 female    58
#> 8  2009 male      59
#> 9  2009 <NA>       3
```

**2.** Using the penguins data frame, group by both `island`, `sex` and `species` and give the average bill length (`bill_length_mm`), average bill depth (`bill_depth_mm`) and the difference between average bill length and average bill depths.



```r
penguins %>% 
  group_by(island, sex, species) %>% 
  summarise(avg_length = mean(bill_length_mm, na.rm = T),
            avg_depth = mean(bill_depth_mm, na.rm = T),
            diff_depth = mean(bill_length_mm) - mean(bill_depth_mm))
#> `summarise()` has grouped output by 'island', 'sex'. You can override using the `.groups` argument.
#> # A tibble: 13 × 6
#> # Groups:   island, sex [9]
#>    island    sex    species   avg_length avg_depth diff_depth
#>    <fct>     <fct>  <fct>          <dbl>     <dbl>      <dbl>
#>  1 Biscoe    female Adelie          37.4      17.7       19.7
#>  2 Biscoe    female Gentoo          45.6      14.2       31.3
#>  3 Biscoe    male   Adelie          40.6      19.0       21.6
#>  4 Biscoe    male   Gentoo          49.5      15.7       33.8
#>  5 Biscoe    <NA>   Gentoo          45.6      14.6       NA  
#>  6 Dream     female Adelie          36.9      17.6       19.3
#>  7 Dream     female Chinstrap       46.6      17.6       29.0
#>  8 Dream     male   Adelie          40.1      18.8       21.2
#>  9 Dream     male   Chinstrap       51.1      19.3       31.8
#> 10 Dream     <NA>   Adelie          37.5      18.9       18.6
#> 11 Torgersen female Adelie          37.6      17.6       20.0
#> 12 Torgersen male   Adelie          40.6      19.4       21.2
#> 13 Torgersen <NA>   Adelie          37.9      18.2       NA
# na.rm = T is optional, safer to use it if you're unsure if 
# your data contains NA's
```


Solution to Exercise 1:

<iframe width="560" height="315" src="https://www.youtube.com/embed/pTuGhkNCTnc" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Solution to Exercise 2:

<iframe width="560" height="315" src="https://www.youtube.com/embed/Dr4b18O-aGo" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Common Mistakes & Errors

Sometimes, you will encounter some errors in the `group_by` function. In this section, we'll cover what you should do when some of the common errors occur.

1. Error: Must group by variables found in `.data`

When this occurs, you are probably trying to group your data frame by a variable that isn't in the data frame. Often times, this happens because of a typo in the variable you want to select.

2. Error in eval(lhs, parent, parent) : object 'totally_real_data_frame' not found

When this error occurs, R is telling us that the data frame we are trying to make groups from does not exist. Once again, this is usually because of a typo.

3. Error in group_by(data) : could not find function "group_by"

When this occurs, it means that R can't find the `group_by` function. To fix this, you should try to load the `tidyverse` library in.

Some mistakes that you may run into when using `group_by` and `ungroup`:

* Calling for variables that are not in the data frame you plan to analyze (usually typos).

* Not calling in the tidyverse/dplyr library in R.

* Sometimes you can encounter difficulties with other functions, usually, typos will be the biggest issue.

## Next Steps

Now that you have got some experience with the `group_by` and `ungroup` functions, these links are useful resources to expand your understanding.

  - R for Data Science contains the `group_by` function with other dplyr functions: https://r4ds.had.co.nz/transform.html

  - Section 6.11 of OHI Data Science Training looks at the `group_by` function: https://ohi-science.org/data-science-training/dplyr.html#group_by-operates-on-groups)











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
