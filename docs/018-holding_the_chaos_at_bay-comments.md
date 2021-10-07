


# Writing comments

*Written by Isaac Ehrlich and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn what a comment is, as well as how and when to write them.

### What is a comment?

Comments are lines of plain text written within code files. The general purpose of comments is to explain what is happening in your code and why. The following sections will outline how to write comments and when they should be used.

## Comments

### Why comment?

When revisiting code you have previously written or when reviewing someone else's code, it is not always immediately clear what the code is doing or how it is working - especially if it is not commented. This makes code difficult to interpret, and hard to edit. By adding comments and explaining what is happening in the code, you make it easier to decipher and understand for when you inevitably return to it in the future.

### How to comment?

In R, comments are written by adding a `#` before text, typically at the beginning of the line. This means that anything written after the `#` will not be interpreted as code by R, but rather as text. Comments also typically precede the code they are referring to.


```r
 # Anything following the octothorp is a comment
 # Writing code after an octothorp will have no effect, even if properly formatted
```

If you want to comment more than one line of code, you can select the desired lines and then use the shortcut **"ctrl + shift + C"** (or **"cmd + shift + C"** on Mac).

### When to comment?

Comments are typically used to improve the readability of code, either by partitioning code into sections, explaining the code, or providing links to additional resources. Not every line of code needs a corresponding comment, it is up to you to determine when you should write a comment. There are certain instances however that typically benefit from commenting.

1. Defining Code Sections

You can use comments to divide sections of your analysis. Often, you can split a single script into multiple sections, such as setting up the environment, writing functions, and sections of your analysis.


```r
# Load Packages
library(tidyverse)
# library(learnr)

# Load Data

# Data Cleaning

# Functions

# And So On

```

2. Functions

When you write new functions, its common practice to explain the inputs, output, and purpose of each function


```r
# Functions

addition <- function(x, y)
# The function addition takes numeric inputs 'x' and 'y' and outputs their sum
  sum <- x + y
return(sum)

subtraction <- function(x, y)
# The function subtraction takes numeric inputs 'x' and 'y' and outputs their difference
  diff <- x - y
return(diff)
```

3. Complex Code

While performing operations such as addition or subtraction typically won't require commenting, once your code begins to involve complex chunks and functions, it becomes important to explain what is going on so that you don't need to figure it out again in the future.

4. Providing Reasoning or Linking to Additional Resources

When performing analyses, you may make decisions based on reasoning that is not always evident. In these situations, it is helpful to include a comment explaining the decision you've made. If your code or reasoning also refers to some external source, it may be helpful to provide a link to the source.

## Preamble

Beyond commenting within your code, you may also want to begin each R script with a multi-line comment that provides general information about the contents of the script, also known as a preamble. This preamble may contain information such as the author, date, and purpose of the script.


```r
### Example Preamble ###
# Author: Your Name
# Date: The Date
# Contact: Your Email
# Prerequisites: Necessary Data of Folder Set-Up
# Links or Resources
# Purpose
```

## Exercises

<!-- ```{r commentsq2, echo = FALSE} -->
<!-- question("Comments should be made when (select all that apply)", -->
<!-- answer("dividing code into sections", correct = TRUE), -->
<!-- answer("explaining complex code", correct = TRUE), -->
<!-- answer("explaining a function", correct = TRUE), -->
<!-- answer("linking to resources", correct = TRUE), -->
<!-- answer("describing a decision process", correct = TRUE), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

<!-- ```{r commentsq1, echo = FALSE} -->
<!-- question("I only need to comment when my professor asks me to. Comments do not help the author at all", -->
<!-- answer("True", message = "Remember you will need to look back and understand your code too! Comments are a crucial step in organizing and understanding code!"), -->
<!-- answer("False", correct = TRUE, message = "Make sure you comment thoroughly so you can understand your code when you look back on it!"), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->


## Key takeaways

* Comments are an invaluable way to organize code and improve readability
* Comments are an effective way of explaining code and the decisions made when writing
* Comments help the author just as much as they help other readers!
* Simple commands and lines do not require comments, but make sure to always comment thoroughly where necessary!


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
