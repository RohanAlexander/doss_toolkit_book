




# function

*Written by Haoluan Chen.*



## Introduction

In this lesson, you will learn how to:

- Write your own functions in R


Prerequisite skills include:

- setup RStudio
- run R code in the console

Highlights:

- Write your own function


## The content


Function in R is a set of statements organized together to perform a specific task. 

The function consists of four parts: 

- Function Name: This is the name of the function. It is stored in the R environment as an object.

- Arguments/Parameters: Just like in math, a function has an input and an output. Arguments/Parameters are the inputs of the function. However, parameters can be required or have default values. Parameters are specified inside a () and split by comma. 

- Function Body: The function body contains a set of statements that defines what the function does. The function body is inside a {}.

- Return Value: The return value of a function is the last expression in the function body to be evaluated. This is the output of the function.

### Why and when should you use it?

Instead of copy and pasting your code multiple times, functions allow you to perform repetitive tasks automatically. It has three advantages over using copy and paste:

- You can give a function an informative name that makes your code easier to understand.

- As requirements change, you only need to update code in one place instead of many.

- You eliminate the chance of making incidental mistakes 

You should consider writing a function whenever you have copied and pasted a block of code more than twice.


### Built-in functions 

There are many built-in functions in R. For example, the `mean()` function in R can calculate the mean of a vector. Whenever we want to calculate a mean of some numbers, we do not have to calculate the sum of all the numbers and divide by the number of numbers. Instead, we can store the numbers in a vector then call the `mean()` function to calculate the mean. Utilize the built-in functions can make your life easier for your projects. 


### User defined functions

We can also write our own function for some specific task.

Here is a very simple function call the sum_of_two_numbers. 


```r
sum_of_two_numbers <- function(a, b){
  y = a + b
  y
}
```


In this function, it consists of four parts: 

- sum_of_two_numbers is the name of the function 
- a and b is the input of this function 
- y = a + b and y inside the {} is the body of the function
- y is the output of this function because it is the last expression in the function body to be evaluated.

We can use this function by calling the function name and specifying the input value in the bracket. We can use the following code to calculate the sum of 2 and 3. 


```r
sum_of_two_numbers(2,3)
#> [1] 5
```

### default parameters
The parameters can have a default value. 
For example, we can set the parameter b to 3 in our sum_of_two_numbers function. 


```r
sum_of_two_numbers <- function(a, b = 3){
  y = a + b
  y
}
```

Now, if we do not specify parameter b in our function call, then b is set to 3 in default. 


```r
sum_of_two_numbers(2)
#> [1] 5
```

Here, we tell R to run the body of sum_of_two_numbers with a = 2, and b is set to the default number 3. 

However, we can still specify parameter b in our function call to calculate the sum of two numbers.


```r
sum_of_two_numbers(2, 5)
#> [1] 7
```

Here, we tell R to run the body of sum_of_two_numbers with a = 2 and b = 5. 

## Exercises

#### Exercise 1

Change the name of the sum_of_two_numbers to mean_of_two_number and modify the function body to calculate the mean of two numbers.


```r
sum_of_two_numbers <- function(a, b){
  y = a + b
  y
}
```



```r
mean_of_two_numbers <- function(a, b){
  y = (a + b)/2
  y
}
```

#### Exercise 2
Write a function called product that takes two numbers as input and calculate the product of two numbers.





```r
product <- function(a, b){
  y = a * b
  y
}
```

#### Exercise 3
Here is the mean_of_two_numbers function in Exercise 1. Set the parameter a to a default value of 6. 


```r
mean_of_two_numbers <- function(a, b){
  y = (a + b)/2
  y
}
```



```r
mean_of_two_numbers <- function(a = 6, b){
  y = (a + b)/2
  y
}
```

#### Exercise 4
Predict the output of the following code.


```r
mean_of_two_numbers <- function(a = 6, b){
  y = (a + b)/2
  y
}
mean_of_two_numbers(3, 5)
#> [1] 4
```



```r
4
#> [1] 4
```




## Common mistakes & errors

- Make sure you have correct input for your function
- Remember that the function returns the last expression in the function body.
- Make sure you define your argument in () and your function body in {}.
- Make sure you define your function before calling it. 



## Next steps
Most of the time, you will be using the function from various packages and the functions in R. However, for some specific tasks, you will have to write your own functions. The ability to use user-defined functions and functions from different packages makes R a powerful tool in Data Science.   

If you want to see more completed function, you can read through this Function chapter in R for Data Science
https://r4ds.had.co.nz/functions.html#when-should-you-write-a-function


