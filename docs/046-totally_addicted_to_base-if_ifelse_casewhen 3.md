


# if, if else and case when

*Written by Haoluan Chen and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- use the `if()` function. 
- use the `if_else()` function.
- use the `case_when()` function.

Prerequisite skills include:

- Setup RStudio.
- Run R code in the console.
- Install and load `dplyr` package.

Highlights:

- Learn how to use if_else statement
- Using `case_when()` to create new variables in your dataset

## `if()`

The `if()` function is a tool for returning an output based on a logical condition. The syntax of the `if()` function is:


```if
if (condition) {
  statement
}
```

If the condition is true, the {statement} will be executed. However, if the condition is false, then nothing will happen. 

## Example


```if2
x <- 5 
if (x > 0){
  print("A positive number")
}
```

Since x is set to 5, so our condition x > 0 is evaluated to true. Therefore, the statement *print("A positive number")* is executed.  


```if3
x <- -3 
if (x > 0){
  print("A positive number")
}
```

However, if x is set to -3, our condition x > 0 is evaluated as false. Therefore, the statement *print("A positive number")* will not be executed, and nothing happens.  

## `if_else()`

The `if_else()` function has two parts. The first part is exactly the same as the if statement, and the second part is the else statement. The else statement will be evaluated if the condition is FALSE. 

The syntax of the `if_else()` function is:


```ifelse
if (condition) {
  statement1 
} else {
  statement2
}
```

If the condition is true, the {statement1} will be executed. However, if the condition is false, then {statement2} will be executed.

### Examples 


```ifelse1
if (x > 0){
  print("A positive number")
} else {
  print("A negative number")
}
```

The above if_else statement will return "A positive number" if x is greater than 0 and "A negative number" if x is less than 0.

## `case_when()` function 
What if you have multiple condition? `case_when()` function is here to help. 

The syntax of `case_when()` function with a single case is a follows:

```case
case_when(condition ~ output_value)
```

If the condition is evaluated to true, then the `case_when()` function will return the output_value. With only a single case, this is exactly the same as an if statement. 


The syntax of `case_when()` function with two cases is a follows:

```case1
case_when(condition ~ output_value_true, 
          TRUE ~ output_value_false)
```

If the condition is evaluates to true, then the `case_when()` function will return the output_value_true. However, if the condition is false, then the function will return the output_value_false.

The syntax of `case_when()` function with multiple cases is a follows:

```case2
case_when(condition_1 ~ output_1, 
          condition_2 ~ output_2,
          condition_3 ~ output_3, 
          ...)
```

Here, when condition_1 is evaluated to true, then the function returns output_1. When condition_2 is evaluated to true, then the function returns output_2 and so on. 


### Examples 
Here is an example of using `case_when()` function with multiple cases. 

We have seven students and their numeric grades for a course, and we want to assign the letter grade for each student. A grade between 80 and 100 is A grade, 70 to 79 is B grade, 60 to 69 is C grade, 50 to 59 is D grade, and below 50 is F grade.  



```r
test_score_df <- tribble(~student_id, ~grade
                  ,'1',  94
                  ,'2',  90
                  ,'3',  88
                  ,'4',  75
                  ,'5',  66
                  ,'6',  65
                  ,'7',  45 
                  )
test_score_df
#> # A tibble: 7 × 2
#>   student_id grade
#>   <chr>      <dbl>
#> 1 1             94
#> 2 2             90
#> 3 3             88
#> 4 4             75
#> 5 5             66
#> 6 6             65
#> 7 7             45
```

To assign the letter grade, we can use mutate and case_when() to create a new variable in our table. 


```r
mutate(test_score_df, letter_grade = 
                           case_when(grade <= 100 & grade >= 80 ~ 'A', 
                                     grade < 80 & grade >= 70 ~ 'B', 
                                     grade < 70 & grade >= 60 ~ 'C', 
                                     grade < 60 & grade >+ 50 ~ 'D',
                                     grade < 50 ~ 'F')) 
#> # A tibble: 7 × 3
#>   student_id grade letter_grade
#>   <chr>      <dbl> <chr>       
#> 1 1             94 A           
#> 2 2             90 A           
#> 3 3             88 A           
#> 4 4             75 B           
#> 5 5             66 C           
#> 6 6             65 C           
#> 7 7             45 F
```



## Exercises

### Exercises 1 
Using if_else statement to see if x can be divided by 3 with remainder equal to zero.  
**Hint: %% is an operation to calculate the remainder **


```r
x <- 123456
```


```r
x <- 123456
if (x %% 3 == 0){
  print(TRUE)
} else{
  print(FALSE)
}
#> [1] TRUE
```

### Exercises 2


<!-- ```{r ifelseex2, echo = FALSE} -->
<!-- question("Predict what is the output of this if_else statement", -->
<!--           answer("0"), -->
<!--           answer("1", correct = TRUE), -->
<!--           answer("5.5"), -->
<!--           answer("5"), -->
<!--           allow_retry = TRUE) -->

<!-- ```  -->

<!-- ```{r eval = FALSE} -->
<!-- x <- c(1,2,3,4,5,6,7,8,9,10) -->
<!-- if (mean(x) > 5){ -->
<!--   print(1) -->
<!-- }else{ -->
<!--   print(0) -->
<!-- } -->
<!-- ``` -->

### Exercises 3


```r
test <- tribble(~student_id, ~pass
                  ,'1',  TRUE
                  ,'2',  TRUE
                  ,'3',  FALSE
                  ,'4',  TRUE
                  ,'5',  TRUE
                  ,'6',  TRUE
                  ,'7',  FALSE 
                  )
test
#> # A tibble: 7 × 2
#>   student_id pass 
#>   <chr>      <lgl>
#> 1 1          TRUE 
#> 2 2          TRUE 
#> 3 3          FALSE
#> 4 4          TRUE 
#> 5 5          TRUE 
#> 6 6          TRUE 
#> 7 7          FALSE
```

Here is a table called test. Replace the TRUE values in pass variable to 1 and FALSE values to 0 by using `case_when()`

<!-- ```{r casewhen, exercise=TRUE, exercise.lines = 5} -->

<!-- ``` -->

<!-- ```{r casewhen-solution} -->
<!-- test %>% mutate(pass = case_when(pass == TRUE ~ 1, TRUE ~ 0)) -->
<!-- ``` -->



## Common mistakes & errors

- Make sure you put the condition inside the ()
- Make sure you put the statements in the {}
- If you receive an unexpected output, you may test your if_else logic by testing some cases
- Make sure you have the correct syntax for the case_when() function

## Next steps

You can write a nested if_else for more complex situations. An example can be found on this website https://www.tutorialgateway.org/nested-if-else-in-r/

You can also combine for and while loop with if_else for other complex situations! For example 


```r

for (i in 1:6){
  if (i == 5){
    print(TRUE)
  }
  else{
    print(FALSE)
  }
}
#> [1] FALSE
#> [1] FALSE
#> [1] FALSE
#> [1] FALSE
#> [1] TRUE
#> [1] FALSE
```

## Exercises

### Question 1
`if()` function is a tool for returning an output based on a logical condition.
    a.  True
    b. False

### Question 2
When will the statement execute in `if(condition){statement}`
    a. Condition evaluate to False
    b.  Condition evaluate to True
    c. statement will execute in any condition
    d. Condition evaluate to NULL
    
### Question 3
`else()` should always be used with `if()`
    a. True
    b.  False
    
### Question 4
The `if_else()` function has two parts. The first part is exactly the same as the if statement, and the second part is the else statement. The else statement will be evaluated if the condition is FALSE. 
    a.  True
    b. False
### Question 5
`~` is used to connect the condition and the output when condition evaluated to TRUE in `case_when()`.
    a.  True
    b. False
    
### Question 6
x <- c(1,2,3,4,5,6,7,8,9,10)
if (mean(x) > 5){
  print(1)
}else{
  print(0)
}
Predict what is the output of this if_else statement?
    a. 0
    b.  1
    c. 5.5
    d. 5
    
### Question 7
x <- c(5, 4, 3, 2, 1)
if (mean(x) > 5){
  print(1)
}else{
  print(0)
}
Predict what is the output of this if_else statement?
    a.  0
    b. 1
    c. 5.5
    d. 5
    
### Question 8
case_when(mean(x) > 5 ~ 1, 
          mean(x) >= 5 ~ 0)
Using this `case_when()` is same as `if_else` in Question 6 and 7 
    a.  True
    b. False
    
### Question 9
`case_when()` can be used when you have multiple condition
    a.  True
    b. False 
    
### Question 10
`case_when()` can be used when you have single condition
    a.  True
    b. False
