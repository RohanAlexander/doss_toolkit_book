



# filter

Written by Shirley Deng.


## What is `dplyr::filter()` for?

The `dplyr::filter()` function is used to extract rows from a given dataframe following given criteria, and any rows that do not meet this criteria are dropped.

This criteria is written in the form of logical conditions that can be evaluated. For example, if a dataframe `ToothGrowth` has a variable called `len` for lengths, we can extract all of the rows such that `len` is equal to 22.0 with the expression `len == 22.0`. We can have one single condition, or several conditions.

Some useful functions and operators include the following:

*  `==`, `>`, `<`, `>=`, `<=`
* `&`, `|`, `!`, `xor()`
* `is.na()`

`dplyr::filter()` is similar to extracting a subset of rows with square brackets in base R, `[]`. However, in the case that evaluating our conditions on a row results in `NA`s, `dplyr::filter()` drops these rows whereas `[]` would continue to extract them. For this reason, `dplyr::filter()` may be preferred when there may be `NA`s.


## What arguments does `dplyr::filter()` take?

* `.data`: the dataframe we're working with
* `...`: the conditions for the rows we want to extract
* `.preserve`: whether or not we want to preserve the grouping of the `.data` dataframe

## What value does `dplyr::filter()` return?

`dplyr::filter()` returns a dataframe retaining all of the same characteristics as the `.data` argument, except only a subset of the rows, based on the conditions or criteria we used to extract this subset. Namely, this means that the columns are unmodified, and the order of the rows remains the same.

## Practice 

How can we check if 2+2 is greater than or equal to 2*2? Try coding it below.




```r
2+2 >= 2*2
#> [1] TRUE
```

## Coding Examples

The following is code similar to that from the video lesson in the previous section.

First, we begin by installing the `dplyr` package:


```r
install.packages("dplyr", repos = "http://cran.us.r-project.org")
```

Next, we load the `dplyr` package:


```r
library(dplyr)
```

Now, we want to prepare a dataframe for us to work with. We will make use of the `ToothGrowth` dataset built into R. 

We can take a look at what this dataset is about:


```r
?ToothGrowth
```

And take a look at the first few rows of observations:


```r
head(ToothGrowth)
#>    len supp dose
#> 1  4.2   VC  0.5
#> 2 11.5   VC  0.5
#> 3  7.3   VC  0.5
#> 4  5.8   VC  0.5
#> 5  6.4   VC  0.5
#> 6 10.0   VC  0.5
```

We want to add an additional variable for the colour of the guinea pigs.

We need to set a seed to ensure we get the same results every time the code is run. We chose the number `123`:


```r
set.seed(123)
```

Now, we create our colour variable by taking a sample of guinea pig fur colours. We use the `sample()` function for this:


```r
colour <- sample(x=c("black", "brown", "grey", "cream", "white", "multi"),
                 size=nrow(ToothGrowth),
                 replace=TRUE)
colour
#>  [1] "grey"  "multi" "grey"  "brown" "brown" "multi" "grey" 
#>  [8] "white" "cream" "multi" "multi" "black" "brown" "grey" 
#> [15] "white" "grey"  "grey"  "black" "cream" "black" "black"
#> [22] "white" "grey"  "brown" "brown" "black" "multi" "grey" 
#> [29] "cream" "multi" "black" "grey"  "white" "cream" "brown"
#> [36] "white" "black" "black" "brown" "grey"  "cream" "white"
#> [43] "white" "grey"  "multi" "black" "brown" "white" "white"
#> [50] "cream" "white" "brown" "black" "black" "grey"  "black"
#> [57] "multi" "white" "black" "brown"
```

And now we create a new dataframe that combines `ToothGrowth` with our `colour` variable using `data.frame()`. We'll also take a look at the frist few observations.


```r
guineas <- data.frame(ToothGrowth, colour)
head(guineas)
#>    len supp dose colour
#> 1  4.2   VC  0.5   grey
#> 2 11.5   VC  0.5  multi
#> 3  7.3   VC  0.5   grey
#> 4  5.8   VC  0.5  brown
#> 5  6.4   VC  0.5  brown
#> 6 10.0   VC  0.5  multi
```

We notice that it looks the same as the original `ToothGrowth` dataframe, but with our added `colour` variable.

We can now move onto trying out the `dplyr::filter()` function!

First, we try extracting a subset of rows using only one condition: that the guinea pigs are brown in colour.


```r
brown_guineas <- filter(guineas, colour == "brown")
brown_guineas
#>     len supp dose colour
#> 1   5.8   VC  0.5  brown
#> 2   6.4   VC  0.5  brown
#> 3  15.2   VC  1.0  brown
#> 4  25.5   VC  2.0  brown
#> 5  26.4   VC  2.0  brown
#> 6  14.5   OJ  0.5  brown
#> 7  16.5   OJ  0.5  brown
#> 8  25.8   OJ  1.0  brown
#> 9  26.4   OJ  2.0  brown
#> 10 23.0   OJ  2.0  brown
```

Next, we try using two conditions: that the guinea pigs are white in colour, and received a supplement dosage of 1.0 mg/day.


```r
white_1_guineas <- guineas %>% filter(colour == "white", dose == 1.0)
white_1_guineas
#>    len supp dose colour
#> 1 22.5   VC    1  white
#> 2 23.3   OJ    1  white
#> 3 23.6   OJ    1  white
#> 4 21.2   OJ    1  white
#> 5 14.5   OJ    1  white
```

Now, we want to see what happens when our conditions evaluate as `NA`s.

First, we try a condition that evaluates all of the rows as `NA`s with `dplyr::filter()`:


```r
no_guineas <- guineas %>% filter(dose/0 == 2)
no_guineas
#> [1] len    supp   dose   colour
#> <0 rows> (or 0-length row.names)
```

And now with the square brackets `[]` in base R:


```r
some_guineas <- guineas[guineas$dose /0 == 2]
some_guineas
#> data frame with 0 columns and 60 rows
```

We notice that using `dplyr::filter()` we extracted no rows, whereas using the square brackets we extracted all of the rows but no columns.

Lastly, we want to see how `dplyr::filter()` works on grouped dataframes.

We begin by greating a grouped version of our `guineas` dataframe, through grouping by colour:


```r
grouped_guineas <- guineas %>% group_by(colour)
grouped_guineas
#> # A tibble: 60 × 4
#> # Groups:   colour [6]
#>      len supp   dose colour
#>    <dbl> <fct> <dbl> <chr> 
#>  1   4.2 VC      0.5 grey  
#>  2  11.5 VC      0.5 multi 
#>  3   7.3 VC      0.5 grey  
#>  4   5.8 VC      0.5 brown 
#>  5   6.4 VC      0.5 brown 
#>  6  10   VC      0.5 multi 
#>  7  11.2 VC      0.5 grey  
#>  8  11.2 VC      0.5 white 
#>  9   5.2 VC      0.5 cream 
#> 10   7   VC      0.5 multi 
#> # … with 50 more rows
```

And then we try filtering by receiving orange juice as the supplement, while preserving the grouping:


```r
orange_grouped_guineas <- grouped_guineas %>% filter(supp == "OJ", preserve=TRUE)
orange_grouped_guineas
#> # A tibble: 30 × 4
#> # Groups:   colour [6]
#>      len supp   dose colour
#>    <dbl> <fct> <dbl> <chr> 
#>  1  15.2 OJ      0.5 black 
#>  2  21.5 OJ      0.5 grey  
#>  3  17.6 OJ      0.5 white 
#>  4   9.7 OJ      0.5 cream 
#>  5  14.5 OJ      0.5 brown 
#>  6  10   OJ      0.5 white 
#>  7   8.2 OJ      0.5 black 
#>  8   9.4 OJ      0.5 black 
#>  9  16.5 OJ      0.5 brown 
#> 10   9.7 OJ      0.5 grey  
#> # … with 20 more rows
```


## Exercises

Let's go over some common mistakes, and then try using the filter() function ourselves.

Make sure you're using `==` instead of `=`. Try changing the `==` to `=` below:

```r
filter(guineas, colour == "brown")
#>     len supp dose colour
#> 1   5.8   VC  0.5  brown
#> 2   6.4   VC  0.5  brown
#> 3  15.2   VC  1.0  brown
#> 4  25.5   VC  2.0  brown
#> 5  26.4   VC  2.0  brown
#> 6  14.5   OJ  0.5  brown
#> 7  16.5   OJ  0.5  brown
#> 8  25.8   OJ  1.0  brown
#> 9  26.4   OJ  2.0  brown
#> 10 23.0   OJ  2.0  brown
```

Make sure you're using quotation marks for strings, or R will read them as variable names. Try removing the quotation marks around `brown` below:

```r
filter(guineas, colour == "brown")
#>     len supp dose colour
#> 1   5.8   VC  0.5  brown
#> 2   6.4   VC  0.5  brown
#> 3  15.2   VC  1.0  brown
#> 4  25.5   VC  2.0  brown
#> 5  26.4   VC  2.0  brown
#> 6  14.5   OJ  0.5  brown
#> 7  16.5   OJ  0.5  brown
#> 8  25.8   OJ  1.0  brown
#> 9  26.4   OJ  2.0  brown
#> 10 23.0   OJ  2.0  brown
```

Onto the exercises!

Extract all guinea pigs that were given the ascorbic acid Vitamin C supplement.




```r
guineas %>% filter(supp=="VC")
#>     len supp dose colour
#> 1   4.2   VC  0.5   grey
#> 2  11.5   VC  0.5  multi
#> 3   7.3   VC  0.5   grey
#> 4   5.8   VC  0.5  brown
#> 5   6.4   VC  0.5  brown
#> 6  10.0   VC  0.5  multi
#> 7  11.2   VC  0.5   grey
#> 8  11.2   VC  0.5  white
#> 9   5.2   VC  0.5  cream
#> 10  7.0   VC  0.5  multi
#> 11 16.5   VC  1.0  multi
#> 12 16.5   VC  1.0  black
#> 13 15.2   VC  1.0  brown
#> 14 17.3   VC  1.0   grey
#> 15 22.5   VC  1.0  white
#> 16 17.3   VC  1.0   grey
#> 17 13.6   VC  1.0   grey
#> 18 14.5   VC  1.0  black
#> 19 18.8   VC  1.0  cream
#> 20 15.5   VC  1.0  black
#> 21 23.6   VC  2.0  black
#> 22 18.5   VC  2.0  white
#> 23 33.9   VC  2.0   grey
#> 24 25.5   VC  2.0  brown
#> 25 26.4   VC  2.0  brown
#> 26 32.5   VC  2.0  black
#> 27 26.7   VC  2.0  multi
#> 28 21.5   VC  2.0   grey
#> 29 23.3   VC  2.0  cream
#> 30 29.5   VC  2.0  multi
```

Extract all guinea pigs that were given the orange juice supplement at a dose of 0.5 mg/day.




```r
guineas %>% filter(supp=="OJ", dose==0.5)
#>     len supp dose colour
#> 1  15.2   OJ  0.5  black
#> 2  21.5   OJ  0.5   grey
#> 3  17.6   OJ  0.5  white
#> 4   9.7   OJ  0.5  cream
#> 5  14.5   OJ  0.5  brown
#> 6  10.0   OJ  0.5  white
#> 7   8.2   OJ  0.5  black
#> 8   9.4   OJ  0.5  black
#> 9  16.5   OJ  0.5  brown
#> 10  9.7   OJ  0.5   grey
```


## Additional Resources

* [`dplyr:filter()` reference page](https://dplyr.tidyverse.org/reference/filter.html)












