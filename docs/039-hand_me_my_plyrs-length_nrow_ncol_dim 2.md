


# length, rows, columns and dimensions

Written by Isaac Ehrlich and last updated on 7 October 2021.*

## Introduction

Understanding the size and dimensions of your variables can be important in a variety of contexts.

In this lesson, you will learn how to

- Use `length()` to find the length of vectors
- Use `nrow()` and `ncol()` to find the dimensions of matrices and data frames
- Use `dim()` to find and set dimensions

Prerequisites:

- Understanding how to create vectors and data frames and their basic principles

## Arguments

### length()
`length()` returns the length (number of items) in a vector. The only argument that `length()` takes is the vector.


```r
x <- c("a", "b", "c", "d")
length(x)
#> [1] 4
```


### nrow() and ncol()

`nrow()` and `ncol()` return the number of rows and columns of a matrix or data frame, respectively. The only argument that `nrow()` and `ncol()` take is the matrix or data frame.


```r
df <- data.frame(col1 = c("a", "b", "c", "d"), col2 = c(1,2,3,4))
df
#>   col1 col2
#> 1    a    1
#> 2    b    2
#> 3    c    3
#> 4    d    4

# Number of Rows:
nrow(df)
#> [1] 4

# Number of Columns:
ncol(df)
#> [1] 2
```

### dim()

`dim()` returns a vector with two elements that denote the dimensions of a matrix or data frame, in the order 'number of rows', 'number of columns'. The first element is equivalent to the output of `nrow()` and the second to that of `ncol()`. Similarly to `nrow()` and `ncol()`, the only argument that `dim()` takes is the matrix or data frame.

```r
# Dimensions of data frame:
dim(df)
#> [1] 4 2

# Note the relationship between 'dim()', 'nrow()', and 'ncol()'
dim(df)[1] == nrow(df)
#> [1] TRUE
dim(df)[2] == ncol(df)
#> [1] TRUE
```

Unlike `nrow()` and `ncol()` however, `dim()` can also be used to set the dimensions of a vector or matrix. Setting dimensions for a vector will turn it into a matrix.

```r
# Create a vector
x <- c("a", "b", "c", "d")
# Check dimensions of x - should output NULL since vectors do not have dimensions
dim (x)
#> NULL

# Set and check new dimensions
dim(x) <- c(2, 2)
dim(x)
#> [1] 2 2

# Output 'x'
x
#>      [,1] [,2]
#> [1,] "a"  "c" 
#> [2,] "b"  "d"
```

Setting new dimensions for an existing matrix will reshape it.

```r
# Create a matrix and check its dimensions
m <- matrix(1:12)
dim(m)
#> [1] 12  1

# Set and check new dimensions
dim(m) <- c(3,4)
dim(m)
#> [1] 3 4
```


### `dplyr::bind_rows()` and `dplyr::bind_cols()`

Finally, it is worth mentioning that there are also `dplyr` versions of `rbind()` and `cbind()`. `dplyr::bind_rows()` is actually a bit more robust since it doesn't require the input data frames to have the same number of columns. If you are making extensive use of `rbind()` and `cbind()`, then exploring their `dplyr` counterparts would be worthwhile.


## Questions and Exercises

###  length()

For questions about `length()` we will be using the built in vector `fruit`, a vector of fruit names.

**1.**

<!-- ```{r length-q1, echo = FALSE} -->
<!-- question("length() returns the following information:", -->
<!-- answer("The number of characters in a string"), -->
<!-- answer("The number of objects in a vector", correct = TRUE), -->
<!-- answer("The length (in centimeters) printing a vector will occupy on your screen"), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->


<!-- **2. Save the length of the vector `fruit` as the variable `fruit_len`** -->

<!-- ```{r length-q2, echo = FALSE, exercise = TRUE} -->
<!-- # Add a function around fruit -->
<!-- fruit_len <- fruit -->
<!-- fruit_len -->
<!-- ``` -->

<!-- ```{r length-q2-solution} -->
<!-- fruit_len <- length(fruit) -->
<!-- ``` -->

<!-- **3. Using indexing and the `length()` function, return the final object in `fruit`** -->

<!-- ```{r length-q3, echo = FALSE, exercise = TRUE} -->
<!-- # Enter your code below -->

<!-- last_fruit <- fruit -->
<!-- last_fruit -->
<!-- ``` -->

<!-- ```{r length-q3-solution} -->
<!-- last_fruit <- fruit[length(fruit)] -->
<!-- ``` -->

### nrow() and ncol()

For questions about `nrow()` and `ncol()` we will be using the data frame `starwars`, which contains Star Wars characters and information about them, and a secret matrix.

**1. Save the number of rows and number of columns in `starwars`**

<!-- ```{r nrow-q1, echo = FALSE, exercise = TRUE} -->
<!-- # Enter your code below -->

<!-- starwars_rows <- starwars -->
<!-- starwars_cols <- starwars -->

<!-- starwars_rows -->
<!-- starwars_cols -->
<!-- ``` -->

<!-- ```{r nrow-q1-solution} -->
<!-- starwars_rows <- nrow(starwars) -->
<!-- starwars_cols <- ncol(starwars) -->
<!-- ``` -->

**2. I've created a matrix, `secret_matrix`, the dimensions of which are a secret. Without printing out the number of rows and columns, check to see if `secret_matrix` is a square matrix (i.e. it has the same number of rows and columns)**




<!-- ```{r nrow-q2, echo = FALSE, exercise = TRUE} -->
<!-- # Enter your code below -->

<!-- ``` -->

<!-- ```{r nrow-q2-solution} -->
<!-- nrow(secret_matrix) == ncol(secret_matrix) -->
<!-- ``` -->

**3. Using indexing, `nrow()`, and `ncol()`, in one line, save the value in the bottom right corner of the matrix `secret_matrix`.**

<!-- ```{r nrow-q3, echo = FALSE, exercise = TRUE} -->
<!-- # Enter your code below -->
<!-- bottom_right_value <- secret_matrix[] -->

<!-- bottom_right_value -->
<!-- ``` -->

<!-- ```{r nrow-q3-solution} -->
<!-- bottom_right_value <- secret_matrix[nrow(secret_matrix), ncol(secret_matrix)] -->
<!-- ``` -->

### dim()

<!-- **1.** -->
<!-- ```{r dim-q1, echo = FALSE} -->
<!-- question("Which of the following are true about the relationship between 'dim()', 'nrow()', and 'ncol()'? Select all that apply.", -->
<!-- answer("There is no relationship"), -->
<!-- answer("The first element of the output of dim(x) is equal to the output of nrow(x)", correct = TRUE), -->
<!-- answer("It depends on whether or not the input is a matrix or data frame"), -->
<!-- answer("The second element of the output of dim(x) is equal to the output of ncol(x)", correct = TRUE), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

**2. Use `dim()` to turn the `fruit` vector into a matrix with 8 rows and 10 columns**

<!-- ```{r dim-q2, exercise = TRUE} -->
<!-- # Enter your code here -->

<!-- dim(fruit) -->
<!-- ``` -->

<!-- ```{r dim-q2-solution} -->
<!-- dim(fruit) <- c(8, 10) -->
<!-- ``` -->


## Special Cases & Common Mistakes

### length()

* Remember that `length()` returns the number of objects in a vector, not the number of digits or characters in a string. See examples below.

```r
length("This sentence has 31 characters")
#> [1] 1
length(c("This sentence has 31 characters", "This sentence has 7 less"))
#> [1] 2
```

* Although a vector is the correct input into `length()`, if the input is a dataframe, the output will be equal to the number of columns.

```r
length(starwars) == ncol(starwars)
#> [1] TRUE
```

* If the input is a matrix, the output will be equal to the number of entries in the matrix.

```r
length(secret_matrix) == nrow(secret_matrix) * ncol(secret_matrix)
#> [1] TRUE
```


### nrow() and ncol()

* Using a vector as input to `nrow()`, `ncol()`, or `dim()` will output `NULL`

```r
# Check dimensions of 'letters', a built-in vector of English letters
nrow(letters)
#> NULL
ncol(letters)
#> NULL
dim(letters)
#> NULL
```


## Overview and Next Steps

`length()`, `nrow()`, and `ncol()`, are useful functions for finding the dimensions of variables. In the next section, we will continue exploring data frames and how to manipulate them.







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
