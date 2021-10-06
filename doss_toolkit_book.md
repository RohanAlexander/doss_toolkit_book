--- 
title: "DoSS Toolkit"
author: "Various authors"
date: "2021-09-06"
site: bookdown::bookdown_site
documentclass: book
bibliography: [book.bib, packages.bib]
# url: your book url like https://bookdown.org/yihui/bookdown
# cover-image: path to the social sharing image like images/cover.jpg
description: |
  This is a minimal example of using the bookdown package to write a book.
  The HTML output format for this example is bookdown::bs4_book,
  set in the _output.yml file.
biblio-style: apalike
csl: chicago-fullnote-bibliography.csl
---

# url: your book url like https://bookdown.org/yihui/bookdown

Placeholder


## Usage 
## Render book
## Preview book
## Hello bookdown 
### A section
#### An unnumbered section {-}
## Cross-references {#cross}
### Chapters and sub-chapters
### Captioned figures and tables
## Parts
## Footnotes and citations 
### Footnotes
### Citations
## Blocks
### Equations
### Theorems and proofs
### Callout blocks
## Sharing your book
### Publishing
### 404 pages
### Metadata for sharing

<!--chapter:end:index.Rmd-->




# (PART\*) Hello World! {-}


# Introduction

*Written by Rohan Alexander.*

Welcome to the first module. In this module we focus on getting R and R Studio, and then showing you a couple of motivating examples that you'll soon have the skills to be able to write yourself.

Don't worry too much if the specifics of those examples leave you a little lost - that's normal. If you stick with it then it'll all make sense eventually.

Welcome aboard!


<iframe width="560" height="315" src="https://www.youtube.com/embed/ccbvKaQeKRY" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>




<!--chapter:end:000-hello_world-introduction.Rmd-->


# Getting and setting up RStudio

Placeholder


## Introduction
## R vs. RStudio
## Getting R
## Getting RStudio
## Next Steps

<!--chapter:end:001-hello_world-setup.Rmd-->


# Getting to know what is what

Placeholder


## Introduction
## Basic Layout
## More Advanced Features
## Next Steps

<!--chapter:end:002-hello_world-what_is_what.Rmd-->


# Hello World! 

Placeholder


## Introduction
## Video Walk Through
## Load Data
## Clean Existing Data
## Summarize Data
## Next Steps

<!--chapter:end:003-hello_world-hello_world_1.Rmd-->


# Hello World, again! 

Placeholder


## Introduction
## Data
## Favourites
## Patterns

<!--chapter:end:004-hello_world-hello_world_2.Rmd-->







# Hello World, yet again! 

<!--chapter:end:005-hello_world-hello_world_3.Rmd-->


# The R community

Placeholder


## Introduction
## R Weekly
### Get Involved
## R-Ladies
### Get Involved
## R Meetups
### Get Involved

<!--chapter:end:006-hello_world-community.Rmd-->





# (PART\*) Operating in an error prone world {-}


# Introduction

Written by Rohan Alexander.

Welcome to a module about getting help. While it may seem odd to start with this, one of the key skills when using R is being able to work yourself out of problems.

The good news is that after you spend time learning R those problems that you had at the start go away. The bad news is that they are replaced with new problems. It's not just you - everyone's code is always full of errors.

<iframe width="560" height="315" src="https://www.youtube.com/embed/82ogkkY7qeQ" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


<!--chapter:end:007-operating_in_an-introduction.Rmd-->


# Getting help is normal! -- Learning to learn R

Placeholder


## Introduction
## Learning R 
## Next Steps

<!--chapter:end:008-operating_in_an-learning_to_learn.Rmd-->


# Using Google and Stack Overflow

Placeholder


## Introduction
## Wait! Before you search the web...
## Googling
### Include "r" in your search!
### Include `tidyverse` or the package name in your search
### Exact matching
### Searching a specific site
### Date range
## What are Stack Overflow and Stack Exchange?
## Questions
## Next Steps

<!--chapter:end:009-operating_in_an-using_google_and_so.Rmd-->


# Stack Overflow

Placeholder


## Introduction
## Use Cases
## Tips for Asking & Searching
### Reproducible Examples
## Next Steps

<!--chapter:end:010-operating_in_an-stack_overflow.Rmd-->


# When your code doesn't work

Placeholder


## Introduction
## Avoiding (big) issues 
### Use common packages where possible
### Check results as you go
## Dealing with issues on your own
### Isolate the issue
### Check that you have the right packages loaded
### Check for typos
### Check the built-in help
## Escalating the issue
### Make a minimal example
### "General" Resources 
### Informal resources
## Still stuck?
### Ask: "do I have other options?"
### Remember to take a break!
## Exercises
## Next Steps

<!--chapter:end:011-operating_in_an-when_your_code_wont_work.Rmd-->


# Making Reproducible Examples

Placeholder


## Introduction
## Seeking help the helpful way
## Elements of a reprex
## Creating a data set for a reprex
## Adding code 
## Packages and any other relevant information
## A closer look at the reprex package
## Exercises
### Exercise 1
## Next Steps

<!--chapter:end:013-operating_in_an-reprex.Rmd-->


# How to make the most of R's cryptic error messages

Placeholder


## Decrypting the cryptic
### Shootin' the troubles
####  Package inputenc Error
##### Example 1
##### Example 2
#### It's one thing to get our code to *work*, but another thing to make sure we don't have to work our code.
## Knitting makes a great pastime
### Parm for your copypasta?
### Code
#### Note: A list of RStudio keyboard shortcuts can be found [here](https://support.rstudio.com/hc/en-us/articles/200711853-Keyboard-Shortcuts)
### Knitting's not for me
## Have you tried turning it off and on again?
### Time waits for no man
#### Note: Keep in mind that you have to install packages again *each time you start a new RStudio session on JupyterHub*.
### Getting back on track when we run
#### Example 4
#### Note: This can especially be an issue if we've used `set.seed()`. Forgetting to set a seed when creating simulations of random objects can drastically change our results!
#### Note: If there are any helper files left behind from a R Markdown document that couldn't knit, like `.aux`, delete them before trying to knit again.
## Clopening
## Warnings, not errors
### Example 5
##### Note: More information on chunk options can be found [here](https://rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf)
## Resources and references

<!--chapter:end:014-operating_in_an-making_the_most.Rmd-->





# (PART\*) Holding the chaos at bay {-}

# Introduction

*Written by Rohan Alexander.*

When you first learn how to code in R, it can feel like you're in a battle to just get something working, without regard for what it looks like. That fine initially, but as you start to use R in more involved settings that approach will become a bit chaotic. This will result in you having to do more work in the long run. 

In this module we cover how to hold back that chaos. While they will add a few minutes initially, the techniques that we cover here will save you time in the long run. Your analysis will be better and more professional, and it will be easier for you to build on the code base that you establish every time you code.

This is a somewhat bitty module. We've been fairly prescriptive here, but you should think of it more as a default to get you started, and you can move from this default as you think best. First we discuss R Projects, and then how to structure your folders. We then discuss writing comments, which makes your code more useful for other people (even if that person is just future-you). Then we cover installing and loading packages, which are collections of other people's code. Finally, we discuss loading data. 

We got the sharks out of the pool - feel free to jump in!

<iframe width="560" height="315" src="https://www.youtube.com/embed/vSuPz7VYG1c" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>




<!--chapter:end:015-holding_the_chaos_at_bay.Rmd-->


# R Projects and working directory

Placeholder


## Introduction
## The working directory
### Drawbacks of `setwd()`
## R Projects
### Creating and Opening R Projects
## Common Mistakes & Errors
## Exercises
## Key Takeaways & Next Steps

<!--chapter:end:016-holding_the_chaos_at_bay-rprojects_setwd.Rmd-->


# Folder set-up

Placeholder


## Introduction
### Folder Set-Up Motivation
## Folder Set-Up
### Data/Input Folder
### Figure/Plot Folder
### Results/Output Folder
### Code/Scripts Folder
### Other/Miscellaneous Folder (If Necessary)
## Key Takeaways
## Exercises
## Next Steps

<!--chapter:end:017-holding_the_chaos_at_bay-folder_setup.Rmd-->


# Writing comments

Placeholder


## Introduction
### What is a Comment?
## Comments
### Why Comment
### How to Comment
### When to Comment
## Preamble
## Exercises
## Key Takeaways

<!--chapter:end:018-holding_the_chaos_at_bay-comments.Rmd-->


# Installing packages

Placeholder


## Introduction
## What is a package?
## What is CRAN
## How to install?
## Using code
## In RStudio 
## Exercises
### Exercise 1
### Exercise 2
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:019-holding_the_chaos_at_bay-install_packages.Rmd-->


# Install from GitHub

Placeholder


## Introduction
## What is GitHub?
## Install packages from GitHub
## Example
## Exercises
### Exercise 1
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:020-holding_the_chaos_at_bay-install_github.Rmd-->


# Calling packages

Placeholder


## Introduction
## Arguments
## library()
## Overview
### Citing R 
## Video
## Exercises
### Exercise 1
### Exercise 2
### Exercise 3
### Exercise 4
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:021-holding_the_chaos_at_bay-library.Rmd-->


# Updating packages

Placeholder


## Introduction
## Arguments
## Overview 
## Exercises
### Exercise 1
### Exercise 2
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:022-holding_the_chaos_at_bay-update_packages.Rmd-->


# Read CSVs

Placeholder


## Introduction
## Delimited data files in R
## A closer look at `read_csv()`
## Arguments of `read_csv()`
## Exercises
### Exercise 1 
### Exercise 2
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:023-holding_the_chaos_at_bay-read_csv.Rmd-->


# Reading tables dta and other data types

Placeholder


## Introduction
## Tabular Data
## Non-Tabular Data
## Statistical Package Data (Using the Tidyverse `haven` Package)
## Overview and next steps

<!--chapter:end:024-holding_the_chaos_at_bay-read_table.Rmd-->




# (PART\*) Hand me my plyrs {-}


# Introduction

The `tidyverse` is a package that loads a whole bunch of other packages. These allow you to write R in a certain way, called 'tidy'. This is kind of like speaking a dialect of a spoken language. It's still the same language, but it's also different.

The key package within the `tidyverse` is called `dplyr`, which is pronounced 'dee-plier', hence the horrible pun in the title. We're going to cover a lot of different functions here, and it may be a bit overwhelming, but just try to apply them to something that you're interested in, be that [stochastic convergence rates](https://github.com/awstringer1/aghq), [baseball](https://www.hodgettsp.com/blog/baseball-a-defensive-critique/), or [DMC embroidery floss colour](https://sharlagelfand.github.io/dmc/).


<iframe width="560" height="315" src="https://www.youtube.com/embed/l15xQTf1m4A" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>










<!--chapter:end:025-hand_me_my_plyrs.Rmd-->


# What is the `tidyverse`?

Placeholder


## Introduction
## Core `tidyverse` packages
### `readr`
### `tibble`
### `tidyr`
### `dplyr` 
### `ggplot2`
### `purrr`  
### `stringr`  
### `forcats`
## References

<!--chapter:end:026-hand_me_my_plyrs-tidyverse.Rmd-->


# The pipe

Placeholder


## Introduction
## Overview
## Exercises
### Exercise 1
### Exercise 2
### Exercise 3
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:027-hand_me_my_plyrs-pipe.Rmd-->


# select

Placeholder


## Introduction
### What is `select()`?
### Prerequisite skills include  
### Basic setup
## Video
## Basics
## Operators 
## Advanced uses
## Exercises
### Question 1
### Question 2 
### Question 3
### Question 4
## Common Mistakes & Errors
## Next Steps & See also 
## Summary

<!--chapter:end:028-hand_me_my_plyrs-select.Rmd-->


# filter

Placeholder


## What is `dplyr::filter()` for?
## What arguments does `dplyr::filter()` take?
## What value does `dplyr::filter()` return?
## Practice 
## Coding Examples
## Exercises
## Additional Resources

<!--chapter:end:029-hand_me_my_plyrs-filter.Rmd-->


# group and ungroup

Placeholder


## Introduction
## The content
## Arguments
## Other Optional Arguments
## Questions
## Exercises
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:030-hand_me_my_plyrs-group_by.Rmd-->


# summarise

Placeholder


## Introduction
## Arguments
## Overview
### Question 1
### Question 2
### Question 3
### Question 4
## Exercises
### Exercise 1
### Exercise 2
### Exercise 3
### Exercise 4
### Exercise 5
### Exercise 6
### Exercise 7
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:031-hand_me_my_plyrs-summarise.Rmd-->


# arrange

Placeholder


## Introduction
## arrange()
## Additional Examples
### Characters
### Multiple Arguments
## Practice Questions
## Practice Coding
## Special Cases and Common Errors
### NA Values
### Common Errors
## Overview

<!--chapter:end:032-hand_me_my_plyrs-arrange.Rmd-->


# mutate

Placeholder


## Introduction
## Examples 
## Concept Maps 
## Common mistakes 
## Exercise
### Question 1 
### Question 2
### Question 3 
### Video Solution
## Next steps
### Other resources

<!--chapter:end:033-hand_me_my_plyrs-mutate.Rmd-->


# pivoting

Placeholder


## Introduction
## pivot_longer()
### Introductory Example
## Visualizing pivot_longer()
## pivot_longer() Arguments
## pivot_wider()
### Introductory Example
## Visualizing pivot_wider()
## pivot_wider() Arguments
## Other Optional Arguments
### pivot_longer()
### pivot_wider()
## Questions
## Exercises
### pivot_longer()
### pivot_wider()
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:034-hand_me_my_plyrs-pivotwider.Rmd-->


# rename

Placeholder


## Introduction
## Arguments
## Overview
## Exercises
### Exercise 1
### Exercise 2
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:035-hand_me_my_plyrs-rename.Rmd-->


# counting

Placeholder


## Introduction
## Video Tutorial
## count()
## Using count()
## count() Arguments
## uncount()
### Arguments
## Using uncount()
## Questions & Exercises
### Exercises
### Questions

<!--chapter:end:036-hand_me_my_plyrs-count_and_uncount.Rmd-->


# slice

Placeholder


## Introduction
## slice()
## Video Overview
## Selecting Rows
### Single Row
### Multiple Rows
### Omitting Rows
## Questions & Exercises
### Questions
### Exercises
## Common Mistakes
## Next Steps

<!--chapter:end:037-hand_me_my_plyrs-slice.Rmd-->


# data

Placeholder


## Introduction
## The content
## Vectors
### Examples
## Matrices
### Examples
## Data Frames
### Examples
## Tibbles
### Questions
## Exercises
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:038-hand_me_my_plyrs-c_matrix_dataframe_tibble.Rmd-->


# length, rows, columns and dimensions

Placeholder


## Introduction
## Arguments
### length()
### nrow() and ncol()
### dim()
### `dplyr::bind_rows()` and `dplyr::bind_cols()`
## Questions and Exercises
###  length()
### nrow() and ncol()
### dim()
## Special Cases & Common Mistakes
### length()
### nrow() and ncol()
## Overview and Next Steps

<!--chapter:end:039-hand_me_my_plyrs-length_nrow_ncol_dim.Rmd-->




# (PART\*) Totally addicted to base {-}

# Introduction

In this module, we are going to explore 'base R'. This means that we don't need to load any packages - we're working with functions that come 'out of the box', as it were. Base is a very stable collection of functions that have been refined over decades. This is in contrast to the `tidyverse`, which we introduced in earlier modules, which is much newer. Some folks are passionate about the differences between them, but they're just tools that we use as appropriate. In this module we are going to cover some base functions that you'll use again and again in your R journey, especially in statistics.

The statistical programming language R was original designed for statistics and so there is a whole lot of functionality built into base R that helps with statistics. For instance, there are great functions to calculate summary statistics, and to quickly plot data. Also in base are the types of foundational programming functions that most languages need, such as `for()`, `while()`, and, of course, the ability to define your own `function()`.

<iframe width="560" height="315" src="https://www.youtube.com/embed/PhljUEN996Y" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>




<!--chapter:end:041-totally_addicted_to_base.Rmd-->


# mean, median, sd, lm, and summary

Placeholder


## Introduction
## Arguments
### `mean()`
### `median()`
### `sd()`
### `summary()`
### `lm()`
## Overview
### summary()
### mean(), median(), and sd()
### lm()
### Example: Combining `mean()`, `median()`, and `lm()`
## Exercises
### Exercise 1
### Exercise 2
### Exercise 3
## Common mistakes & errors
## Next steps

<!--chapter:end:042-totally_addicted_to_base-mean_median_sd_lm_summary.Rmd-->




# glm

<!--chapter:end:043-totally_addicted_to_base-glm.Rmd-->




# lmer()

# Introduction

# lmer()

# Exercises

# Common Errors

<!--chapter:end:043-totally_addicted_to_base-lme4.Rmd-->


# function

Placeholder


## Introduction
## The content
### Why and when should you use it?
### Built-in functions 
### User defined functions
### default parameters
## Exercises
#### Exercise 1
#### Exercise 2
#### Exercise 3
#### Exercise 4
## Common mistakes & errors
## Next steps

<!--chapter:end:044-totally_addicted_to_base-function.Rmd-->


# for and while

Placeholder


## Introduction
### What are Loops?
### Packages
## `for()`
### Structure 
### Mutating a Dataset using `for()`
### Nested `for()` loops 
## `while()`
### Structure
### Example
## Differences between `for()` and `while()`
## Exercises
### Question 1 
### Question 2
### Question 3
## Common mistakes & errors
## Next steps
## References  

<!--chapter:end:045-totally_addicted_to_base-for_while.Rmd-->


# if, if else and case when

Placeholder


## Introduction
## `if()`
## Example
## `if_else()`
### Examples 
## `case_when()` function 
### Examples 
## Exercises
### Exercises 1 
### Exercises 2
### Exercises 3
## Common mistakes & errors
## Next steps

<!--chapter:end:046-totally_addicted_to_base-if_ifelse_casewhen.Rmd-->


# c, seq, seq along, and rep

Placeholder


## Introduction
## The content
## Arguments
## Other Optional Arguments
## Questions and Exercises
### `c()`
### `seq()`
### `seq_along()`
### `rep()`
## Common mistakes & errors
## Next steps

<!--chapter:end:047-totally_addicted_to_base-c_seq_seqalong_rep.Rmd-->


# hist, plot and boxplot

Placeholder


## Introduction
## Histogram: `hist()`
### Number of Bins
### Colour of the histogram
### Title and Axis
## Other base graphing options
### Scatterplot
### Boxplot
## exporting base graphs 
## Exercises
### Question 1
### Question 2
### Question 3
## Common mistakes & errors
### Overview and Next steps
## References  

<!--chapter:end:048-totally_addicted_to_base-hist_plot_boxplot.Rmd-->






# apply sapply lapply

<!--chapter:end:049-totally_addicted_to_base-apply_sapply_lapply.Rmd-->






# basename etc

<!--chapter:end:050-totally_addicted_to_base-basename_rm_fileexists_dircreate.Rmd-->






# sum round etc

<!--chapter:end:051-totally_addicted_to_base-sum_dim_round.Rmd-->






# isna which unique identical

<!--chapter:end:052-totally_addicted_to_base-isna_which_unique.Rmd-->






# rownames and colnames

<!--chapter:end:053-totally_addicted_to_base-rownames_colnames.Rmd-->






# floor ceiling round and abs

<!--chapter:end:054-totally_addicted_to_base-floor_ceiling_round_abs.Rmd-->


# (PART\*) He was a d8er boi {-}
# Introduction

Placeholder



<!--chapter:end:055-he_was_a_d8er_boi.Rmd-->


# head, tail, glimpse and summary

Placeholder


## Introduction
## `head()`
## `tail()`
## `glimpse()`
## `summary()`
## Exercises
### Exercise 1
### Exercise 3
## Next Steps

<!--chapter:end:056-he_was_a_d8er_boi-head_tail_glimpse_summary.Rmd-->


# paste, paste0, glue and stringr

Placeholder


## Introduction  
## Paste strings and data with `paste()` and `paste0()`
## "Gluing" your data with the `glue` package
### The functions of `glue`
## First taste of the `stringr` package
## Exercises
### Exercise 1
### Exercise 2
### Exercise 3 
### Exercise 4
## Next Steps

<!--chapter:end:057-he_was_a_d8er_boi-paste_glue_stringr.Rmd-->


# names, rbind and cbind

Placeholder


## Introduction
## Arguments
### `names()`
### `rbind()`
### `cbind()`
## Questions and Exercises
### Question 1
### Question 2
## Special Cases & Common Mistakes
## Overview & Next Steps

<!--chapter:end:058-he_was_a_d8er_boi-names_rbind_cbind.Rmd-->


# Joins

Placeholder


## Introduction
## `left_join()`
## `right_join()`
## `full_join()`
## `inner_join()`
## `anti_join()`
## Exercises
### Exercises 1
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:059-he_was_a_d8er_boi-leftjoin_antijoin_fulljoin.Rmd-->


# Looking for missing data

Placeholder


## Introduction
## Overview
### Example
## Video
## Arguments
## complete()
## fill()
## Exercises
### Exercise 1
### Exercise 2
## Next Steps

<!--chapter:end:061-he_was_a_d8er_boi-missing_data.Rmd-->


# setseed, runif, rnorm, and sample

Placeholder


## Introduction
## The content
### runif()
#### Arguments
#### Example
### rnorm()
#### Arguments
#### Example
### sample()
#### Arguments
#### Examples
### set.seed()
#### Arguments
#### Example
## Exercises
### Exercise 1
### Exercise 2
### Exercise 3
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:062-he_was_a_d8er_boi-setseed_runif_sample.Rmd-->


# Simulating datasets for regression

Placeholder


## Introduction
## Overview
## Idea
## Example
## Exercises
### Exercise 1
### Exercise 2
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:063-he_was_a_d8er_boi-simulating_datasets_for_regression.Rmd-->


# Conditional mutating and summarising

Placeholder


## Introduction
## Overview
### Video
## Questions
### Question 1
### Question 2
### Question 3
## Arguments
### `across()`
### `mutate_if()`
### `na_if()`
## Exercises
### Exercise 1
### Exercise 2
### Exercise 3
## Next Steps

<!--chapter:end:064-he_was_a_d8er_boi-conditional_mutate_and_summarise.Rmd-->


# Tidying up datasets

Placeholder


## Introduction
## Video
## Arguments
### recode()
### replace_na()
### coalesce()
### n_distinct()
### distinct()
### drop_na()
### lag(), lead()
## Exercise
## Next Steps

<!--chapter:end:065-he_was_a_d8er_boi-tidying_up_datasets.Rmd-->


# pull, pluck and unnest

Placeholder


## Introduction
## pull()
### Examples
## pluck()
### Examples
## `unnest()`
### Examples
## Practice questions
## Practice coding
## Overview and Next Steps

<!--chapter:end:066-he_was_a_d8er_boi-pull_pluck_unnest.Rmd-->


# forcats and factors

Placeholder


## Introduction
## The Content
## Factors
## Forcats
### `fct_count`
### `fct_c` 
### `fct_lump` functions
### `fct_reorder` 
### `fct_relevel`
## Exercises
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:067-he_was_a_d8er_boi-forcats_and_factors.Rmd-->


# More on strings

Placeholder


## Introduction
## Separate text-based data frames using separate() and separate_rows()
## Trouble Shooting separate()
## Working with text data using str_match() and str_remove()
## Questions
## Exercises
### Exercise 1
### Exercise 3
### Exercise 2
## Next Steps

<!--chapter:end:068-he_was_a_d8er_boi-more_on_strings.Rmd-->


# Working with dates

Placeholder


## Introduction
## Overview
### Example
## Exercises
### Exercise 1
### Exercise 2
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:069-he_was_a_d8er_boi-dates.Rmd-->


# Regular expressions

Placeholder


## Starting with the basics
## Wrapping our package
## Insensitive about cases
## Period.
## From start to finish
## Or how about...
## Color or colour?
## Building character
## Help me escape!
## Functioning functions
## Additional resources and references

<!--chapter:end:069-he_was_a_d8er_boi-regular_expressions.Rmd-->


# janitor

Placeholder


## Introduction
## Overview
## Arguments
## `clean_names()`
## `get_dupes()`
## Exercises
### Exercise 1
### Exercise 2
### Exercise 3
### Exercise 4
## Next Steps

<!--chapter:end:070-he_was_a_d8er_boi-janitor.Rmd-->


# `tidyr` package

Placeholder


## Introduction
## Overview
## Example 
## Exercises
### Exercise 1
## Next Steps

<!--chapter:end:071-he_was_a_d8er_boi-tidyr.Rmd-->




# (PART\*) To ggplot or not to ggplot {-}


# Introduction

I hope that this module will make you love plotting your data. When you're using data, there's almost nothing more important than just showing the data that you're interested in. The `ggplot2` package has become the go-to for graphing in R.

It's a powerful and versatile tool and I think that you're going to love learning about it.



<!--chapter:end:072-to_ggplot_or_not_to_ggplot.Rmd-->


# Overview of ggplot2

Placeholder


## Introduction to `ggplot()` through the scatterplot
### What is a scatterplot?
### Let's look at an example of a scatterplot
## Using `ggplot()`
### What is `ggplot()` for?
### What arguments does `ggplot()` take?
### What are aesthetics?
#### Exercise 1
### What else do we need to use `ggplot()` ? **Layers**
#### Geoms
#### Example 1 - the `+`
#### Themes 
## Handy Layers
#### Labels
#### Adjusting title positions using the **theme** layer
##### To the left, to the left...
##### Writing to the right-ing
#### Axis scale limits
#### Axis text angle
## Additional Resources and References

<!--chapter:end:073-to_ggplot_or_not_to_ggplot-overview.Rmd-->


# Bar charts

Placeholder


## Introduction
## The content
## Arguments
## Other Optional Arguments
## Questions
### Optional Arguments
### Adding labels to your bar charts
### Plotting numeric variables
### Rotating your bar chart
## Exercises
### Plot a Simple Bar Chart
### Making your bar chart a little more interesting
### Using the `aes()` fill option
### Check your understanding
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:074-to_ggplot_or_not_to_ggplot-barcharts.Rmd-->


# Histograms

Placeholder


## Introduction
## Making and customizing histograms
### What is a histogram?
### Other Optional Arguments
#### Bin size
#### Color and fill
#### Title, and name of the axes
## Exercises
### Exercise 1
### Exercise 2
### Exercise 3
### Exercise 4
### Video Solutions
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:075-to_ggplot_or_not_to_ggplot-histograms.Rmd-->


# Scatter plots

Placeholder


## Introduction
## The content
## What is a Scatter plot?
## Arguments
### Basic scatter plot
## Change the appearance of the point
## Scatter plots with multiple groups
## Exercises
## Exercise 1 
## Exercise 2
## Exercise 3
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:076-to_ggplot_or_not_to_ggplot-scatterplots.Rmd-->


# Various useful options

Placeholder


## Introduction
### Packages  
## Faceting
### `facet_grid()`
#### Arguments 
### `facet_wrap()`
#### Arguments
### `facet_grid()` vs `facet_wrap()`
## Labelling ggplot
### Arguments for `labs()`
### Labeling without using `labs()`  
## How to change colors of ggplot
### Change to a single color
### Change color by groups
### basic theme changing
## `pretty_breaks()` or `breaks_pretty()` 
## Exercises
### Question 1
### Question 2
### Question 3
## Next Steps
## References  

<!--chapter:end:077-to_ggplot_or_not_to_ggplot-various_options.Rmd-->


# Saving graphs

Placeholder


## Introduction
## Saving Graphs 
### Save as Jpeg image
### Save as png image
### Save as pdf file
### Delete the saved image/file
### `ggsave()`
## Exercises
### Question 1
### Question 2
### Question 3
## Next Steps
### Common Mistakes & Errors
### Next Steps
## References  

<!--chapter:end:078-to_ggplot_or_not_to_ggplot-saving_graphs.Rmd-->




# gganimate

<!--chapter:end:079-to_ggplot_or_not_to_ggplot-gganimate.Rmd-->




# Some other geom

<!--chapter:end:080-to_ggplot_or_not_to_ggplot-some_other_geom.Rmd-->




# some geom

<!--chapter:end:081-to_ggplot_or_not_to_ggplot-some_other_other_geom.Rmd-->




# (PART\*) R Marky Markdown and the Funky Docs {-}

# Introduction

*Written by Rohan Alexander.*

In this module, we are going to go through R Markdown. 

R Markdown is an incredibly powerful way of combining text and code, and you can produce html, pdf, word and many other outputs. Most of us learn it as a great way to write class assignments, but these days it's used for everything from making textbooks, websites, and is even the foundation on which these tutorials are based.





<!--chapter:end:082-r_marky_markdown.Rmd-->


# Introduction to R Markdown

Placeholder


## Introduction
### Why use R Markdown?
## Creating a R Markdown file
### YAML Header Chunk
## Markdown
### Sections
### Paragraphs
#### Note
### Bold Text
### Italicized Text
### Superscript
### Subscript
### Lists
### Sublists
### Ordered lists
### Hyperlinks
### Images
### Hyperlinked images
### Escapes
## Math environments
### Delimiters
#### Inline
#### Centred Display
#### Aligned
### Superscript
#### Note: Remember to use the curly brackets! 
### Subscript
### Math escapes: brackets and dolla dolla bill \$ignz
#### Exceptions? 
### Other syntax
#### Note: For the rest of the *Math environments* section, we will be making use of the inline delimiters `\( \)` **unless** otherwise specified.
#### Fractions:
#### Binomials:
#### Integrals
##### Indefinite
##### Definite
#### Sums 
#### Limits
#### Note: More resources on LaTeX math syntax can be found in the *Resources and references* section :\^)
### Spaces
## Code
### Displaying
#### Inline
#### Blocks
##### Readability
### Running
### Chunk options
## Resources and references
### Introductory
#### From RStudio
#### From other sources
### LaTeX 

<!--chapter:end:083-r_marky_markdown-introduction.Rmd-->


# Top Matter: Title, Date, Author, Abstract

Placeholder


## Introduction
## Title, Date, Author
## Abstract
## Exercises
### Question 1 
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:085-r_marky_markdown-top_matter.Rmd-->


# Tables: kable, kableextra, and gt

Placeholder


## Introduction
### Packages  
## Kable()
### Arguments of `kable()`
### Formatting of `kable`  
## `kableExtra`
### `kable_styling()`  
### How to put multiple tables side by side
## GT Table
### Add parts to the gt Table
## Exercises
### Question 1
### Question 2
### Question 3
## Common Mistakes & Errors  
## Next Steps
## Reference  

<!--chapter:end:086-r_marky_markdown-tables.Rmd-->


# Multiple plots with `patchwork`

Placeholder


## Introduction
## What is `patchwork`?
## Getting started
## More complicated layouts
## Customization and annotation
## Exercises
### Exercise 1
### Exercise 2 
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:088-r_marky_markdown-patchwork.Rmd-->


# References and Bibtex

Placeholder


## Introduction
## Bibliographies
### BIB file? 
### Placement
### Citing R packages using `citation()` function
## Reference

<!--chapter:end:089-r_marky_markdown-references.Rmd-->


# PDF outputs

Placeholder


## Introduction
## PDF outputs
## Exercises
### Question 1
### Question 2
## Next Steps

<!--chapter:end:090-r_marky_markdown-pdfs.Rmd-->


# here and filepaths

Placeholder


## Introduction
## The content
### Filepaths
### Here
## Arguments
## Examples
## Exercises
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:091-r_marky_markdown-here.Rmd-->


# (PART\*) Git outta here {-}
# Introduction

Placeholder



<!--chapter:end:092-git_outta_here.Rmd-->


# What is version control and GitHub?

Placeholder


## Introduction
## Overview
### Visualizing Git
## Next Steps

<!--chapter:end:093-git_outta_here-what_is_version_control.Rmd-->


# Git: pull, status, add, commit, push

Placeholder


## Introduction
## Overview
## Videos
## Exercises
### Exercise 1
### Exercise 2
### Exercise 3
### Exercise 4
### Exercise 5
### Exercise 6
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:094-git_outta_here-pull_push.Rmd-->


# Branches in GitHub

Placeholder


## Introduction
## The content
### About Branches
### How to Create a Branch
### How to make a pull request
### Forks
### Updating a Branched (or Forked) Repo
## Questions
## Exercises
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:095-git_outta_here-branches.Rmd-->


# Dealing with conflicts

Placeholder


## Introduction
## The content
### Conflicts from Pushing before Pulling
### Conflicts from Having an Issue with a Pull Request
### Solving Conflicts
## Questions
## Exercises
## Next Steps

<!--chapter:end:096-git_outta_here-conflict.Rmd-->


# Putting (G)it All together in RStudio

Placeholder


## Introduction
## Bringing the Repo into R
## Explaining the buttons/commands
### Making an R project into a GitHub repo
## Live Demonstration 
## Test Your Understanding
## Common Mistakes and Errors
## Next Steps

<!--chapter:end:097-git_outta_here-git_in_rstudio.Rmd-->






# Projects issues

<!--chapter:end:098-git_outta_here-projects_issues_comments.Rmd-->






# (PART\*) Indistinguishable from magic {-}

# Introduction

*Written by Rohan Alexander.*

In this module, we are going to go through various aspects that are, and there's no word for this other than, magical. We learn R because we're forced to for a class or work, or because we have some problem that a 'friend' says we should solve in R. Eventually we get better at it, but it's a slog. But when you get to this module, we start to see the power of the foundation that we've established.

We will be able to make websites using R! We will be able to make interactive applications using R. After using countless packages throughout these modules, we'll even be able to write out own packages! There are also a few aspects around style that are worth addressing at this point, and so there is also a lesson on that. 

For me, it was when I got to this type of content, that I started to really 'get' R. And I hope that you feel similarly.



<!--chapter:end:099-indistinguishable_from_magic-.Rmd-->






# Iteration

<!--chapter:end:100-indistinguishable_from_magic-iteration.Rmd-->


# Coding style

Placeholder


## Naming things: the tidy way
### Naming files 
### Naming objects
## Tidying up your "syntax"
### Commas and spaces
### Curly braces and code hierarchies
### Few other notes on syntax
## Exercises
## Next Steps

<!--chapter:end:101-indistinguishable_from_magic-coding_style.Rmd-->


# Static maps using ggmap

Placeholder


## Introduction
## Package
## Backgrounds
## Plotting Data
## Exercises
### Exercise 1
### Exercise 2
### Exercise 3
## Google Maps APIs
## Next Steps

<!--chapter:end:102-indistinguishable_from_magic-static_maps.Rmd-->


# Writing R Packages

Placeholder


## Introduction
## Steps for Making a Package in R
## Each Section of Packages in depth
### After you have filled out each file
### Sharing Your Package
## Live Coding
## Exercises
## Next Steps

<!--chapter:end:103-indistinguishable_from_magic-packages.Rmd-->




# Writing R Packages II

<!--chapter:end:104-indistinguishable_from_magic-packages_ii.Rmd-->


# Getting started with Blogdown

Placeholder


## Introduction
## Set Up
## Creating a new site
## Initial Configurations and File Structure
## Making your website public
### GitHub
### Netlify
## Next Steps

<!--chapter:end:105-indistinguishable_from_magic-blogdown.Rmd-->




# postcards

<!--chapter:end:106-indistinguishable_from_magic-distill_postcards.Rmd-->


# Getting started with Shiny

Placeholder


## About
## The Parts
## Making the App
## Arguments
## Live Coding
## After you code your app
## Testing Your Understanding
## Common Mistakes & Errors
## Next Steps

<!--chapter:end:107-indistinguishable_from_magic-shiny.Rmd-->




# Writing a CV

<!--chapter:end:108-indistinguishable_from_magic-cv.Rmd-->




# tidymodels


<!--chapter:end:109-indistinguishable_from_magic-tidymodels.Rmd-->




# leaflet

<!--chapter:end:110-indistinguishable_from_magic-leaflet.Rmd-->




# diagrammer

<!--chapter:end:111-indistinguishable_from_magic-diagrammer.Rmd-->




# (PART\*) Specialised topics {-}

# Overview

<!--chapter:end:112-specialised_topics-overview.Rmd-->




# Stan

<!--chapter:end:113-specialised_topics-stan.Rmd-->




# devtools


<!--chapter:end:114-specialised_topics-devtools.Rmd-->




# usethis

<!--chapter:end:115-specialised_topics-usethis.Rmd-->




# testthat

<!--chapter:end:116-specialised_topics-testthat.Rmd-->




# Tidytext and NLP


<!--chapter:end:117-specialised_topics-tidytext_and_nlp.Rmd-->




# OOP

<!--chapter:end:118-specialised_topics-oop.Rmd-->




# Functional programming

<!--chapter:end:119-specialised_topics-functional_programming.Rmd-->




# SQL


<!--chapter:end:120-specialised_topics-sql_and_r.Rmd-->




# Python


<!--chapter:end:121-specialised_topics-python_and_r.Rmd-->




# C++

<!--chapter:end:122-specialised_topics-c_and_r.Rmd-->

