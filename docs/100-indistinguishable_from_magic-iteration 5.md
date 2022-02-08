


# Iteration

*Written by José Casas and last updated on February 2022.*

## Introduction

When doing analyses or programming, there are many times where you have to repeat the same operation many times on different inputs. In this lesson, you will learn how to:

  - use loops, `purrr::map`, and many of its derivative functions to iterate a task
  - read in many files into R iteratively
  - write safe iterations

Prerequisites:

  - Vectors, lists, and indexing
  - Functions
  - Pipe operator (`%>%`)

## Before iterating

Before you start writing your code to iterate through a list/vector/etc., you have to understand what's in there, so that you can account for any variations in your input. One tip for when you want to iterate over many things: try to do it for just one or two things first. When you get a few things working fine, it's easy to make it into an iteration. This is better than trying to iterate over many things in the first go and wasting a lot of time if (when) something goes wrong.

## For loops

One way to do iterations is through the classic *for* loop. In R, for loops have three parts: output (usually a vector or list with enough space allocated in it), sequence (what the for loop will loop over, usually called `i`), and body (the action that the loop will perform over `i` iteratively).

An example of a simple usage of a for loop in R:

```r
output = vector(mode = "double", length = 5) # output allocation
for (i in 1:5) {                             # sequence
  output[[i]] = sqrt(i)                      # body
}
output
#> [1] 1.000000 1.414214 1.732051 2.000000 2.236068
```
In R, for loops are not used very often, and it is usually preferred to use the "body" as a function and then calling that function using a different method that we'll talk about below.

## `purrr`'s `map`

Simply put, `purrr::map()` is a function that applies a function to each element of a list. A basic template of its usage is:
```map(some_list, some_function, ...)```

  - The first input, `.x`, is your list/vector/etc.
  - The second input, `.f`, is the function to apply to each component of `.x`.

`map` always returns a list containing each of the outputs of applying the function `.f` to each of the elements in `.x`.

`map` also has type-specific cousins, which are `map_lgl()`, `map_int()`, `map_dbl()`, and `map_chr()`. These functions return a vector of the type indicated in the name, rather than the lists returned by `map()`. The types are as follows:
  
  - `map_lgl()` → logical vector
  - `map_int()` → integer vector
  - `map_dbl()` → double vector
  - `map_chr()` → character vector

These type-specific functions will fail if they can't return a vector of the specified type. This is useful for when you want to control your function so that it doesn't give you outputs of the wrong type.

A very simple example of using `map`:

```r
numbers = c(4, 9, 16)

map(numbers, sqrt) # sqrt is the base R square root function
#> [[1]]
#> [1] 2
#> 
#> [[2]]
#> [1] 3
#> 
#> [[3]]
#> [1] 4
```
As you can see, it returns a list containing each of the outputs of applying `sqrt` to each number in the vector `c(4, 9, 16)`. We will get to more complex examples soon.

There are three ways you can specify a function to `map`:

  - The normal way. Calling the function name in `map`. \newline
    `map(your_input, your_function)`
  - Defining a function inside the `map` call. \newline
    `map(your_input, function(x) [function body goes here])`
  - Using a formula. Also inside `map`, using the `~` symbol and using `.x` to refer to the input. \newline
    `map(your_input, ~ some_new_function(.x, ...))`

## `map`'s other friends

There are many variations of the `map` function, and they all have a specific purpose. Since there are so many, it can get pretty confusing to know which one does what, but you can always refer to the documentation for each one (by typing `?` before the function name in the R console, e.g. `?purrr::map()`) or use [this `purrr` cheatsheet from RStudio](https://raw.githubusercontent.com/rstudio/cheatsheets/main/purrr.pdf) to help you remember.

Here are some important ones:

### `map_dfr` & `map_dfc`
`map_dfr()` and `map_dfc()` are like the other type-specific `map` functions, but they are special because they return a **data frame** created by row-binding and column-binding, respectively.

They are also useful when you want to read in data from multiple files like CSVs or Excel sheets. We will look at an example of that later.

### `map2` and `pmap`
Now, you might be thinking "if `map` is so good, then why isn't there a `map` 2?" And boy oh boy, have I got a function for you.

With `map2()`, you can apply a function over two vectors/lists in parallel. A basic template of its usage is:
```map2(first_list, second_list, some_function, ...)```
And the function you pass in (`some_function` in this example) should have two parameters, for which the two inputs of `map2` (`first_list` and `second_list` in this example) will be used. This makes it easier to make iterations using both data and models, of the form `map2(models, datasets, predict)`.

`map2()` also has the same type-specific cousins as `map()`: `map2_lgl()`, `map2_int()`, etc.


```r
odd_numbers = c(1, 3, 5)
even_numbers = c(2, 4, 6)

map2(odd_numbers, even_numbers, `+`) # you can pass in operators as functions!
#> [[1]]
#> [1] 3
#> 
#> [[2]]
#> [1] 7
#> 
#> [[3]]
#> [1] 11
```

Now, if you need to iterate over two or *more* lists in parallel, `pmap` works for that. A basic template of its usage is:
```pmap(list_of_input_lists, some_function, ...)```
Where `list_of_input_lists` is a (nested) list that contains all the lists you want to use in parallel. And again, the function you pass should have parameters for each of the inputs in the list you pass to `pmap`.


```r
odd_numbers = c(1, 3, 5)
even_numbers = c(2, 4, 6)
more_numbers = c(7, 8, 9)

all_numbers = list(odd_numbers, even_numbers, more_numbers)

pmap(all_numbers, sum)
#> [[1]]
#> [1] 10
#> 
#> [[2]]
#> [1] 15
#> 
#> [[3]]
#> [1] 20
```

### `reduce`
With `reduce`, you can combine the elements of a list/vector into a single value, through a specified function, iteratively. That is, it takes the first two elements, combines them through the function (e.g. `+` to sum them), and then combines that result with the next element, and so on. An example of its usage is:

```r
numbers = c(2, 3, 4)
reduce(numbers, `+`) # same as saying (2 + 3) + 4
#> [1] 9
reduce(numbers, `^`) # same as (2^3)^4
#> [1] 4096
```

You can also specify the order in which to reduce the list

```r
numbers = c(2, 3, 4)
reduce(numbers, `^`, .dir = "backward") # same as 2^(3^4)
#> [1] 2.417852e+24
```

### `walk`
`walk` is for when you don't care about the return value of a function, and only want to use the function for its process. For example, if you wanted to generate and save an image of a `ggplot` graph of 50 different data frames, or save multiple cleaned data frames to CSV files. These tasks would not have a return value, but they still do something. 

You use it in the same way as `map`, like this:

```r
numbers = c(4, 25, 9)
walk(numbers, print)
#> [1] 4
#> [1] 25
#> [1] 9
```

As an example, imagine we have many data frames with Weight and Height measurements from many dogs of a different breed in each data frame. We will create a function that will generate a scatterplot of a certain data frame, and save the image with the data frame's name using `walk`.

```r
# Define the function
generate_scatterplot = function(dat){ # here dat is the dataframe parameter
  dat %>% 
    ggplot(aes(x = Weight, y = Height)) +
    geom_point() %>% # notice it is %>% and not + here!
    ggsave(paste0(substitute(dat), ".png"))
    # substitue(dat) return the name of the argument given as dat
}

# Use walk to save images to computer
walk(some_list_of_dataframes, generate_scatterplot)
```
There are different ways to do this, of course. For example, you could separate the steps into first generating all the plots, and then saving all of them as images.

`walk` also has parallel versions: `walk2` and `pwalk`, which work in the same way as `map2` and `pmap`.

`walk`, `walk2`, and `pwalk` all return the first argument (invisibly, so it is not printed as output), this is useful for when you want to use them in the middle of a pipeline, like this:

```r
numbers = c(4, 25, 9)

numbers %>% 
  sqrt %>% # calculate square root of numbers
  walk(print) %>% # print all numbers one by one
  sqrt # calculate square root again
#> [1] 2
#> [1] 5
#> [1] 3
#> [1] 1.414214 2.236068 1.732051
```

## Reading in many files

Most times, when working in R you need to load in your data from some source, and that source is usually a CSV or Excel file. This can easily be done with `read.csv` (also `readr::read_csv()`) or `readxl::read_excel`, respectively. Whenever you have a directory with many different files that you want to load into R, you can save a lot of time by doing do iteratively!

A simple way to do this is to use the `list.files()` function to get a list of all the file names you want to read in. You can use some simple regex in `list.files` to indicate that you only want files with a specific type, like .csv or .xlsx.

```r
files_to_read = list.files(path = "data/", pattern = "*.csv")
```
Here, `path = "data/"` means that it should look inside a folder called 'data', and `pattern = "*.csv"` means that it will select all file names that end in '.csv'.

Then, you can use `map` to iterate reading all the names in the list:

```r
map(files_to_read, read.csv)
```
Which will give you a list of data frames of each of the CSV files in the 'data' folder. If you wanted to combine them all into one, you can use a function like `bind_rows`.

Another quick way to do this is by using `map_dfr`, which will output a new data frame created by merging all the elements by row automatically:

```r
map_dfr(files_to_read, read.csv)
```

## Writing safe iterations

A very useful thing from `purrr` is the `safely()` function. It works by taking a function and returning a list with two elements:

  - `result`: the normal result of the function if there were no errors (otherwise it is `NULL`)
  - `error`: an error object if there was an error (otherwise it is `NULL`) \newline *Note that it will only have one or the other

This is specially useful for when you are working with really big lists or inputs that take a long time to run. This way, if there is an error along the way, your code will take a note of the error and it will keep going so you won't lose all your progress.


```r
safe_sqrt = safely(sqrt) # pass in the function sqrt
safe_sqrt(9) # will give no error
#> $result
#> [1] 3
#> 
#> $error
#> NULL
safe_sqrt("a") # will give an error
#> $result
#> NULL
#> 
#> $error
#> <simpleError in .Primitive("sqrt")(x): non-numeric argument to mathematical function>
```

`safely` works with `map` too:

```r
numbers = list(9, 16, "abc")

map(numbers, safe_sqrt)
#> [[1]]
#> [[1]]$result
#> [1] 3
#> 
#> [[1]]$error
#> NULL
#> 
#> 
#> [[2]]
#> [[2]]$result
#> [1] 4
#> 
#> [[2]]$error
#> NULL
#> 
#> 
#> [[3]]
#> [[3]]$result
#> NULL
#> 
#> [[3]]$error
#> <simpleError in .Primitive("sqrt")(x): non-numeric argument to mathematical function>
```
So you can see how it's useful.

And, if you wanted to get a list with just the results and another with just the errors, you can use `transpose()`:

```r
map(numbers, safe_sqrt) %>% transpose()
#> $result
#> $result[[1]]
#> [1] 3
#> 
#> $result[[2]]
#> [1] 4
#> 
#> $result[[3]]
#> NULL
#> 
#> 
#> $error
#> $error[[1]]
#> NULL
#> 
#> $error[[2]]
#> NULL
#> 
#> $error[[3]]
#> <simpleError in .Primitive("sqrt")(x): non-numeric argument to mathematical function>
```

If you don't care about errors, then you can use the simpler function `possibly()`. With `possibly()`, you can specify a default value for when it encounters an error.


```r
possibly_sqrt = possibly(sqrt, NA)

map(numbers, possibly_sqrt)
#> [[1]]
#> [1] 3
#> 
#> [[2]]
#> [1] 4
#> 
#> [[3]]
#> [1] NA

map_dbl(numbers, possibly_sqrt) # want something simpler? use map_dbl()
#> [1]  3  4 NA
```

If you want to save the actual printed output, warnings, and messages, you can use `quietly()`. For example:

```r
numbers = list(9, -10) # sqrt(-10) gives the warning "NaNs produced"
quiet_sqrt = quietly(sqrt)

map(numbers, quiet_sqrt)
#> [[1]]
#> [[1]]$result
#> [1] 3
#> 
#> [[1]]$output
#> [1] ""
#> 
#> [[1]]$warnings
#> character(0)
#> 
#> [[1]]$messages
#> character(0)
#> 
#> 
#> [[2]]
#> [[2]]$result
#> [1] NaN
#> 
#> [[2]]$output
#> [1] ""
#> 
#> [[2]]$warnings
#> [1] "NaNs produced"
#> 
#> [[2]]$messages
#> character(0)
```

## Notes
`map()` is basically the same as the base R function `lapply()`, but its syntax is more consistent with the rest of the purrr functions and you can use the `.f` shortcut in the function parameter.

`safely()` is similar to the base R function `try()`, but `try()` can be more difficult to work with since its output is less predictable.

## Exercises

### Question 1
What will be the output on the following code?
```
output = vector(mode = "double", length = 3)
for(i in 1:3) {
  output[[i]] = i - 1
}
output
```

  a. 0 0 0
  b. -1 0 1
  c.  0 1 2
  d. It will give an error.

### Question 2
What will be the output of the following code?
```
map_lgl(c(1, 2, 3), sqrt)
```

  a. 1.000000 1.414214 1.732051
  b. 1 1 1
  c. 1 1 0
  d.  It will give an error.

### Question 3
Which of the following function calls in `map` gives an error?

  a. `map(c(1, 2, 3), sum)`
  b. `map(c(1, 2, 3), function(x) x + 1)`
  c. `map(c(1, 2, 3), ~ .x + 1)`
  d.  None will give an error.

### Question 4
Which of the options will *NOT* give the following output *vector*?
```
## 1 2 3
```

  a.  `map(c(1, 2, 3), sum)`
  b. `map_dbl(c(1, 2, 3), sum)`
  c. `map_dbl(c(1, 2, 3), ~ .x)`
  d. All of them will give that output.

### Question 5
Which of the options will give the following output?
```
## [[1]]
## [1] 3
## 
## [[2]]
## [1] 7
## 
## [[3]]
## [1] 11
```

  a. `map2(c(1, 3, 5), c(2, 4, 6),` \``+`\``)`
  b. `pmap(list(c(1, 3, 5), c(2, 4, 6)),` \``+`\``)`
  c.  Both a and b.
  d. None.

### Question 6
Are the following two lines equivalent?
```
reduce(c(2, -3, .4), `+` )
reduce(c(2, -3, .4), `+`, .dir = "backward")
```

  a.  Yes
  b. No

### Question 7
What is the output of the following code?
```
out1 = map(c("aa"), ~ paste0(.x, "a"))
out2 = map_chr(c("aa"), ~ paste0(.x, "a"))

out1 == out2
typeof(out1) == typeof(out2)
```

  a.  TRUE, FALSE
  b. TRUE, TRUE
  c. FALSE, FALSE
  d. It will give an error.

### Question 8
Which option will give the following output?
```
## [1] 1
## [1] 2
## [1] 3
```

  a. map_dbl(c(1, 2, 3), ~ .x)
  b. map_dbl(c(1, 2, 3), print)
  c.  walk(c(1, 2, 3), print)
  d. All of them.

### Question 9
Which function could you use if you wanted to know whether there was an error in your summations?

  a. `safely(sum, NULL)`
  b. `possibly(sum, NULL)`
  c. `quietly(sum)`
  d.  All of them

### Question 10
Which of the following options would successfully sum up all the elements in `numbers = c(1, 2, 3)`?

  a. `map(numbers, sum)`
  b. `map(numbers,` \``+`\``)`
  c.  `reduce(numbers, sum)`
  d. None.

## References

  - Iteration | R for Data Science ([r4ds.had.co.nz/iteration.html](https://r4ds.had.co.nz/iteration.html))
  - purrr tutorial: Lessons and Examples ([jennybc.github.io/purrr-tutorial](https://jennybc.github.io/purrr-tutorial/))
  - Apply a function to each element of a list or atomic vector — map | purrr ([purrr.tidyverse.org/reference/map](https://purrr.tidyverse.org/reference/map.html))
  - Other purrr functions | Functional Programming ([dcl-prog.stanford.edu/purrr-extras.html](https://dcl-prog.stanford.edu/purrr-extras.html))
