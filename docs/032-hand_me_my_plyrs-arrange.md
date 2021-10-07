


# arrange

*Written by Isaac Ehrlich and last updated on 7 October 2021.*


## Introduction

Sometimes, you may want to view a dataset in a specific order. Data sets will often be displayed in the order the data were input, but you may want to view it sorted by a different variable. You can use the tidyverse `arrange()` function, to order a data set by a specific column.

## arrange()

The `arrange()` function takes in a data frame and columns to sort by as its input, and will output the re-ordered data frame. `arrange()` does not modify any values in your data, it only changes the presentation.

Let's take a look at a simple example using R's `mtcars` data set:


```r
head(mtcars)
#>                    mpg cyl disp  hp drat    wt  qsec vs am
#> Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1
#> Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1
#> Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1
#> Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0
#> Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0
#> Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0
#>                   gear carb
#> Mazda RX4            4    4
#> Mazda RX4 Wag        4    4
#> Datsun 710           4    1
#> Hornet 4 Drive       3    1
#> Hornet Sportabout    3    2
#> Valiant              3    1
```

There's a lot of information in this data, like miles per gallon, number of cylinders, and displacement, but it doesn't seem to be ordered in any way.

Supposing we want to order the data frame by miles per gallon (i.e. see cars with lowest mpg at the top and highest mpg at the bottom), we can pass the following function:


```r
head(arrange(mtcars, mtcars$mpg))
#>                      mpg cyl disp  hp drat    wt  qsec vs
#> Cadillac Fleetwood  10.4   8  472 205 2.93 5.250 17.98  0
#> Lincoln Continental 10.4   8  460 215 3.00 5.424 17.82  0
#> Camaro Z28          13.3   8  350 245 3.73 3.840 15.41  0
#> Duster 360          14.3   8  360 245 3.21 3.570 15.84  0
#> Chrysler Imperial   14.7   8  440 230 3.23 5.345 17.42  0
#> Maserati Bora       15.0   8  301 335 3.54 3.570 14.60  0
#>                     am gear carb
#> Cadillac Fleetwood   0    3    4
#> Lincoln Continental  0    3    4
#> Camaro Z28           0    3    4
#> Duster 360           0    3    4
#> Chrysler Imperial    0    3    4
#> Maserati Bora        1    5    8
```

Note, `arrange()` by default sorts in ascending order. If we want to sort in descending order, we can pass `desc()` to the column names:


```r
head(arrange(mtcars, desc(mtcars$mpg)))
#>                 mpg cyl  disp  hp drat    wt  qsec vs am
#> Toyota Corolla 33.9   4  71.1  65 4.22 1.835 19.90  1  1
#> Fiat 128       32.4   4  78.7  66 4.08 2.200 19.47  1  1
#> Honda Civic    30.4   4  75.7  52 4.93 1.615 18.52  1  1
#> Lotus Europa   30.4   4  95.1 113 3.77 1.513 16.90  1  1
#> Fiat X1-9      27.3   4  79.0  66 4.08 1.935 18.90  1  1
#> Porsche 914-2  26.0   4 120.3  91 4.43 2.140 16.70  0  1
#>                gear carb
#> Toyota Corolla    4    1
#> Fiat 128          4    1
#> Honda Civic       4    2
#> Lotus Europa      5    2
#> Fiat X1-9         4    1
#> Porsche 914-2     5    2
```

## Additional Examples

### Characters

`arrange()` can also sort by character vectors. In this case, `arrange()` by default will sort alphabetically. Let's take a look at R's `HairEyeColor` data set ordered by hair color:


```r
HairEyeColor <- data.frame(HairEyeColor)
head(arrange(HairEyeColor, HairEyeColor$Hair))
#>    Hair   Eye    Sex Freq
#> 1 Black Brown   Male   32
#> 2 Black  Blue   Male   11
#> 3 Black Hazel   Male   10
#> 4 Black Green   Male    3
#> 5 Black Brown Female   36
#> 6 Black  Blue Female    9
```

### Multiple Arguments

If you pass multiple columns into arrange, it will order by columns in the order they are passed. For example, in the code below, we order the `HairEyeColor` first by hair color and then by frequency.


```r
head(arrange(HairEyeColor, HairEyeColor$Hair, HairEyeColor$Freq))
#>    Hair   Eye    Sex Freq
#> 1 Black Green Female    2
#> 2 Black Green   Male    3
#> 3 Black Hazel Female    5
#> 4 Black  Blue Female    9
#> 5 Black Hazel   Male   10
#> 6 Black  Blue   Male   11
```

We can see that the data was first ordered alphabetically by hair color, followed by frequency.


## Practice Questions

For the following questions, please refer to R's `quakes` data set:


```r
head(quakes)
#>      lat   long depth mag stations
#> 1 -20.42 181.62   562 4.8       41
#> 2 -20.62 181.03   650 4.2       15
#> 3 -26.00 184.10    42 5.4       43
#> 4 -17.97 181.66   626 4.1       19
#> 5 -20.42 181.96   649 4.0       11
#> 6 -19.68 184.31   195 4.0       12
```

<!-- ```{r arrangeq1, echo = FALSE} -->
<!-- question("arrange() by default sorts in descending order", -->
<!-- answer("True"), -->
<!-- answer("False", correct = TRUE), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

<!-- ```{r arrangeq2, echo = FALSE} -->
<!-- question("Select the correct code to sort 'quakes' by magnitude in descending order", -->
<!-- answer("arrange(quakes, quakes$mag)", -->
<!--        message = "Remember the default!"), -->
<!-- answer("arrange(quakes, quakes$stations, desc(quakes$mag))", -->
<!--        message = "Keep in mind what you want to sort by!"), -->
<!-- answer("arrange(quakes, desc(quakes$mag)", correct = TRUE), -->
<!-- answer("arrange(desc(quakes), quakes$mag)", -->
<!--        message = "Remember what you apply 'desc()' to!"), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

<!-- ```{r arrangeq3, echo = FALSE} -->
<!-- question("Select the correct code to sort 'quakes' by magnitude and then by depth", -->
<!-- answer("arrange(quakes, quakes$mag, quakes$depth)", correct = TRUE), -->
<!-- answer("arrange(quakes, quakes$depth, quakes$mag))", -->
<!--        message = "Keep in mind the order you want to sort by!"), -->
<!-- answer("arrange(quakes$mag, quakes$depth)", -->
<!--        message = "Don't forget the first argument!"), -->
<!-- answer("arrange(quakes, c(quakes$mag, quakes$depth))", -->
<!--        message = "Keep in mind how to pass multiple arguments!"), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

## Practice Coding

The following questions will ask you to use the arrange function on your own.
For these questions, please refer to R's `quakes` data set:


```r
head(quakes)
#>      lat   long depth mag stations
#> 1 -20.42 181.62   562 4.8       41
#> 2 -20.62 181.03   650 4.2       15
#> 3 -26.00 184.10    42 5.4       43
#> 4 -17.97 181.66   626 4.1       19
#> 5 -20.42 181.96   649 4.0       11
#> 6 -19.68 184.31   195 4.0       12
```

1. Arrange the data in quakes so that it is ordered by magnitude and then by stations, both in descending order

<!-- ```{r arrangeq4, exercise = TRUE} -->

<!-- ``` -->

## Special Cases and Common Errors

### NA Values

Regardless of if you are sorting in ascending or descending order, NA values will be sent to the bottom of your reordered data frame.

### Common Errors

1. The first input to arrange must be of type "data.frame," it cannot be applied to objects that are tables or matrices. Make sure to convert to a data frame using `as.data.frame()` if needed.

2. Make sure you are properly calling your column names to order by. There are several ways to do this - the expressions below all output the same result.
* `arrange(quakes, quakes$mag)`
* `arrange(quakes, col = mag)`
* `quakes %>% arrange(mag)`

Other errors are bound to pop up. Remember that Stack Overflow is your best friend!

## Overview

`arrange()` is a useful function for reorganizing the structure of your data set. While it does not change any values, it may be useful if you need to order you data by a certain variable, or even just for easier viewing.

The following video summarizes what we have gone over in this tutorial: ![](https://www.youtube.com/watch?v=Ni6_PEzqLGQ&ab_channel=DOSSToolkit)


















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
