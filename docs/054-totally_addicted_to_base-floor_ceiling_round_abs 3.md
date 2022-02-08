


# floor(), ceiling(), round(), and abs()

*Written by José Casas and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- Use `floor()` and `ceiling()` to get the floor and ceiling of a number, respectively.
- Use `round()` to round a number to a specified number of decimal places.
- Use `abs()` to compute the absolute value of a number.

Prerequisites:

- Basic knowledge of R.

All of the following functions can only take numeric or logical (TRUE and FALSE) objects, and NA. These functions also work with vectors of those types.

## `floor()` and `ceiling()`

The floor and ceiling of a number are defined as the nearest integer less than and greater than that number, respectively. The floor and ceiling of an integer number are the same number.

Here, we will use `floor()` and `ceiling()` to get the floor and ceiling of a single number. For this, simply put a number as the function argument:


```r
floor(3.5)
#> [1] 3
ceiling(7.3)
#> [1] 8
ceiling(-12.8)
#> [1] -12
```

`floor()` and `ceiling()` can also take a vector as an argument:


```r
numbers <- c(2.17, 5.6, 8.0, 9.99, 13.5)

floor(numbers)
#> [1]  2  5  8  9 13

ceiling(numbers)
#> [1]  3  6  8 10 14
```

## `round()`

`round()` lets you round up a number to however many decimal places you want. It takes two arguments: the value to be rounded, and the number of decimal places (called `digits` in the function).

For example:


```r
round(5.28495, digits = 2)
#> [1] 5.28

round(3.55 * -2.67, digits = 3) # -9.4785
#> [1] -9.478
```

`round()` can also take a vector as an argument:


```r
numbers <- c(6.2345, 24.545611, 5, 8.29, 0.00003)

round(numbers, digits = 3)
#> [1]  6.234 24.546  5.000  8.290  0.000
```

Notice that `round()` does "round up" after decimals greater than 5, for example:


```r
round(1.345, 2)
#> [1] 1.34
round(1.346, 2)
#> [1] 1.35
round(1.3458, 2)
#> [1] 1.35
```

`round()` can also be used to round to a power of ten, by giving a negative number for the second argument. This negative number $n$ represents the nearest $n$-th power of ten. For example, using -2 will round to the nearest hundred.

More examples:


```r
round(132, -2)
#> [1] 100
round(156, -2)
#> [1] 200
round(23, -2)
#> [1] 0
round(689, -3)
#> [1] 1000
```


## `abs()`

The absolute value is defined as the distance of a number from the origin of a number line.

With `abs()` you can calculate the absolute value of a number. For example:


```r
abs(23.1)
#> [1] 23.1
abs(-12)
#> [1] 12
```

`abs()` can also take a vector as an argument:


```r
numbers <- c(12, -4, 2.5, -3.77, -.05, NA)
abs(numbers)
#> [1] 12.00  4.00  2.50  3.77  0.05    NA
```

## Exercises

### Question 1

<!-- ```{r q1, echo=FALSE} -->
<!-- question( -->
<!--   "What will the following code return?\n```round(23.437, 2)```", -->
<!--   answer("23.44", correct = TRUE, message = "`round()` rounds up!"), -->
<!--   answer("23.40"), -->
<!--   answer("23.43"), -->
<!--   answer("23.45"), -->
<!--   random_answer_order = TRUE, -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

### Question 2

Round the following number to the nearest tenth:

<!-- ```{r q2, exercise=TRUE, exercise.lines = 2} -->
<!-- x <- 9.368983428 -->
<!-- ``` -->

<!-- ```{r q2-solution} -->
<!-- x <- 9.368983428 -->
<!-- round(x, 1) -->
<!-- ``` -->

### Question 3

Calculate the absolute value and round the decimals to 2 digits of the following vector `x`:

<!-- ```{r q3, exercise=TRUE, exercise.lines = 2} -->
<!-- x <- c(0.5431, -553.4534, 43.345, -907.89888, -0.0006, 8.1) -->
<!-- ``` -->

<!-- ```{r q3-solution} -->
<!-- x <- c(0.5431, -553.4534, 43.345, -907.89888, -0.0006, 8.1) -->
<!-- abs(round(x, 2)) -->
<!-- ``` -->

### Question 4

<!-- ```{r q4, echo=FALSE} -->
<!-- question( -->
<!--   "What will the following code return?\n ```round(2.68897) ```", -->
<!--   answer("`3`", correct = TRUE, message = "If you don't pass in a second argument to `round`, the default is `digits = 0` (remember it rounds up)."), -->
<!--   answer("`2`"), -->
<!--   answer("`2.69`"), -->
<!--   answer("`2.6`"), -->
<!--   random_answer_order = TRUE, -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

### Question 5

<!-- ```{r q5, echo=FALSE} -->
<!-- question( -->
<!--   "What will the following code return?\n ```round(ceiling(23.45395), 3) ```", -->
<!--   answer("24", correct = TRUE), -->
<!--   answer("23.453"), -->
<!--   answer("23.454"), -->
<!--   answer("23"), -->
<!--   random_answer_order = TRUE, -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

### Question 6

<!-- ```{r q6, echo=FALSE} -->
<!-- question( -->
<!--   "What will the following code return?\n```round(3537, -3)```", -->
<!--   answer("4000", correct = TRUE, message = "A value of `digits = -3` means that it will round to the closest thousand; 3537 is closest to 4000."), -->
<!--   answer("3000"), -->
<!--   answer("0"), -->
<!--   answer("300"), -->
<!--   random_answer_order = TRUE, -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

### Question 7

<!-- ```{r q7, echo=FALSE} -->
<!-- question( -->
<!--   "What will the following code return?\n```floor(FALSE) ```", -->
<!--   answer("0", correct = TRUE, message = "When doing arithmetic operations, FALSE is taken as 0."), -->
<!--   answer("1"), -->
<!--   answer("FALSE"), -->
<!--   answer("TRUE"), -->
<!--   answer("It will give an error"), -->
<!--   random_answer_order = TRUE, -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

### Question 8

<!-- ```{r q8, echo=FALSE} -->
<!-- question( -->
<!--   "Which of the following code snippets will give `0` as a result? (Select all that apply)", -->
<!--   type = "learnr_checkbox", -->
<!--   answer("`round(421.75, -3)`", correct = TRUE), -->
<!--   answer("`round(0.002, 2)`", correct = TRUE), -->
<!--   answer("`ceiling(abs(FALSE))`", correct = TRUE), -->
<!--   answer("`abs(-FALSE)`", correct = TRUE), -->
<!--   answer("`floor(TRUE)`"), -->
<!--   answer("`round(0.007, 2)`"), -->
<!--   answer("`ceiling(NA)`"), -->
<!--   answer("`abs('-3')`"), -->
<!--   random_answer_order = TRUE, -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

### Question 9

<!-- ```{r q9, echo=FALSE} -->
<!-- question( -->
<!--   "Which of the options would give the error '`Error: non-numeric argument to mathematical function`'?", -->
<!--   answer("`abs('3')`", correct = TRUE, message = "The '3' passed as input is actually text, since it is wrapped inside ' '."), -->
<!--   answer("`abs(NA)`"), -->
<!--   answer("`abs(+)`"), -->
<!--   answer("`abs(- + - 1)`"), -->
<!--   random_answer_order = TRUE, -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

### Question 10

<!-- ```{r q10, echo=FALSE} -->
<!-- question( -->
<!--   "TRUE or FALSE: Will the following commands give equal results?\n `round(2.500)`\n `round(2.503)`", -->
<!--   answer("FALSE", correct = TRUE, message = "In the second command it rounds up!"), -->
<!--   answer("TRUE"), -->
<!--   random_answer_order = TRUE, -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

## Common Errors

- `non-numeric argument to mathematical function`. Remember, all of the functions can only take numeric values, logical objects (TRUE and FALSE), or NA, so if you input something else you will get this error. Make sure that your input doesn't have some text hiding in there!

## References

- [`floor()`, `ceiling()`, and `round()`](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/Round)
- [`abs()`](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/MathFun)





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
