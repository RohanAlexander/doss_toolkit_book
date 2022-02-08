


# Coding style

*Written by Marija Pejcinovska and last updated on 7 October 2021.*

By now you've probably worked through dozens of modules and are feeling a lot more comfortable coding in R. This is a good spot to spend a moment or two thinking about your coding style. A good style will help you keep your R scripts consistent and easy to read (and, of course, easier to navigate through when you revisit them at a later time). In this lesson we'll focus on the coding style used throughout the `tidyverse`. More specifically, we will highlight some naming conventions for objects and functions and discuss useful structures that will make your programs easier to write and read.

Prerequisite skills include:

- Some data manipulation
- The tidyverse
- Writing basic functions and conditional statements 


## Naming things: the tidy way

### Naming files 

In a previous lesson you learned how to set up folders and organize files in your R projects. Here we'll talk about a few things you might want to keep in mind when naming your R files.  

  * Make sure your file have meaningful (though if possible also relatively short) names that end in `.R`. 
  * Try sticking to a specific capitalization. The tidyverse style recommends using lower case letters.
  * Avoid spaces and special characters. Consider separating words in a file name by using `_` or `-`. 



```r

# A good example of file name

my_first_script.R

# And a few bad (and less than ideal) examples

my first script.R   # there should be no spaces
myfirstscript.R     # not a terrible file name but hard to read; 
my_first_script.r   # r should be capitalized
file1.R           # not descriptive enough
models&results.R          # contains special characters

```


### Naming objects

Just like with file names, you should name your R objects using descriptive and informative names. Here are some guidelines to keep in mind:

  - Object and function names should start with a letter (and not a number)!

```r
# Good 
group_1
# or
group_one

# Bad 
1st_group
```
  
  - Names should include only letters, numbers, `_`, and `.`. Though, you should probably decide on a single separator; pick either `_` or `.` to be somewhat consistent and follow basic conventions.
  - Since classes and methods in the S3 object system use dots, to avoid confusion, it might be best to use `_` in your function names. 
  - In fact, the tidy style guide, in general, recommends using `_` to separate words both in function names and object names. Separating lowercase words with `_` is sometimes referred to as using *snake_case*.
  - To avoid errors, names should be kept as short as possible.
  - When naming your functions consider using active verbs 
  

```r
# Okay function names
permute()
count_event()

# Less okay
permuatation()
event_counter()

```

  - Typos and cases matter; so, be careful when calling your objects and functions. Sometime errors in your code can be misspellings. 
  - Avoid re-using names of common R functions and variables. For instance, avoid naming objects `T` or `F` since R reserves these for `TRUE` and `FALSE`.
  

  
## Tidying up your "syntax"

### Commas and spaces

Many of the syntax rules in the English language are applicable to R coding. Commas and spaces are a good example of this. 

  - Place spaces after commas, but not before them (just like you would when you write).

```r
# Good 

B[, 2]

# Not so good

B[,2]
B[ ,2]
B[ , 2]

```
  
  - Avoid putting space between your function name and the arguments in parenthesis when calling your function  
  

```r

# Do
sum(x)

# Don't

sum (x)
sum( x )
```
  

  - When using conditional (`if`, `for`, `while`) statements separate the condition expression in `()` by placing space around `()`
  

```r

# Good

while (i < 10) {
  print(i)
}

# Not so good

while(i<10){
  print(i)
}

```
  
  - *Infixed* operators (i.e. those placed between operands), such as `==`, `+`, `-`, `<-` and so on, **should always** be surrounded by spaces:
  

```r

# Good
my_var <- y + 24 + (x * 0.5)


# Not great

my_var<-y+24+(x*0.5)
```

  - There are, however, a few exceptions to the above rule. *Operators with high precedence*, such as those that access stuff in a namespace (`::`, `:::`), those used for extracting slots or components (`$`, `@`), those used for indexing (`[]`, `[[]]`), the exponentiation operator (`^`), or the sequence operator (`:`) *should not* be surrounded by space.
  

```r

# Good
x <- data$height
y <- 1:20
z <- x^2

# Bad
x <- data $ height
y <- 1 : 20
z <- x ^ 2

```
  
### Curly braces and code hierarchies

  - When writing functions and conditional statements which are not short or simple you would need should be pacing your code in a block sectioned off by **curly braces**. Enclosing the "body" of your function or conditional statement inside curly braces allows one to more easily see the hierarchy of a piece of code. There are few things to keep in mind here: 
    + `{` should be the last character on a line. Once you open the left squiggly bracket start the actual body of the code in a new line. 
    + The code content inside the curly braces should be indented by two spaces. By skimming the left-hand margin, this way you'll be able to see the hierarchy of the code block more easily
    + When you are done with specifying the code that defines your function or conditional statement place the closing curly brace on a new line, so that it's the first character on the line. In fact, unless it is followed by `else {`, the closing curly brace should be on its own line.
    

```r
# Good
if (x < 3) {
  exp(x)
} else {
  x^3
}

if (i < 10){
  if (x > 0){
    y = log(x)
  } else {
    y = x
  }
} else {
  message("i is too large")
}


# Not so good
if (x < 3) {
  exp(x)
} 
else {
  x^3
}

if (i < 10){
  if (x > 0){
    y = log(x)
  } else {
    y = x
  }
} else {
  message("i is too large")
}

```
    


### Few other notes on syntax

  - Avoid using semicolons (`;`) at the end of a line of code. 
  - Avoid putting multiple commands on one line; hence, avoid using semicolons to separate multiple commands on one line! 
  - You can use `<-` or `=` for assignment in R, however, the tidyverse style guide strongly advocates for consistently using `<-` for value assignment.

```r
# Do
my_var <- 7

# Maybe don't do
my_var = 7
```
  - The pipe operator,` %>% `, should be preceded by space and should usually be followed by a new line. Just like indentation in code blocks the code following a pipe should be indented by two spaces.

```r
# Good
data %>% 
  filter(x > 10) %>% 
  group_by(my_cat_var) %>% 
  summarize(my_sum = sum(my_other_var)) %>% 
  ungroup()

# Not so good
data %>% filter(x > 10) %>% group_by(my_cat_var) %>% summarize(my_sum = sum(my_other_var)) %>% 
  ungroup()

```
  


## Exercises

<!-- ```{r style_q1, echo=FALSE} -->
<!-- question("Which one of these follows the tidy style?", -->
<!--          answer("x<-3"), -->
<!--          answer("x=3"), -->
<!--          answer("x <- 3", correct = TRUE), -->
<!--          answer("x < - 3")) -->
<!-- ``` -->



<!-- ```{r style_q2, echo=FALSE} -->
<!-- question("Select the appropriately styled line of code?", -->
<!--          answer("here::here(\"data/my_file.R\")", correct = TRUE), -->
<!--          answer("here::here (\"data/my_file.R\")"), -->
<!--          answer("here ::here(\"data/my_file.R\")") -->
<!-- ) -->
<!-- ``` -->


## Next Steps

This tutorial is largely based on content in the tidyverse style guide. For more detailed information check out: https://style.tidyverse.org/




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
