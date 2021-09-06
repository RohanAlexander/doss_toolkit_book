



# Looking for missing data

*Written by Mariam Walaa.*


## Introduction

In this lesson, you will learn how to:

- Find implicit missing data

Prerequisite skills include:

- Using the pipe operator %>%

Highlights:

- Use complete() and fill() to find implicit missing data

## Overview

When we think of looking for missing data, we may think of looking for missing values, 
but there is also another type of missing data that is implicit which we can look for.
For example, are there missing variables or observations in the data? We can answer this
question by looking at combinations of values and seeing if all the possible combinations
exist.

### Example

Suppose we have a data set representing student grades for a collection of required first
year courses for the statistics major: STA130, CSC108, MAT137, at the end of their first
year. However, some students have not finished all three courses and may be taking some in
the summer.

Lets start by loading the tidyverse.


```r
library(tidyverse)
```

Here is our hypothetical data of courses and grades.




```r
first_year
#> # A tibble: 12 × 3
#>    student_id course grade
#>         <dbl> <chr>  <dbl>
#>  1          1 STA130    84
#>  2          1 CSC108    79
#>  3          1 MAT137    83
#>  4          2 STA130    70
#>  5          2 CSC108    80
#>  6          3 STA130    82
#>  7          4 STA130    75
#>  8          4 CSC108    77
#>  9          4 MAT137    80
#> 10          5 STA130    80
#> 11          5 MAT137    81
#> 12          6 MAT137    79
```

As you can see, our data is missing some rows that would correspond to courses that 
students have yet to complete. Suppose, for some reason, that you want to count the number 
of courses that are left for all students to take until they have completed all their 
requirements, or maybe you want to try predicting the grades a student will get on their 
remaining courses. Regardless, you will need to "manipulate" this data set to make it so 
that you can see which courses students have yet to complete. The `complete()` function is 
right tool to do this and we can do this as follows.



<pre><code class='language-r'><code>first_year %>%<br>&nbsp;&nbsp;<span style='color:hotpink'>complete</span>(student_id, course)<br>#> # A tibble: 18 × 3<br>#> &nbsp;&nbsp;&nbsp;student_id course grade<br>#> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<dbl> <chr> &nbsp;<dbl><br>#> &nbsp;1 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1 CSC108 &nbsp;&nbsp;&nbsp;79<br>#> &nbsp;2 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1 MAT137 &nbsp;&nbsp;&nbsp;83<br>#> &nbsp;3 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1 STA130 &nbsp;&nbsp;&nbsp;84<br>#> &nbsp;4 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2 CSC108 &nbsp;&nbsp;&nbsp;80<br>#> &nbsp;5 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2 MAT137 &nbsp;&nbsp;&nbsp;NA<br>#> &nbsp;6 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2 STA130 &nbsp;&nbsp;&nbsp;70<br>#> &nbsp;7 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3 CSC108 &nbsp;&nbsp;&nbsp;NA<br>#> &nbsp;8 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3 MAT137 &nbsp;&nbsp;&nbsp;NA<br>#> &nbsp;9 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3 STA130 &nbsp;&nbsp;&nbsp;82<br>#> 10 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;4 CSC108 &nbsp;&nbsp;&nbsp;77<br>#> 11 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;4 MAT137 &nbsp;&nbsp;&nbsp;80<br>#> 12 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;4 STA130 &nbsp;&nbsp;&nbsp;75<br>#> 13 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5 CSC108 &nbsp;&nbsp;&nbsp;NA<br>#> 14 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5 MAT137 &nbsp;&nbsp;&nbsp;81<br>#> 15 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5 STA130 &nbsp;&nbsp;&nbsp;80<br>#> 16 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;6 CSC108 &nbsp;&nbsp;&nbsp;NA<br>#> 17 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;6 MAT137 &nbsp;&nbsp;&nbsp;79<br>#> 18 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;6 STA130 &nbsp;&nbsp;&nbsp;NA</code></code></pre>

This function gives us rows that represent courses students still haven't completed,
which we don't have their grades for.

## Video

![](https://youtu.be/1zowsiffKHg)

## Arguments

## complete()

The `complete()` function takes the following as arguments:

| Argument | Parameter        | Details                                           |
| -------- | ---------------- | ------------------------------------------------- |
| data     | input data frame | data whose columns we'll use to find missing data |
| …        | vector           | columns to find and complete all combinations for |
| fill     | named list       | values to fill the cells for newly added rows     |

You can read more about the arguments in the `complete()` function reference
[here](https://tidyr.tidyverse.org/reference/complete.html) or with `?complete`.

## fill()

The `fill()` function takes the following as arguments:

| Argument   | Parameter        | Details                                               |
| ---------- | ---------------- | ----------------------------------------------------- |
| data       | input data frame | dataframe whose columns we use to fill missing data   |
| …          | vector           | columns to find and complete all combinations for     |
| .direction | string           | 'up', 'down', 'downup' for direction to fill values   |

You can read more about the arguments in the `fill()` function reference
[here](https://tidyr.tidyverse.org/reference/fill.html) or with `?fill`.

## Exercises

There are many ways to fill the data we got above. If, for some reason, we wanted to fill
it based on the past or the next value, we can use the fill() function. If, however, we 
wanted to fill all the empty values with a specific number, we could use the fill 
parameter within the complete() function.

### Exercise 1

Referencing the Arguments section, try to fill it based on the _past_ value using the
fill() function.






### Exercise 2

Referencing the Arguments section, try to fill all the empty values with a specific number
0 and using the fill parameter within the complete() function.






## Next Steps

If you would like to learn more about the complete() and fill() functions, you will find
these resources from tidyr very helpful:

- [tidyr: Complete a data frame with missing combinations of data](https://tidyr.tidyverse.org/reference/complete.html)
- [tidyr: Fill in missing values with previous or next
value](https://tidyr.tidyverse.org/reference/fill.html)













