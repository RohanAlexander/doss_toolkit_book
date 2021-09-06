



# Using Google and Stack Overflow

Written by Michael Chong.

## Introduction

In this lesson, you will learn how to:

- search the web for help

Prerequisite skills include:

- knowing how Web searches fit into the troubleshooting process

Highlights:

- the date on web resources is very important!
- you can modify your Google search to give exact matches, specific date ranges, and specific websites
- Stack Overflow and Stack Exchange are a great place to look, but see how the 

## Wait! Before you search the web...

Did you try other, more reliable resources first? Answers you find "in the wild" might be out of date, or not be the best way to accomplish your task. 

Look to the **When your code doesn't work** lesson on the left on where to look before you look on the Internet. In short, you might want to try:

1. the function's help document (`?function_name`)
2. looking in this toolkit
3. [*R for Data Science* by Hadley Wickham](https://r4ds.had.co.nz/)

## Googling

Googling (or searching with another search engine) is a key part of programming! The Internet collectively knows more about using R than any single person or resource. You just need to know how to search efficiently and effectively, and be careful with what solutions you use! Not every solution is reliable.

You probably know how to use a search engine like Google or Bing. This subsection will teach you some tips (in Google) to narrow your search to get more relevant results.

### Include "r" in your search!

Make sure you're not getting other programming languages or software in your search. For example, search:

```
how to import data in R
```
instead of: 
```
how to import data
```

### Include `tidyverse` or the package name in your search

Because there are so many R packages, there are often several ways to do the same thing. We're usually going to try using a `tidyverse` implementation to complete our tasks. So, for example, if we want to learn to "combine strings in R", try:

```
combining strings in R tidyverse
```
instead of:
```
combining strings in R
```

The second search will bring up valid ways to combine strings, but usually with older syntax which may not be as fast, may not be compatible with newer functions, or with clunkier syntax that requires more memorization.

### Exact matching

Google results include things that are related to your search, but may not contain *exactly* what you're looking for. This can be frustrating if you're looking for something specific. Use quotation marks `""` to force exact matching. Then, the returned search results will include the phrase that you've quoted.

For example, if you're looking for help on `left_join()` 


### Searching a specific site

If you want results from a specific website (e.g. StackExchange/StackOverflow) then you can use the `site:` modifier with your search. For example, if you want to search for how to deal with `dates` in the R for Data Science textbook, one way to do it is:

```
dates site:r4ds.had.co.nz
```

### Date range

The R community moves fast! The `tidyverse` evolves quickly and is relatively new, so older results might no longer be relevant, or there might be better ways to do what you want to do.

Personally, I would be a bit suspicious of results before approximately 2014(ish) if the solution seems more difficult than what you expect. Of course, this varies from case to case, but it's something to keep in mind when you're browsing!

To narrow the date range on a Google search, use the "Tools" button:

<img src="images/07_google-tools.png" width="90%" />

then choose your date range:

<img src="images/07_google-dates.png" width="40%" />


## What are Stack Overflow and Stack Exchange?

These are online Q&A communities focused around programming or other domain-specific knowledge. Chances are that, for most common problems, someone has asked about it on Stack Exchange!

Some things to pay attention to in the answer:

<img src="images/07_stack-screenshot.png" width="90%" />

1. **Answer score** (left side). Users can "upvote" or "downvote" responses to the question. Higher scores generally mean better answers. 

2. **Answer accepted** (indicated by green checkmark). The person who asked the question can mark a specific answer indicating that this solved their problem. This might not be the same as the answer with the highest score!

3. **Date and time** (after each post and comment). The date is **very important!** How people use R has changed dramatically over the past several years, and so there are often newer, better ways to do things. As a loose rule of thumb, I would consider solutions before 2014 as probably out of date. The solution still might work, but there may be an easier way to do it now. 

4. **Comments** (following post). This is a good place to look for potential issues with the answer, or how to extend it to a related use case.

5. **Author reputation** (bottom right corner of answer). As users ask and answer more questions, they accumulate reputation from people voting on their answers. You can loosely think of people with higher scores being more trustworthy. 


## Questions

<!-- ```{r 07q1, exercise = FALSE, echo = FALSE} -->
<!-- question( -->
<!--   "Who can contribute solutions on Stack Exchange and Stack Overflow?", -->
<!--   answer("anyone who makes an account.", correct = TRUE), -->
<!--   answer("only certified programming experts and instructors"), -->
<!--   answer("primarily Internet trolls and inexperienced users"), -->
<!--   correct = "Correct! These are used by a wide range of people -- it can be a great resource, but be careful!", -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->


<!-- ```{r 07q2, exercise = FALSE, echo = FALSE} -->
<!-- question( -->
<!--   "Scenario: You've found two ways to do the same task. An answer from 2008, and an answer from 2018. They use different packages and functions. Which one should you use? ", -->
<!--   answer("Old solutions are usually just as good as new solutions. Newer packages are usually unreliable."), -->
<!--   answer("It's usually preferable to look for new(ish) solutions, since R packages are improved on frequently.", correct = TRUE), -->
<!--   answer("Newer solutions are better if I'm doing something advanced, but for simple tasks it doesn't matter."), -->
<!--   correct = "Since R is evolving so quickly, it's safer to go with newer resources if everything else is comparable. If you're trying something you haven't seen before, try to pick the package(s) that are better documented.", -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

## Next Steps

* If you're troubleshooting, consider where would be most appropriate to look for help for your problem. A quick Google search rarely hurts, as long as you stay critical about what the information that's out there.
* Continue with the lessons in this section to learn how to ask for help effectively!










