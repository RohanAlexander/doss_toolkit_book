


# for and while

*Written by Yena Joo and last updated on 7 October 2021.*


## Introduction

In this lesson, you will learn about "loops", and how to use the function `for` and `while`. It is one of the key concepts that is widely used and fundamental for any kind of programming languages.  

### What are Loops?
Loops, or iterations are a step that the program automatically goes through certain logical conditions or a range of a list, array, vector, dataset, and many more. Loops allow code to be executed repeatedly, which is used often in programming to repeat a specific block of code. You can make hundreds and thousands of redundant codes into a few lines of simple code using loops. 

You can iterate through:  

- vectors: `fruits <- c('apple', 'banana', 'mango')`   
- lists: `list <- list(1, 2, "melon")`   
- datasets/tibble  
- range of numbers  
- sequence: `seq(from=0,to=8,by=2)`   


Prerequisite skills include:  

- You should be familiar with the basic data manipulation.  
- You should understand how vectors, lists, tibble, etc. works  


Highlights:  

- How `for` and `while` loops work and some examples  
- Differences between the two  
- Nested Loops  
- `break` in loops  

### Packages

```r
library(tidyverse)
```

## `for()`

### Structure 


```r
for(var in iterable) { 
  #statement
  print(var)
}
#another statement
```

The structure of the for loop is simple. You start with `for()` to indicate that you are going to use the for loop. The argument to the `for()` consists of a variable, which takes items from iterable one by one. Iterable is a collection of objects (like a list, vector, sequence, etc.) For each iteration in the `for` loop, a value is taken from the list and assigned to the variable, and the following statement in the curly braces, `{}` is evaluated. 

Let's take a look at an example.


```r
index<-seq(1,10,by=2) 
for(i in index){ 
  print(i) 
}
#> [1] 1
#> [1] 3
#> [1] 5
#> [1] 7
#> [1] 9
```

Here is sequences from 1 to 10, by 2. If you iterate through the sequence using for loop and print each variable, each value is taken from the sequence and print, which is the statement in the curly braces `{}`.   


### Mutating a Dataset using `for()`

Now, let's use a different dataset to add some new variables using for loop, and get some useful information. Let's first create a simple dataset of grades of each student in `math`, `cs`, `sta` courses. 


```r
set.seed(6055)
student_id <- c(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
math <- sample(c(60:100), size=10, replace=TRUE)
cs <- sample(c(60:100), size=10, replace=TRUE)
sta <- sample(c(60:100), size=10, replace=TRUE) 
## tibble()
student_data <- tibble(student_id, math, cs, sta)
student_data
#> # A tibble: 10 × 4
#>    student_id  math    cs   sta
#>         <dbl> <int> <int> <int>
#>  1          1    67    87    66
#>  2          2    72    92    88
#>  3          3    81    99    73
#>  4          4    62    94   100
#>  5          5    62    86    98
#>  6          6    80    93    63
#>  7          7    65    74    86
#>  8          8    96    97    86
#>  9          9    96    66    66
#> 10         10    83    72    87

## data.frame()
student <- data.frame(student_id, math, cs, sta)
student
#>    student_id math cs sta
#> 1           1   67 87  66
#> 2           2   72 92  88
#> 3           3   81 99  73
#> 4           4   62 94 100
#> 5           5   62 86  98
#> 6           6   80 93  63
#> 7           7   65 74  86
#> 8           8   96 97  86
#> 9           9   96 66  66
#> 10         10   83 72  87
```

Then, let's say we want to see each student's total mark as well as their average mark. First, we have to assign numeric variable names for `avg` and `tot`, and n is going to be the number of students, which is number of rows of the data. 


```r
## empty vector
avg <- numeric()
tot <- numeric()
n <- nrow(student)  ## number of students
```


We will now use `for` loop iterating from range 1 to the number of students, and for each iteration, we will assign `tot` be the total mark of `math`, `cs`, and `sta`. Average grade would be total grade divided by 3 courses. 

```r
## tot and avg
for(i in 1:nrow(student)){
  tot[i] <- student$math[i] + student$cs[i] + student$sta[i]
  avg[i] <- round(tot[i]/3, 2)
}

## new col
student$tot <- tot
student$avg <- avg

student
#>    student_id math cs sta tot   avg
#> 1           1   67 87  66 220 73.33
#> 2           2   72 92  88 252 84.00
#> 3           3   81 99  73 253 84.33
#> 4           4   62 94 100 256 85.33
#> 5           5   62 86  98 246 82.00
#> 6           6   80 93  63 236 78.67
#> 7           7   65 74  86 225 75.00
#> 8           8   96 97  86 279 93.00
#> 9           9   96 66  66 228 76.00
#> 10         10   83 72  87 242 80.67
```

Let's say we want to know how many students got their average grade higher than 80 which is A. We can use `for` in this case, to go through each student's average grade, and determine if the average grade is over 80, we can increase the arbitrary variable assigned- `a`-  by 1 in each iteration. 


```r
a <- 0
for (i in 1:nrow(student)) {
  if(student$avg[i] >= 80){
    a = a + 1
  }
}
a
#> [1] 6
```


### Nested `for()` loops 
A nested `for` loop is a loop within a loop. They are useful for when you want to repeat a statement several times for several things.

Nested `for` loops are often used to manipulate a bi-dimensional array by setting its elements to specific values.  

The placing of one loop inside the body of another loop is called nesting.  When you “nest” two loops, the outer loop takes control of the number of complete repetitions of the inner loop. Thus inner loop iterates n times where the length of the array of inner for loop is n, for every execution of the outer loop.

Let's take a look at a simple example. 

```r
for(i in 1:2) {
  for(j in 1:3) {
    print(i*j);
    }
}
#> [1] 1
#> [1] 2
#> [1] 3
#> [1] 2
#> [1] 4
#> [1] 6
```
The outer for loop iterates through c(1, 2), and the inner loop is c(1, 2, 3)
First, i = 1. We have to iterate through 1, 2, 3 now for j. `1*1`, `1*2`, `1*3` is executed respectively. Same for i = 2. Therefore, you can see that the number of the returned outputs is equal to the number of outer loops multiplied by the number of inner loops: 2 x 3. 


## `while()`
There is another way to create loops, using `while` statement. The `while` loops are used to loop until a specific condition is met/satisfied. In for loops, we already know how many times the loop will run. However, `while` can be used when the exact number of iterations is not known.  

### Structure

```r
while (condition) {
  statement
}
```
  
The structure of the while loop is similar to the for loop. `condition` is evaluated whether it is `TRUE` or `False`. It enters the body of the loop, which is the `statement` when the result of the condition is `TRUE`. Then, after executing the statement, the same process is repeated until `condition` has a `FALSE` result, and the loop exits.


### Example
Let's start with a simple example without using a dataset. 

```r
i <- 0 
while (i < 5){
  print(i)
  i = i+1
}
#> [1] 0
#> [1] 1
#> [1] 2
#> [1] 3
#> [1] 4
i 
#> [1] 5
```
Here, the condition is `i < 5`, which evaluates `TRUE` in the first loop, since 1 < 5.  
So, the loop enters the body, prints 1, and i is incremented by 1 since the body is `i = i + 1`. In the next iteration, 2 < 5 so the loop repeats the same step, until i becomes 5. 5 is not smaller (`<`) than 5, which evaluates `FALSE` in the condition `i < 5`. Here, the loop terminates. 


## Differences between `for()` and `while()`

- `for()` is used when you know how many iterations the code should go through.   
- `while()` is used when the number of iteration depends on the condition, and evaluates whether the condition is 'TRUE' or 'FALSE'. If it is evaluated 'FALSE', the loop terminates.  
- This means that in `while()` loops, most of the time you will need to code the incrementation yourself, such as `i = i + 1` so the loop would terminate at some point.   



## Exercises

### Question 1 
Here is a simple `for` loop code: 

<!-- ```{r eval = F} -->
<!-- example <- c(a, b, c) -->
<!-- for (i in example){ -->
<!--   print(example[i]) -->
<!-- } -->
<!-- ``` -->
<!-- ```{r q1, echo = F, exercise.eval = TRUE} -->
<!-- question_checkbox( -->
<!--   "What is the correct output of the code above? ", -->
<!--   answer("a b c ", correct = T), -->
<!--   answer("(a, b, c) (a, b, c) (a, b, c) ", message = "Check the statement again"), -->
<!--   answer("c b a ", correct = F), -->
<!--   answer("a", correct = F), -->
<!--   allow_retry = T, -->
<!--   random_answer_order = T, -->
<!--   incorrect = "Try again. You got this!" -->
<!-- ) -->

<!-- ``` -->


### Question 2
Here is a dataset of people who climbed Mount Himalayan. How many members were injured? Use the `for` loop to get the answer. (Hint: look for the variable `injured` to set the `if` condition inside the loop)


<!-- ```{r, echo = F, message = F} -->
<!-- members <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-09-22/members.csv') -->
<!-- head(members) -->
<!-- ``` -->


<!-- ```{r q2, exercise.eval = TRUE, exercise=TRUE} -->
<!-- members <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-09-22/members.csv')   -->

<!-- ``` -->

<!-- ```{r q2-solution} -->
<!-- x <- 0  -->

<!-- for (i in 1:nrow(members)){ -->
<!--   if(members$injured[i] == T){ -->
<!--     x = x + 1 -->
<!--   } -->
<!-- } -->
<!-- x -->
<!-- ``` -->

### Question 3
The following is a simple `while` loop code. 


```r
i = 15
while (i > 10){
  i = i -1
}
i 
```

<!-- ```{r q3, echo = F, exercise.eval = TRUE} -->
<!-- question_checkbox( -->
<!--   "How many iterations does the while loop go through until it terminates?", -->
<!--   answer("3", correct = F), -->
<!--   answer("4 ", correct = F), -->
<!--   answer("5", correct = T), -->
<!--   answer("6", correct = F), -->
<!--   allow_retry = T, -->
<!--   random_answer_order = T, -->
<!--   incorrect = "Try again. You got this!" -->
<!-- ) -->

<!-- ``` -->


## Common mistakes & errors

- It is easy to forget to put curly braces after the loop statement. If you only have one statement to execute, you don't need to put the curly braces `{}`. However, if you have multiple statements, `{}` is necessary. You won't get the result you want without the curly braces.  

- Be aware of your use of the iterable object. For example, `for (i in student)` would not execute the result you want in the previous example. Let's say you would want to give bonus marks to one of the courses. Then you should use `1:nrow(student)` as your iterable object as follows:  


```r
for (i in 1:nrow(student)) {
  student$cs[i] = student$cs[i] + 1
}
head(student)
#>   student_id math  cs sta tot   avg
#> 1          1   67  88  66 220 73.33
#> 2          2   72  93  88 252 84.00
#> 3          3   81 100  73 253 84.33
#> 4          4   62  95 100 256 85.33
#> 5          5   62  87  98 246 82.00
#> 6          6   80  94  63 236 78.67
```

However, using `i in student` will iterate through the entire data, and the length of the iteration would be larger than the length of the number of the grades in the `cs` course.    

```
for (i in student) {
  student$cs[i] = student$cs[i] + 1
}
student
```
And the code will execute the following error message, if not, similar:  
```
“Error: replacement has X rows, data has Y”.
``` 
This happens since the length of the vector you are trying to replace does not match the length of the iteration.  

- Think carefully of what statement you're trying to iterate.  

## Next steps

- Practice how to manipulate data using `for` and `while` loops.

## References  

- [R for loop](https://www.datamentor.io/r-programming/for-loop/)
- [R while loop](https://www.datamentor.io/r-programming/while-loop/)


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
