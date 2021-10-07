


# When your code doesn't work

*Written by Michael Chong and last updated on 7 October 2021.*

## Introduction

This lesson contains:

- suggestions on how to avoid big problems in R
- possible ways to troubleshoot your R code

Prerequisite skills include:

- None!

Highlights:

<img src="images/08_troubleshooting-image.png" width="85%" style="display: block; margin: auto;" />

## Avoiding (big) issues 

### Use common packages where possible

There are *a lot* of R packages, collectively written by *a lot* of authors, and this inevitably means some packages may interfere with each other and some packages may not be well-documented. Because of this, as you're starting out, it's best to stick with packages that are well-maintained and widely used.

Most of the functions in this toolkit are from the `tidyverse` suite of packages, which fit these criteria. Try to stick with these functions, because they behave predictably together, and help is easier to find because of their wide use. 

### Check results as you go

It's easier to fix a small problem than a big problem. Whenever you're writing or editing an R file, here are some good practices that I follow:

1. test your code in your console before making the change in the file
2. check that the result of your code is what you expect it to be
3. every once in a while, clear your R environment, run your entire script or document, and check the results again

The third step is really important, because you want to make sure your script or document is *self-contained*. You want the script to be able to reproduce the results on its own when you come back to it later.

## Dealing with issues on your own

### Isolate the issue

Run your code bit by bit until you know which functions are making the problem. In the RStudio editor, you can do this by highlighting a portion of your code, and hitting `CTRL/CMD` + `Enter`. 

At each point, check that you're getting what you expect! For example, if your code changing an object over and over:


```r
my_number <- 23
my_number <- my_number * 2
my_number <- my_number - 12
```

then it can help to print the object after every time you change it:


```r
my_number <- 23
print(my_number)
#> [1] 23

my_number <- my_number * 2
print(my_number)
#> [1] 46

my_number <- my_number - 12
print(my_number)
#> [1] 34
```

### Check that you have the right packages loaded

Did you forget to use `library()` on the package you need? If you forgot, you probably get the error `could not find function`. For example, the `read_excel()` function comes from the `readxl` package. If you try to use it without loading the package, we get the following error:


```r
read_excel("some_file_name.xlsx")
#> Error in read_excel("some_file_name.xlsx"): could not find function "read_excel"
```

### Check for typos

Seems obvious, but make sure you're using the variables and functions that you're intending to use! 

### Check the built-in help

R and RStudio have great built-in references. To access the help document for a function, use `?function_name`. For example, if you want to access the help document for the `read_csv()` function, type `?read_csv` in the RStudio console, which brings up this help page. Equivalently, you can type `help(read_csv)`. 

## Escalating the issue

### Make a minimal example

Simplify the problem so it's easier to see what's going on! There are a couple ways you can do this:

* try it on a smaller, similar data set
* make up some fictional in the same format 

There's more on this in [another section]

### "General" Resources 

These can be good places to start if you're not familiar with the function or package you're using.

* **this toolkit!**
* [**R for Data Science** by Hadley Wickham](https://r4ds.had.co.nz/): the definitive online textbook resource for getting started in the `tidyverse`
* **package vignettes**: Some packages have *vignettes*, which are like user tutorials for the package written by the package authors. You can check for package vignettes using `browseVignettes("package_name")`

### Informal resources

If you know what that what you want to do is a bit unconventional or more complicated than usual, you can try:

* consult TAs, instructors, or other friendly experienced users
* search the web! More on this in [another section] 
* ask StackOverflow! More on this in [another section]

## Still stuck?

### Ask: "do I have other options?"

Some tasks are just *really*, **really** time-consuming or difficult to accomplish in R. Or there are just a lot of tools you would need to know before you can do what you want!

It's okay to adjust your goal or approach based on what's feasible! Some ways to do this:

* break your goal down into smaller parts
* write "pseudocode" first: write down what you want to do in plain words first, then translate to R code
* look for packages that al

### Remember to take a break!

It can be easy to get stuck thinking about a problem, and become consumed in an endless cycle of Googling and copying and pasting. Take a break and come back.

## Exercises

<!-- ```{r q1, exercise = FALSE, echo = FALSE} -->
<!-- question( -->
<!--   "Scenario: Reading over someone's code, and you don't know what `mutate()` does. How can you bring up the help document for `mutate()`? There are two multiple correct answers.", -->
<!--   answer("Type `mutate?`"), -->
<!--   answer("Type `?mutate`", correct = TRUE), -->
<!--   answer("Type `what_is(mutate)`", correct = TRUE), -->
<!--   answer("Type `help(mutate)`"), -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

<!-- ```{r q2, exercise = FALSE, echo = FALSE} -->
<!-- question( -->
<!--   "When writing code, it's best to:", -->
<!--   answer("write all the code first, and check for errors when finished"), -->
<!--   answer("check for errors frequently (every couple of lines)", correct = TRUE), -->
<!--   correct = "Yes! Checking often makes it easier to find where problems are.", -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

<!-- ```{r q3, exercise = FALSE, echo = FALSE} -->
<!-- question( -->
<!--   "You can bring up the vignettes for a package using the `browseVignettes()` function. What are vignettes?", -->
<!--   answer("User guides for the package written by package authors.", correct = TRUE), -->
<!--   answer("Instructions from the package authors on how to cite the package."), -->
<!--   answer("Technical stuff behind the package that's not worth worrying about."), -->
<!--   answer("Online forums discussing the package."), -->
<!--   correct = "Correct! These are a good place to go for help!", -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

## Next steps

* Asking for help? Learn how to make a minimal example in the **Making reproducible examples** lesson.
* Having trouble finding what you want on the web? See the lesson **Using Google and Stack Overflow** and **Even more on Stack Overflow** for tips on using these tools more effectively!


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
