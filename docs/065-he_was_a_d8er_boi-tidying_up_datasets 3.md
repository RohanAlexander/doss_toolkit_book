


# Tidying up datasets

*Written by Mariam Walaa and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- Use recode()
- Use coalesce()
- Use lag() and lead()
- Use replace_na(), drop_na()
- Use n_distinct(), distinct()

Prerequisite skills include:

- Familiarity with NA values
- Familiarity with data types 

Highlights:

- Use **replace_na()** and **drop_na()** to work with NA values
- Use **n_distinct()** and **distinct()** to look at unique rows
- Use **lag()** and **lead()** to push a set of values forward or backward in a vector
- Use **coalesce()** to look at the first occurrence of a non-NA value across vectors
- Use **recode()** to change certain values to something else that is of the same data type

## Video

![](https://youtu.be/0lz5kRNbQso)

## Arguments

### recode()

The `recode()` function takes the following as arguments:

| Argument | Parameter | Details                                                                       |
| -------- | --------- | ----------------------------------------------------------------------------- |
| .x       | vector    | the vector you want to modify                                                 |
| ...      | old value | old value = new value; assign a new value to the old value you want to modify |

You can read more about the arguments in the `recode()` functions documentation
[here](https://dplyr.tidyverse.org/reference/recode.html).

### replace_na()

The `replace_na()` function takes the following as arguments:

| Argument | Parameter        | Details                                                  |
| -------- | ---------------- | -------------------------------------------------------- |
| data     | input data frame | data frame with columns we want to replace NAs for       |
| replace  | list             | list of values for each column to replace their NAs with |

You can read more about the arguments in the `replace_na()` functions documentation
[here](https://tidyr.tidyverse.org/reference/replace_na.html).

### coalesce()

The `coalesce()` function takes the following as arguments:

| Argument | Parameter      | Details                                                           |
| -------- | -------------- | ----------------------------------------------------------------- |
| …        | set of vectors | set of vectors to extract series of first non-empty elements from |

You can read more about the arguments in the `coalesce()` functions documentation
[here](https://dplyr.tidyverse.org/reference/coalesce.html).

### n_distinct()

The `n_distinct()` function takes the following as arguments:

| Argument | Parameter      | Details                                                 |
| -------- | -------------- | ------------------------------------------------------- |
| …        | set of vectors | set of vectors to count number of distinct elements for |

You can read more about the arguments in the `n_distinct()` functions documentation
[here](https://www.rdocumentation.org/packages/dplyr/versions/0.7.8/topics/n_distinct).

### distinct()

The `distinct()` function takes the following as arguments:

| Argument | Parameter | Details                            |
| -------- | --------- | ---------------------------------- |
| .data    | tibble    | tibble to return distinct rows for |

You can read more about the arguments in the `distinct()` functions documentation
[here](https://www.rdocumentation.org/packages/dplyr/versions/0.7.8/topics/distinct).

### drop_na()

The `drop_na()` function takes the following as arguments:

| Argument | Parameter        | Details                                                    |
| -------- | ---------------- | ---------------------------------------------------------- |
| data     | input data frame | data frame with columns we want to drop rows with NAs for  |
| …        | vector           | columns you want to drop observations for if they have NAs |

You can read more about the arguments in the `drop_na()` functions documentation
[here](https://www.rdocumentation.org/packages/tidyr/versions/0.8.0/topics/drop_na).

### lag(), lead()

The `lag()` and `lead()` functions take the following as arguments:

| Argument | Parameter | Details                                                 |
| -------- | --------- | ------------------------------------------------------- |
| x        | vector    | vector of values to work with                           |
| n        | number    | number of positions to lead or lag by                   |
| default  | number    | value to fill the empty spots with                      |

You can read more about the arguments in the function documentation
[here](https://dplyr.tidyverse.org/reference/lead-lag.html).

## Exercise

Match each of the function names to their descriptions.

| Function      | Description                                                                                            |
| ------------- | ------------------------------------------------------------------------------------------------------ |
| A             | This function pulls a vector backward by n positions and fills with NAs.                               |
| B             | This function provides all the distinct values in a vector.                                            |
| C             | This function replaces NA values with a specified value.                                               |
| D             | This function counts the number of distinct values in a vector.                                        |
| E             | This function pushes a vector forward by n positions and fills with NAs.                               |
| F             | This function returns the first non-NA value at each row of a set of data.                             |
| G             | This function takes out all the rows that include NA values.                                           |
| H             | This function allows you to change values of certain categories into new values of the same data type. |


<!-- ```{r matching, echo = FALSE} -->
<!-- quiz(question("Which function is A?", -->
<!--               answer("coalesce()"), -->
<!--               answer("lag()"), -->
<!--               answer("recode()"), -->
<!--               answer("lead()", correct = TRUE), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("Which function is B?", -->
<!--               answer("coalesce()"), -->
<!--               answer("drop_na()"), -->
<!--               answer("n_distinct()"), -->
<!--               answer("distinct()", correct = TRUE), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("Which function is C?", -->
<!--               answer("drop_na()"), -->
<!--               answer("replace_na()", correct = TRUE), -->
<!--               answer("distinct()"), -->
<!--               answer("n_distinct()"), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("Which function is D?", -->
<!--               answer("n_distinct()", correct = TRUE), -->
<!--               answer("distinct()"), -->
<!--               answer("recode()"), -->
<!--               answer("coalesce()"), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("Which function is E?", -->
<!--               answer("coalesce()"), -->
<!--               answer("lead()"), -->
<!--               answer("recode()"), -->
<!--               answer("lag()", correct = TRUE), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("Which function is F?", -->
<!--               answer("coalesce()", correct = TRUE), -->
<!--               answer("lead()"), -->
<!--               answer("recode()"), -->
<!--               answer("lag()"), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("Which function is G?", -->
<!--               answer("replace_na()"), -->
<!--               answer("lag()"), -->
<!--               answer("drop_na()", correct = TRUE), -->
<!--               answer("lead()"), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("Which function is H?", -->
<!--               answer("coalesce()"), -->
<!--               answer("lag()"), -->
<!--               answer("recode()", correct = TRUE), -->
<!--               answer("distinct()"), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE)) -->
<!-- ``` -->

## Next Steps

If you are looking for more information on some of these functions, please check out the
following resources:

- [dplyr: Compute lagged or leading
values](https://dplyr.tidyverse.org/reference/lead-lag.html) - [dplyr: Recode
values](https://dplyr.tidyverse.org/reference/recode.html) - [tidyr: Replace NAs with
specified values](https://tidyr.tidyverse.org/reference/replace_na.html) - [dplyr: Find
first non-missing element](https://dplyr.tidyverse.org/reference/coalesce.html) -
[n_distinct: Efficiently count the number of unique values in a set of
vector](https://www.rdocumentation.org/packages/dplyr/versions/0.7.8/topics/n_distinct) -
[distinct: Select distinct/unique
rows](https://www.rdocumentation.org/packages/dplyr/versions/0.7.8/topics/distinct) -
[drop_na: Drop rows containing missing
values](https://www.rdocumentation.org/packages/tidyr/versions/0.8.0/topics/drop_na)



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
