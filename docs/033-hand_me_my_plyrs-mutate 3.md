


# mutate

*Written by Haoluan Chen and last updated on 7 October 2021.*

## Introduction

![Image Source:https://github.com/allisonhorst/stats-illustrations/blob/master/rstats-artwork/dplyr_mutate.png, Allison Horst](https://github.com/allisonhorst/stats-illustrations/blob/master/rstats-artwork/dplyr_mutate.png?raw=true){width=400 height=300}

`mutate()` is a function in the dplyr library. It is used to create new variables in your dataset while keeping the existing variables. 

## Examples 

I generated a dataset contains student test scores and their student id for a course. 


```r
scores <- tibble(student_ID = c("1", "2", "3", "4", "5", "6"),
               test_one_score = c(87, 76, 61, 80, 72, 69),
               test_two_score = c(79, 85, 52, 72, 65, 75),
               test_three_score = c(92,79, 45, 85, 76, 73))

scores
#> # A tibble: 6 × 4
#>   student_ID test_one_score test_two_score test_three_score
#>   <chr>               <dbl>          <dbl>            <dbl>
#> 1 1                      87             79               92
#> 2 2                      76             85               79
#> 3 3                      61             52               45
#> 4 4                      80             72               85
#> 5 5                      72             65               76
#> 6 6                      69             75               73
```

Q1: What is the average test score for each student? 

we can use mutate to calculate the average test score for each student and store it as a new variable called avg_test_score,


```r
avg <- scores %>% mutate(avg_test_score = (test_one_score + test_two_score + test_three_score)/3)
avg
#> # A tibble: 6 × 5
#>   student_ID test_one_score test_two_score test_three_score
#>   <chr>               <dbl>          <dbl>            <dbl>
#> 1 1                      87             79               92
#> 2 2                      76             85               79
#> 3 3                      61             52               45
#> 4 4                      80             72               85
#> 5 5                      72             65               76
#> 6 6                      69             75               73
#> # … with 1 more variable: avg_test_score <dbl>
```

Here, we have a expression for the new variable: 

avg_test_score = (test_one_score + test_two_score + test_three_score)/3 

The left side of the expression specifies the name of the new variable and the right side of the expression specifies how to calculate the new variable.  

Now, Lets assume the following weights for this course:

* 10% for test one
* 30% for test two 
* 60% for test three

Q2: What is the final grade for each student?


```r
final <- scores %>% mutate(final_grade = 0.1*test_one_score + 0.3*test_two_score + 0.6*test_three_score)
final
#> # A tibble: 6 × 5
#>   student_ID test_one_score test_two_score test_three_score
#>   <chr>               <dbl>          <dbl>            <dbl>
#> 1 1                      87             79               92
#> 2 2                      76             85               79
#> 3 3                      61             52               45
#> 4 4                      80             72               85
#> 5 5                      72             65               76
#> 6 6                      69             75               73
#> # … with 1 more variable: final_grade <dbl>
```

Here, we calculate the final grade by summing the value of each test score times its weight. Then, we store the final grade it as final_grade. 

Q3: Who received the highest final grade in this course?

**Note: rank() produces a vector that contains the rank of the values in the vector that was evaluated such that the lowest value would have a rank of 1 and the second-lowest value would have a rank of 2.**

**desc() transform a vector into a format that will be sorted in descending order. **


```r
final %>% mutate(rank = rank(desc(final_grade)))
#> # A tibble: 6 × 6
#>   student_ID test_one_score test_two_score test_three_score
#>   <chr>               <dbl>          <dbl>            <dbl>
#> 1 1                      87             79               92
#> 2 2                      76             85               79
#> 3 3                      61             52               45
#> 4 4                      80             72               85
#> 5 5                      72             65               76
#> 6 6                      69             75               73
#> # … with 2 more variables: final_grade <dbl>, rank <dbl>
```

Here, we created a new variable called rank and specify its value using `rank()` and `desc()`. The `rank()` function produces the rank of the student final grade, but it assigns rank from lowest to largest(lowest final grade will assign to 1). So, we have to use `desc()` to get the rank from largest to lowest(largest final grade will assign to 1)

Therefore, student 1 received the highest final grade in this course. 

Q4: Did all student pass the class?


```r
final %>% mutate(pass = ifelse(final_grade>=50, TRUE, FALSE))
#> # A tibble: 6 × 6
#>   student_ID test_one_score test_two_score test_three_score
#>   <chr>               <dbl>          <dbl>            <dbl>
#> 1 1                      87             79               92
#> 2 2                      76             85               79
#> 3 3                      61             52               45
#> 4 4                      80             72               85
#> 5 5                      72             65               76
#> 6 6                      69             75               73
#> # … with 2 more variables: final_grade <dbl>, pass <lgl>
```

Here, we created a new variable called pass, which is a logical variable that is TRUE when student received final grade higher or equal to 50(FALSE otherwise). 

We used another function `ifelse()`, it is equivalent to if...else statement in R. It takes in 3 parameters(test_expression, x, y). If the test_expression is true, it will return x, if the test_expression is not true, it will return y. 

In this case, When the final_grade is greater or equal to 50, the pass variable will assign to TRUE. And when the final_grade is less than 50, the pass variable will assign to FALSE.

Unfortunately, student 3 failed the course :(

**Note: this question can also be done using case_when function. **


## Concept Maps 


![Source: https://github.com/rstudio/concept-maps, Monica Alonso and Greg Wilson](https://github.com/rstudio/concept-maps/blob/master/en/mutate.svg?raw=true)

## Common mistakes 

* Make sure you download dplyr and called library(dplyr) before using mutate()
* Incorrect spelling of the name of the dataset or variables
* the name of new variable should not contain space or other special symbols such as / or " 
* Make sure your expression is mathematically correct and avoid division by 0



## Exercise

### Question 1 

Now, due to the COVID-19 the weight of this course has been changed. Consider the following weight:

* 20% for test one
* 50% for test two 
* 30% for test three

Please use the dataset(scores) to calculate the final score for each of the students and store it as new_final_score.


```r
scores <- tibble(student_ID = c("1", "2", "3", "4", "5", "6"),
               test_one_score = c(87, 76, 61, 80, 72, 69),
               test_two_score = c(79, 85, 52, 72, 65, 75),
               test_three_score = c(92,79, 45, 85, 76, 73))

```


<!-- ```{r mutateex1, exercise=TRUE, exercise.lines = 10} -->
<!-- scores -->


<!-- ``` -->

### Question 2

Did everyone pass the course under this new marking scheme in Q1?
Please create a new logical variable called pass to identify if any student did not pass the course.
*Note: You may want to copy your code in Question 1 here *

<!-- ```{r mutateex2, exercise=TRUE, exercise.lines = 5} -->

<!-- ``` -->

### Question 3 

Please create a new variable called rank that assigns student with highest new_final_score as 1, second highest new_final_score as 2 and so on. 
*Note: You may want to copy your code in Question 1 here *

<!-- ```{r mutateex3, exercise=TRUE, exercise.lines = 5} -->

<!-- ``` -->


### Video Solution

![Question 1](https://youtu.be/fZck9kRLw9s)
![Question 2](https://youtu.be/Xm8qB5W4PUw)
![Question 3](https://youtu.be/QNUafgFtRvQ)


## Next steps

Now you may use other functions in dplyr to generate variables in your dataset. For example




```r
final %>% select(student_ID, final_grade) %>% 
  filter(final_grade>80) %>% 
  mutate(letter_grade = "A",
         reward = TRUE)
#> # A tibble: 3 × 4
#>   student_ID final_grade letter_grade reward
#>   <chr>            <dbl> <chr>        <lgl> 
#> 1 1                 87.6 A            TRUE  
#> 2 2                 80.5 A            TRUE  
#> 3 4                 80.6 A            TRUE
```
*As you can see you can create multiple variables within one function call by separate them using comma *

### Other resources

R for Data Science: https://r4ds.had.co.nz/transform.html (Chapter 5.5 covers mutate() and 5.5.1 contains useful creation function)

Documentation for mutate() https://dplyr.tidyverse.org/reference/mutate.html

Vignettes(demonstration of how to use functions in dplyr including mutate()) for dplyr: https://cran.r-project.org/web/packages/dplyr/vignettes/dplyr.html













## Exercises

### Question 1
`mutate()` is a function in the dplyr library.
    a.  True
    b. False
    
### Question 2
`mutate()` create new variables in your dataset while keeping the existing variables. 
    a.  True
    b. False
    
### Question 3
`mutate()` can only create numeric variable. 
    a. True
    b.  False

### Question 4
`mutate()` is a built-in function
    a. True
    b.  False

### Question 5
Name of the new variable can contain space or other special symbols such as / or " 
    a. True
    b.  False

### Question 6
Which of the following code creates a new variable called `test_score` with value 100?
    a.  mutate(data, test_score = 100)
    b. mutate(test_score = 100)
    c. mutate(test_score = 100, data)
    d. mutate(test_score)
    
### Question 7
`mutate()` can create new string variable 
    a.  True
    b. False
    
### Question 8
Do you need to install and load dplyr package to use `mutate()`
    a.  Yes
    b. No
    
### Question 9
Other functions can be used in `mutate()` to create new variable
    a.  True
    b. False
    
### Question 10
`mutate()` can remove the existing variables.
    a. True
    b.  False

