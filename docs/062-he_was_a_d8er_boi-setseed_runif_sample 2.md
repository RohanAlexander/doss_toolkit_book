


# setseed, runif, rnorm, and sample

*Written by Haoluan Chen and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- Generate numbers from a uniform distribution or normal distribution 
- Sample from a collection of numbers

Prerequisite skills include:

- Run code in R
- Basic knowledge of uniform distribution and normal distribution and sampling

Highlights:

- Generate random value from a uniform distribution and normal distribution
- Generate random value from a set
- `set.seed()` for reproducibility 


## The content


Simulation is an important topic in statistics because it helps you understand how random data might be generated. For some experiments, you may want to simulate values from probability distributions. In R, we can use `runif()` and `rnorm()` function to generate random number from uniform distribution or normal distributionr. Also, we can randomly sample from a set of numbers by using the `sample()` function. 

### runif()


The `runif()` function generate random numbers from a uniform distribution.  

#### Arguments

It takes in three parameters: `n`, `min` and `max`. The parameter `n` specifies the number of random values you want to generate. The parameter `min` and `max` specify the range of the uniform distribution. The default of min and max are 0 and 1.

Arguments | What does it mean
------------- | -------------
n (required) | number of random values you want to generate (numeric)
min (optional) | the minimum value of the uniform distribution you are sampling from (numeric)
max (optional)| the maximum value of the uniform distribution you are sampling from (numeric)


#### Example



```r
runif(n = 3)
#> [1] 0.9317394 0.3456249 0.7127989
```
The above code means to generate three random numbers from unif(0,1) where unif is a uniform distribution with a minimum value of 0 and maximum value of 1.

What if you want to generate number from `unif(2,8)` uniformly?

In `runif()` function, we can specify the min and max to be 2 and 8 to generate three numbers from unif(2,8):


```r
runif(n = 3, min = 2, max = 8)
#> [1] 2.506564 3.583140 5.068793
```

### rnorm()


In R, we can use `rnorm()` function to generate numbers from a normal distribution. 

#### Arguments

It takes in three parameters: `n`, `mean`, and `sd`. The parameter `n` specifies the number of random values you want to generate. The parameter `mean` and `sd` specifies the mean and standard deviation of the normal distribution you wish to sample. The default of `mean` and `sd` are 0 and 1.

Arguments | What does it mean
------------- | -------------
n (required) | number of random values you want to generate (numeric)
mean (optional) | the mean value of the normal distribution you are sampling from (numeric)
sd (optional)| the standard deviation of the normal distribution you are sampling from (numeric)

#### Example

Let's say we want to generate 5 random number from a normal distribution with `mean = 0` and `sd = 2`.


```r
rnorm(n = 5, sd = 2)
#> [1] -4.0530897 -0.4828468  0.8745783  0.1097077 -0.8059629
```

Here, we set the `n` to be 5 and `sd` to be 2, because we want to generate five random numbers from a normal distribution with a standard deviation of 2. We do not have to specify the mean value here because the default of the mean parameter is 0, which is exactly what we want. 

What if we want to generate 5 number from normal(10,2)?


```r
rnorm(n = 5, mean = 10, sd = 2)
#> [1]  8.144985  9.890151 10.006775  6.725741  9.411133
```
Here, we generated 5 numbers from normal(10,2) distribution.

### sample()

In R, we can using `sample()` to randomly sample numbers from a collection of numbers. 

#### Arguments

It takes in three parameters: x, size, and replace. The x is the vector of one or more elements that you wish to sample. The parameter size specifies the number of random values you want to generate. The parameter replace is a logical variable; true if you want to sample with replacement. 

When replace is set to true, you will be sampling from the same set of numbers for each generation. When replace is set to false, every time you sample a number, it will be taken out of the vector x for the next number generation. 

Arguments | What does it mean
------------- | -------------
x (required) | vector of one or more elements that you are sampling from
size (required) | number of random values you want to generate (numeric)
replace (optional)| true if you want to sample with replacement (logical)
prob (optional) | a vector of probability weights for obtaining the elements of the vector being sampled.

#### Examples




Here, we have a vector containing 6 numbers to simulate rolling dice. Let's roll the dice 6 times and see what we get:



```r
x <- c(1, 2, 3, 4, 5, 6)
set.seed(2)
sample(x = x, size = 6, replace = TRUE)
#> [1] 5 6 6 1 5 1
```

**Don't worry about set.seed(1), you will learn in this tutorial!**
What if we set the replace to `FALSE`? 



```r
set.seed(1)
sample(x = x, size = 6, replace = FALSE)
#> [1] 1 4 3 6 2 5
```

As we see that when `replace = TRUE`, we obtain repeated sample of 6 and 1. However, when `replace = FALSE`, there is no repeated sample in the output. 

When setting the replace to `FALSE`, the numbers are taken out for each round of sampling. Here, our first number is 5, which means that the second number will only be a sample from the set {2,3,4,5,6}. The 1 will be taken out of the vector for this sampling process. So, that is why we always get each number to appear once in the simulation.  

Using the prob argument, we can assign the probability of each elements the vector being sampled.
For example, for a unfair dice, The probability of getting a 6 is 40% and the probability of getting any other number are 12%. We may simulate this unfair dice using sample() function and setting the prob argument. 


```r
set.seed(2)
sample(x = x, size = 6, replace = TRUE, prob = c(0.12, 0.12, 0.12, 0.12, 0.12, 0.4))
#> [1] 6 5 4 6 1 1
```



### set.seed()




Let's run our dice simulation twice and see what happens (run the following code twice)


```r
x <- c(1, 2, 3, 4, 5, 6)
sample(x = x, size = 6, replace = TRUE)
#> [1] 6 1 5 5 1 3
```

We get different results every time we run the simulation, because we randomly sampled from 1-6 with replacement. What if you want to reuse the result from one simulation? Sometimes you do not want your result to change every time you run the function. This is what `set.seed()` does. 

When you use `set.seed()` function before your simulation, the simulation output will be the same every time. 

#### Arguments


The `set.seed()` function takes in a number, and it can be any number.

#### Example


Let's use `set.seed()` before we do the dice simulation

Please run the following code twice. 


```r
set.seed(2)
x <- c(1, 2, 3, 4, 5, 6)
sample(x = x, size = 6, replace = TRUE)
#> [1] 5 6 6 1 5 1
```

This also works for `runif()`, `rnorm()` and other simulation functions. Once you use `set.seed()` your simulation will always produce the same result. 

## Exercises


### Exercise 1


Please generate 10 random values from unif(-1,1) 



### Exercise 2

Please generate 10 random values from normal(0,5)



### Exercise 3


<!-- ```{r exercise3, echo = FALSE} -->
<!-- question("Which of the following code simulates rolling a fair dice 5 times?", -->
<!--           answer("sample(c(1, 2, 3, 4, 5, 6), 5, replace = TRUE)", correct = TRUE), -->
<!--           answer("sample(c(1, 2, 3, 4, 5, 6), 5, replace = FALSE)"), -->
<!--           answer("sample(c(1, 2, 3, 4, 5, 6), 5)"), -->
<!--           answer("runif(5, 1, 6)"), -->
<!--           allow_retry = TRUE) -->

<!-- ``` -->

<!-- ### Exercise 4 -->


<!-- Please generate 10 random values from normal(10,5) and calculate the mean. -->
<!-- ```{r exercise4, exercise=TRUE, exercise.lines = 2} -->

<!-- ``` -->

<!-- ### Exercise 5 -->


<!-- Please generate 1000 random values from normal(10,5) and calculate the mean.  -->
<!-- ```{r exercise5, exercise=TRUE, exercise.lines = 2} -->

<!-- ``` -->

<!-- ### Exercise 6 -->


<!-- Run your code from exercise 4 and 5 few times and compare the results, what did you notice? -->

<!-- ```{r exercise6} -->

<!-- ``` -->


<!-- ### Exercise 7 -->


<!-- ```{r exercise7, echo = FALSE} -->
<!-- question("How would you ensure that the simulations in Exercises 4 and 5 give the same result every time?", -->
<!--           answer("You do not have to do anything, the simulation result will always be the same"), -->
<!--           answer("Use set.seed() function before you run the simulation", correct = TRUE), -->
<!--           answer("Set the set.seed parameter to TRUE"), -->
<!--           answer("Use sample() function instead of rnorm"), -->
<!--           allow_retry = TRUE) -->

<!-- ``` -->


![Exercise 1 & 2](https://youtu.be/2HMfMnvSVkg)
![Exercise 4 & 5 & 6](https://youtu.be/HJtZfqgc6fY)


## Common Mistakes & Errors


- Make sure you have input parameter in the right order!

## Next Steps


Sometimes you need to do additional things to make your simulated more similar to your data. You can take a look on this book: R Programming for Data Science: https://bookdown.org/rdpeng/rprogdatascience/simulation.html. It has videos that explains simulation concepts and simulating a linear model. 

You can also generate binomial random variables using `rbinom()`, and Poisson random variables using `rpois()`, among others!



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
