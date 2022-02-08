


# Joins

*Written by Haoluan Chen and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- Join two tables by using `left_join()`, `right_join()`, `full_join()`, `inner_join` and `anti_join()`

Prerequisite skills include:

- Install and load dplyr package

Highlights:

- Learn how two join two tables  

Sometimes you may want to combine two data frames into a single table. Here we have one table which contains data such as the student id and their grade. And we have another table that includes demographic information about the student.


```r
test_score <- tribble(~student_id, ~grade
                  ,'1',  94
                  ,'2',  90
                  ,'3',  88
                  ,'4',  75
                  ,'5',  66
                  )
student_info <- tribble(~student_id, ~age,~gender
                  ,'1', 18, 'F'
                  ,'2', 20, 'F'
                  ,'4', 25, 'M'
                  ,'6', 21, 'M'
                  ,'7', 23, 'F'
                  )
test_score
#> # A tibble: 5 × 2
#>   student_id grade
#>   <chr>      <dbl>
#> 1 1             94
#> 2 2             90
#> 3 3             88
#> 4 4             75
#> 5 5             66
student_info
#> # A tibble: 5 × 3
#>   student_id   age gender
#>   <chr>      <dbl> <chr> 
#> 1 1             18 F     
#> 2 2             20 F     
#> 3 4             25 M     
#> 4 6             21 M     
#> 5 7             23 F
```

Using `dplyr` within R, we can easily import our data and join these tables, using the following join types.

- Left Join (`left_join()`)
- Right Join (`right_join()`)
- Full Join (`full_join()`)
- Inner Join (`inner_join()`)
- Anti Join (`anti_join()`)

The general syntax of these joins is as follows:

join_type(firstTable, secondTable, by=columnTojoinOn)

We'll now run through an example of using each of these join types on our two tables.


## `left_join()`

`left_join()` will take all of the values from the table we specify as left (e.g., the first one) and match them to records from the table on the right (e.g., the second one) by the variable we specified. If there is no match in the second table, it will show NULL for the values in the second table. For example, if we left joined 'test_score' to 'student_info', our data would look as follows:


```r
leftJoinDf <- 
  left_join(test_score,student_info, by='student_id')

leftJoinDf
#> # A tibble: 5 × 4
#>   student_id grade   age gender
#>   <chr>      <dbl> <dbl> <chr> 
#> 1 1             94    18 F     
#> 2 2             90    20 F     
#> 3 3             88    NA <NA>  
#> 4 4             75    25 M     
#> 5 5             66    NA <NA>
```


## `right_join()`

One of the easiest ways to consider a right join is the opposite of a left join! In this instance, the table specified second within the join statement will be the one that the new table takes all of its values from. If there is no match in the first table (the table specified first in the argument), it will return NULL for the values in the first table that did not find a match. In this instance, if we right joined student_info to test_score, our data would look as follows:


```r
rightJoinDf <- right_join(test_score,student_info,by='student_id')
rightJoinDf
#> # A tibble: 5 × 4
#>   student_id grade   age gender
#>   <chr>      <dbl> <dbl> <chr> 
#> 1 1             94    18 F     
#> 2 2             90    20 F     
#> 3 4             75    25 M     
#> 4 6             NA    21 M     
#> 5 7             NA    23 F
```

## `full_join()`

The full join returns all of the data in a new table, whether it matches on either the left or right tables. If the specified variable match on two tables, then a join will be executed. Otherwise, it will return NULL in places where a matching row does not exist.


```r
FullJoinDf <- full_join(test_score,student_info,by='student_id')
FullJoinDf
#> # A tibble: 7 × 4
#>   student_id grade   age gender
#>   <chr>      <dbl> <dbl> <chr> 
#> 1 1             94    18 F     
#> 2 2             90    20 F     
#> 3 3             88    NA <NA>  
#> 4 4             75    25 M     
#> 5 5             66    NA <NA>  
#> 6 6             NA    21 M     
#> 7 7             NA    23 F
```

## `inner_join()`

inner_join creates a new table that only contains matched rows in both tables. 
For example, if we decided to join by student_id, the new table would contain rows 1 and 2:


```r
InnerJoinDf <- inner_join(test_score,student_info,by='student_id')
InnerJoinDf
#> # A tibble: 3 × 4
#>   student_id grade   age gender
#>   <chr>      <dbl> <dbl> <chr> 
#> 1 1             94    18 F     
#> 2 2             90    20 F     
#> 3 4             75    25 M
```

## `anti_join()`

An anti join will return all of the rows from the first table where there are no matching values from the second.

An example of this is shown below:


```r
AntiJoinDf <- anti_join(test_score,student_info,by='student_id')
AntiJoinDf
#> # A tibble: 2 × 2
#>   student_id grade
#>   <chr>      <dbl>
#> 1 3             88
#> 2 5             66
```





## Exercises


```r
test_score <- tribble(~student_id, ~grade
                  ,'1',  94
                  ,'2',  90
                  ,'3',  88
                  ,'4',  75
                  ,'5',  66
                  )
student_info <- tribble(~student_id, ~age,~gender
                  ,'1', 18, 'F'
                  ,'3', 20, 'F'
                  ,'5', 25, 'M'
                  ,'7', 21, 'M'
                  ,'9', 23, 'F'
                  )
test_score
#> # A tibble: 5 × 2
#>   student_id grade
#>   <chr>      <dbl>
#> 1 1             94
#> 2 2             90
#> 3 3             88
#> 4 4             75
#> 5 5             66
student_info
#> # A tibble: 5 × 3
#>   student_id   age gender
#>   <chr>      <dbl> <chr> 
#> 1 1             18 F     
#> 2 3             20 F     
#> 3 5             25 M     
#> 4 7             21 M     
#> 5 9             23 F
```

### Exercises 1

<!-- ```{r joinex2, echo = FALSE} -->
<!-- question("Which set of student id is in the output of left_join(test_score, student_info)", -->
<!--           answer("1, 2, 3, 4, 5", correct = TRUE), -->
<!--           answer("1, 3, 5"), -->
<!--           answer("7, 9"), -->
<!--           answer("1, 2, 3, 4, 5, 7, 9"), -->
<!--           allow_retry = TRUE) -->

<!-- ```  -->

<!-- ### Exercises 2 -->

<!-- ```{r joinex3, echo = FALSE} -->
<!-- question("Which set of student id is in the output of right_join(test_score, student_info)", -->
<!--           answer("1, 3, 5"), -->
<!--           answer("7, 9"), -->
<!--           answer("1, 3, 5, 7, 9", correct = TRUE), -->
<!--           answer("1, 2, 3, 4, 5, 7, 9"), -->
<!--           allow_retry = TRUE) -->

<!-- ```  -->

<!-- ### Exercises 3 -->

<!-- ```{r joinex4, echo = FALSE} -->
<!-- question("Which set of student id is in the output of inner_join(test_score, student_info)", -->
<!--           answer("1, 3, 5", correct = TRUE), -->
<!--           answer("7, 9"), -->
<!--           answer("1, 3, 5, 7, 9"), -->
<!--           answer("1, 2, 3, 4, 5, 7, 9"), -->
<!--           allow_retry = TRUE) -->

<!-- ```  -->


<!-- ### Exercises 4 -->

<!-- ```{r joinex5, echo = FALSE} -->
<!-- question("Which set of student id is in the output of full_join(test_score, student_info)", -->
<!--           answer("1, 3, 5"), -->
<!--           answer("7, 9"), -->
<!--           answer("1, 3, 5, 7, 9"), -->
<!--           answer("1, 2, 3, 4, 5, 7, 9", correct = TRUE), -->
<!--           allow_retry = TRUE) -->

<!-- ```  -->


## Common Mistakes & Errors

- Make sure there is at least one common variable in the tables you are joining.
- Think about how you want to join the table and use the appropriate join function.

## Next Steps

You can read through R for Data Science Chapter 13 Relational(working with multiple tables) data (https://r4ds.had.co.nz/relational-data.html) for a more detailed explanation and visualization. 

Here is the documentation for all the joins function in dplyr package: https://dplyr.tidyverse.org/reference/join.html



## Exercises

### Question 1
What function can we use to combine two data frames into a single table
    a. `left_join()`
    b. `right_join()`
    c. `full_join()`
    d.   All of the above
    

### Question 2
`left_join()` will take all of the values from the first table and match them to records from the second by the variable we specified.
    a.  True
    b. False
  
### Question 3
If there is no match in the second table, it will show False for the values in the second table.
    a. True
    b.  False
 
### Question 4
`left_join(a, b)` is similar  to `right_join(b, a)`
    a.  True
    b. False

### Question 5
`full_join()` creates a new table that only contains matched rows in both tables. 
    a. True
    b.  False 
### Question 6
`inner_join()` returns all of the data in a new table, whether it matches on either the left or right tables.
    a.  True
    b. False 
### Question 7
`anti_join()` will return all of the rows from the first table where there are no matching values from the second.
    a.  True
    b. False 
    
### Question 8
test_score <- tribble(~student_id, ~grade
                  ,'1',  94
                  ,'2',  90
                  ,'3',  88
                  ,'4',  75
                  ,'5',  66
                  )
student_info <- tribble(~student_id, ~age,~gender
                  ,'1', 18, 'F'
                  ,'3', 20, 'F'
                  ,'5', 25, 'M'
                  ,'7', 21, 'M'
                  ,'9', 23, 'F'
                  )

Which set of student id is in the output of `left_join(test_score, student_info)`
    a.  1, 2, 3, 4, 5
    b. 1, 3, 5
    c. 7, 9
    d. 1, 2, 3, 4, 5, 7, 9

### Question 9
Using the code in question 8
Which set of student id is in the output of `inner_join(test_score, student_info)`
    a.  1, 3, 5
    b. 7, 9
    c. 1, 3, 5, 7, 9
    d. 1, 2, 3, 4, 5, 7, 9
    

### Question 10
Using the code in question 8
Which set of student id is in the output of `full_join(test_score, student_info)`
    a. 1, 3, 5
    b. 7, 9
    c. 1, 3, 5, 7, 9
    d.  1, 2, 3, 4, 5, 7, 9
