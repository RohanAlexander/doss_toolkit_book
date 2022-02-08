



# Simulating datasets for regression

*Written by Mariam Walaa and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- Simulate data for regression 

Prerequisite skills include:

- Familiarity with `set.seed()`, `runif()`, `rnorm()`, `sample()` 

Highlights

- We can recover the linear regression model from simulated data

## Overview

In the previous section, we learned about how to simulate data. We can build
regression models from this simulated data. However, another thing we can do with these
functions is build simulated data _for_ regression models.

For example, suppose you were not given a data set but instead was told of the
distributions of some variables and given their coefficients for a linear regression
model. We can use this information to _create_ the simulated data.

## Idea

To simulate a data set, try writing it down on paper first, and then
think about which parts are random, then translate it to code! For example, if you think
some number $y$ is related *linearly* to $x$ with a slope of 0.3, with some random
measurement error, you could write it down on paper like this:

$$
y = 0.3\cdot x + error
$$

Translating it to code might look like:


```r
x <- 2 # set some value of x
measurement_error <- rnorm(1) # normally distributed measurement error

y <- 0.3*x + rnorm(1) # calculate value of y
```

## Example

Suppose we are given distributions of weights and heights for a population of 50 people, 
and a linear regression equation for this data, which is the slope and intercept. We can 
then use this information to simulate the data _from_ the slope and intercept. Lets start 
with loading the tidyverse.


```r
library(tidyverse)
```

We can simulate the data as follows.



<pre><code class='language-r'><code>set.seed(2)<br><br>data <- tibble(weight = rnorm(n = 50, mean = 125, sd = 5),<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;error = rnorm(n = 50, mean = 0, sd = 1),<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style='color:hotpink'>height = weight * 1.2 + error</span>)</code></code></pre>

Lets see what this relationship looks like with the regression line and data points plotted.


```r
data %>% 
  ggplot(aes(x = weight, y = height)) +
  geom_point() + 
  geom_smooth(method = "lm", se = FALSE, formula = 'y ~ x')
```

<img src="063-he_was_a_d8er_boi-simulating_datasets_for_regression_files/figure-html/simulating-data-5-1.png" width="672" />

We may use this data set to build a regression models using the `lm()` function as follows.


```r
lm(height ~ weight, data = data)
#> 
#> Call:
#> lm(formula = height ~ weight, data = data)
#> 
#> Coefficients:
#> (Intercept)       weight  
#>      0.9387       1.1915
```

As we expect, building this linear regression model successfully recovers the original
slope of 1.2.

## Exercises

There are many functions involved when it comes to trying to simulate a data set. These
exercises will help you better learn which functions to use for which parts of the
simulation.

### Exercise 1

When simulating a data set, you will likely need to work with various types of variables
-- continuous variables, discrete variables, numeric variables, and non-numeric variables.

When it comes to discrete variables (whether numeric, non-numeric, or a mix of both), you
will likely want to see a repetition of a finite set of values. There is a certain
function out of the handful of functions we learned about for simulating datasets that
will be helpful for this task.

For this exercise, youll try to simulate data points for a discrete variable representing
the number of times you might pick out a red ball from a jar full of blue, red, and yellow
balls. Suppose youll pick out a ball 10 times and put it back every time, and that each
ball has equal probability of being picked.

Fill in the blanks for the code below to create data that represents the above scenario.



<pre><code class='language-r'><code>sample(<span style='background-color:#ffff7f'> </span> = c("Red", "Blue", "Yellow"),<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style='background-color:#ffff7f'> &nbsp;&nbsp;&nbsp;</span> = 10,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style='background-color:#ffff7f'> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>= TRUE,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style='background-color:#ffff7f'> &nbsp;&nbsp;&nbsp;</span> = c(0.33, 0.33, 0.33))</code></code></pre>

You'll notice that there are 4 blanks in total that you'll need to fill.

<!-- ```{r simulate-fill-in-sample-2, echo = FALSE} -->
<!-- quiz(question("What should the first blank be?", -->
<!--               answer("n"), -->
<!--               answer("x", correct = TRUE), -->
<!--               answer("c"), -->
<!--               answer("size"), -->
<!--               answer("replace"), -->
<!--               answer("prob"), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("What should the second blank be?", -->
<!--               answer("n"), -->
<!--               answer("x"), -->
<!--               answer("c"), -->
<!--               answer("size", correct = TRUE), -->
<!--               answer("replace"), -->
<!--               answer("prob"), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("What should the third blank be?", -->
<!--               answer("n"), -->
<!--               answer("x"), -->
<!--               answer("c"), -->
<!--               answer("size"), -->
<!--               answer("replace", correct = TRUE), -->
<!--               answer("prob"), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("What should the fourth blank be?", -->
<!--               answer("n"), -->
<!--               answer("x"), -->
<!--               answer("c"), -->
<!--               answer("size"), -->
<!--               answer("replace"), -->
<!--               answer("prob", correct = TRUE), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE)) -->
<!-- ``` -->

### Exercise 2

Suppose we are given a regression model with a slope of 1.2, and we want to simulate a 
dataset from the regression model similar to the previous scenario. We have the below code
to generate the data. What is wrong with this data-generating code below?

<!-- ```{r simulate-data-exercise-2, exercise = TRUE, exercise.eval = TRUE} -->
<!-- set.seed(2) -->
<!-- data <- tibble(weight = rnorm(n = 50, mean = 125, sd = 5), -->
<!--                height = rnorm(n = 50, mean = 150, sd = 4)) -->
<!-- ``` -->

<!-- ```{r simulate-data-exercise-2-hint-1} -->
<!-- # It works in the sense that we get meaningful output, but it is not the output we want for this problem -->
<!-- ``` -->
<!-- ```{r simulate-data-exercise-2-hint-2} -->
<!-- # If you are stuck, try looking at the code we used for this above, and determine what's different -->
<!-- ``` -->

<!-- ```{r simulate-data-exercise-2-solution, exercise = FALSE} -->
<!-- set.seed(2) -->
<!-- data <- tibble(weight = rnorm(n = 50, mean = 125, sd = 5), -->
<!--                error = rnorm(n = 50, mean = 0, sd = 1), -->
<!--                height = weight * 1.2 + error) -->
<!-- ``` -->

## Common Mistakes & Errors

Here are some common mistakes and errors you may come across:

- You may be confusing some of the arguments for different distribution functions. Make
sure you are using `runif()` to sample points from the _uniform_ distribution and `rnorm()`
to sample points from the _normal_ distribution.
- You may be misusing some of the arguments for a function like `sample()`. Make sure you
read the argument descriptions as well as the given examples in the documentation.
- You may forget to set the seed before running a chunk of code, or you may be using a
different value for a seed to obtain results you previously got with your code.

## Next Steps

If you would like to learn more about these functions, read the documentation associated
with each of the functions. But if you would like to learn more about simulating datasets
from a regression model, please take a look at the following:

- [Telling Stories With Data -- Its Just a Linear Model](https://www.tellingstorieswithdata.com/its-just-a-linear-model.html#overview)




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
