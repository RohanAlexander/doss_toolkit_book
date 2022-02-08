


# More on strings

*Written by Annie Collins and last updated on 7 October 2021.*

## Introduction

In this lesson, we will be covering some additional functions that will help us work with text data. If you have not already done so, please feel free to look through the previous lesson "58: paste, paste0, glue and stringr" for more functions and examples of working with strings that might help your understanding of this lesson's content.

In this lesson, you will learn how to:

- Expand deliminated text data in a data frame using `separate()` and`separate_rows()`; and,
- Extract and manipulate text data in character vectors using `str_match()`, and `str_remove()`

Prerequisite skills include:

- Some knowledge from the previous strings lesson in this module, as well as the `stringr` and `tidyr` packages.

## Separate text-based data frames using separate() and separate_rows()

`separate()` and `separate_rows()` allow you to split up a single column of text data in different ways.

`separate()` divides a single column of text data into multiple columns. There are several arguments that allow you to specify how this is done. We will focus on the most significant ones to start:

| Argument | Parameter | Details
| -------- | --------- | ----------------------------------------- |
| data     | data frame | A data frame |
| col | number OR string | The name or position of the column containing the data to be separated |
| into | vector | A character vector of the names you wish to give to the newly created columns. You can omit columns by putting `NA` in the corresponding place within this vector. The length of your input must match the largest number of columns produced by separating one of the cells in `col`, otherwise the excess columns will be omitted  |
| sep | number OR string | Indicates how text will be separated. Defaults to splitting at any non-alpha numeric characters. If you use a number, the column will split at the specified position within each string. If you use a character, the text will split at every instance of that character and the character will be omitted from the outputted columns. |

To see `separate()` in action, let's look at the following data frame called `dinner_party` which contains a list of guests for a dinner party and their food choices for a three course meal consisting of soup, salad, and a main course.


```r
guest <- c("Annie", "Mariam", "Haoluan", "Shirley", "Rohan", "Sam")
food <- c("butternut squash, ceasar, lasagna", "italian wedding, garden, chicken", "italian wedding, ceasar, lasagna", "italian wedding, ceasar, lasagna", "butternut squash, garden, chicken", "butternut squash, garden, lasagna")
dinner_party <- data.frame(guest, food)
dinner_party
#>     guest                              food
#> 1   Annie butternut squash, ceasar, lasagna
#> 2  Mariam  italian wedding, garden, chicken
#> 3 Haoluan  italian wedding, ceasar, lasagna
#> 4 Shirley  italian wedding, ceasar, lasagna
#> 5   Rohan butternut squash, garden, chicken
#> 6     Sam butternut squash, garden, lasagna
```

Right now the guests' orders are listed together in the column called `food`, but the data might be easier to read if each person's order for each course was in its own column. Observe the code below to see how this can be accomplished.


```r

separate(dinner_party, food, c("soup", "salad", "main course"), sep = ",")
#>     guest             soup   salad main course
#> 1   Annie butternut squash  ceasar     lasagna
#> 2  Mariam  italian wedding  garden     chicken
#> 3 Haoluan  italian wedding  ceasar     lasagna
#> 4 Shirley  italian wedding  ceasar     lasagna
#> 5   Rohan butternut squash  garden     chicken
#> 6     Sam butternut squash  garden     lasagna

# We can also exlude the salad column in the output by using the following code instead
# separate(dinner_party, food, c("soup", NA, "main course"), sep = ",")
```

Using `separate()`, we now can see each course as its own column and all the commas have been removed. Note that it's important to specify `sep = ","` in this case, since the default option would separate by spaces as well and split soup orders into separate columns which is not practical for our needs.

We can split up the information contained in the `food` column in a different way using `separate_rows()`. As the name might suggest, this function will split each string into distinct rows instead of columns. The syntax and arguments are similar to `separate()`:

| Argument | Parameter | Details
| -------- | --------- | ----------------------------------------- |
| data     | data frame | A data frame |
| ... | string | The name(s) of the column(s) containing the data to be separated. Multiple columns can be inputted if their lengths are compatible (i.e. the same number of new rows will be created once they are separated). Otherwise, an error will be raised. |
| sep | number OR string | Character between values to be separated. Defaults to any non-alpha-numeric characters. |

Notice that we don't need to worry about the name or number of new columns since none will be created. Once the data in the indicated column(s) has separated into additional rows, the data from accompanying columns will be duplicated to fill in the new row's remaining cells.

Run the code below and observe the difference between `separate()` and `separate_rows()`.


```r
separate_rows(dinner_party, food, sep = ",")
#> # A tibble: 18 × 2
#>    guest   food              
#>    <chr>   <chr>             
#>  1 Annie   "butternut squash"
#>  2 Annie   " ceasar"         
#>  3 Annie   " lasagna"        
#>  4 Mariam  "italian wedding" 
#>  5 Mariam  " garden"         
#>  6 Mariam  " chicken"        
#>  7 Haoluan "italian wedding" 
#>  8 Haoluan " ceasar"         
#>  9 Haoluan " lasagna"        
#> 10 Shirley "italian wedding" 
#> 11 Shirley " ceasar"         
#> 12 Shirley " lasagna"        
#> 13 Rohan   "butternut squash"
#> 14 Rohan   " garden"         
#> 15 Rohan   " chicken"        
#> 16 Sam     "butternut squash"
#> 17 Sam     " garden"         
#> 18 Sam     " lasagna"
```

## Trouble Shooting separate()

Sometimes it is hard to know exactly how many columns your data will create when using `separate()`, which can lead to errors or unintended results when specifying the `into` argument. The function comes with a few *additional* arguments to help you control what happens in these scenarios. Note that this applies only when `sep` is a string, since if `sep` is numeric the column in question is always separated into two columns at the indicated location.

| Argument | Parameter | Details
| -------- | --------- | ----------------------------------------- |
| extra | string | Used to control what happens if there are extra columns created once all the names from `sep` are used. There are two options (not including the default, "warn"): **"drop"**, which will exclude any additional columns created, or **"merge"**, which will split the text at most `length(into)` times (so the last column indicated by `into` will contain unseparated data). |
| fill | string | Used to control what happens if there are not enough columns created to match the names indicated in `into`. There are two options (not including the default, "warn"): **"right"**, which fills the data frame with missing values on the right, and **"left"**, which fills the data frame with missing values on the left of the actual data. |

Run and edit the code below and observe the difference between the scenarios.


```r
letters <- data.frame(x = c("a.b", "a.b.c", "a.b.c.d"))
letters
#>         x
#> 1     a.b
#> 2   a.b.c
#> 3 a.b.c.d

# Too many columns created - try "drop" and "merge" in place of "warn"
separate(letters, x, c("A", "B"), extra = "warn")
#> Warning: Expected 2 pieces. Additional pieces discarded in 2
#> rows [2, 3].
#>   A B
#> 1 a b
#> 2 a b
#> 3 a b

# Not enough columns created - try "left" and "right" in place of "warn"
separate(letters, x, c("A", "B", "C", "D"), fill = "warn")
#> Warning: Expected 4 pieces. Missing pieces filled with `NA`
#> in 2 rows [1, 2].
#>   A B    C    D
#> 1 a b <NA> <NA>
#> 2 a b    c <NA>
#> 3 a b    c    d
```


## Working with text data using str_match() and str_remove()

`str_match()` and `str_remove()` are functions from the `stringr` package that can be used to manipulate character vectors in different ways.

`str_match()` identifies the first instance of a given pattern within each element of a character vector by returning a new vector indicating the string found that matches the pattern. This is particularly useful for data that follows a set structure, such as phone numbers or postal codes. `str_match()` returns a character matrix, in which the first column contains the complete match and subsequent columns contain any matching sub-groups within the full match. 

`str_remove()` removes the first instance of a given pattern within each string in a character vector, returning an updated character vector.

Both functions take the same two arguments:

| Argument | Parameter | Details
| -------- | --------- | ----------------------------------------- |
| string | vector | Your character vector |
| pattern | string | The pattern to look for in `string` (either a general pattern or a specific string). |

Consider this vector called `postal_codes` containing 30 Toronto postal codes.



```r
postal_codes
#>  [1] "M5S2W8" "M5S5G5" "M4W3X2" "M5T3T3" "M4V9F6" "M4V6V9"
#>  [7] "M4V5K4" "M5T8U1" "M4V1V6" "M5R6X1" "M4Y7R8" "M5S5R9"
#> [13] "M4Y7N6" "M4W2S9" "M5S5X9" "M4V8K3" "M4V8K1" "M5T3B9"
#> [19] "M5S2Q7" "M5S5A4" "M4V5S4" "M5T1V4" "M5S5E2" "M4V9U6"
#> [25] "M5R8B8" "M4Y2K9" "M5R7T9" "M4W8M8" "M4Y8T7" "M5T7D1"
```

Suppose we want to identify the postal codes in this vector from areas surrounding the University of Toronto, which begin with "M5S". We can use the code below to do so.


```r
str_match(postal_codes, "M5S[1-9][A-Z][1-9]") 
#>       [,1]    
#>  [1,] "M5S2W8"
#>  [2,] "M5S5G5"
#>  [3,] NA      
#>  [4,] NA      
#>  [5,] NA      
#>  [6,] NA      
#>  [7,] NA      
#>  [8,] NA      
#>  [9,] NA      
#> [10,] NA      
#> [11,] NA      
#> [12,] "M5S5R9"
#> [13,] NA      
#> [14,] NA      
#> [15,] "M5S5X9"
#> [16,] NA      
#> [17,] NA      
#> [18,] NA      
#> [19,] "M5S2Q7"
#> [20,] "M5S5A4"
#> [21,] NA      
#> [22,] NA      
#> [23,] "M5S5E2"
#> [24,] NA      
#> [25,] NA      
#> [26,] NA      
#> [27,] NA      
#> [28,] NA      
#> [29,] NA      
#> [30,] NA
# The input for pattern here essentially means "M5S followed by any combination of the format number-letter-number"
```

We now have a vector containing only the postal codes of interest. Now suppose we actually wanted to remove these postal codes from the original data. This is where we could use `str_remove()`.


```r
str_remove(postal_codes, "M5S[1-9][A-Z][1-9]")
#>  [1] ""       ""       "M4W3X2" "M5T3T3" "M4V9F6" "M4V6V9"
#>  [7] "M4V5K4" "M5T8U1" "M4V1V6" "M5R6X1" "M4Y7R8" ""      
#> [13] "M4Y7N6" "M4W2S9" ""       "M4V8K3" "M4V8K1" "M5T3B9"
#> [19] ""       ""       "M4V5S4" "M5T1V4" ""       "M4V9U6"
#> [25] "M5R8B8" "M4Y2K9" "M5R7T9" "M4W8M8" "M4Y8T7" "M5T7D1"
```

We now have a vector with blank strings instead of postal codes that begin with "M5S". We can further manipulate the output of either of these functions to remove evidence of missing or blank values entirely.


```r
# Identify only postal codes near the University of Toronto
m5s_codes <- str_match(postal_codes, "M5S[1-9][A-Z][1-9]")
m5s_codes[!is.na(m5s_codes)]
#> [1] "M5S2W8" "M5S5G5" "M5S5R9" "M5S5X9" "M5S2Q7" "M5S5A4"
#> [7] "M5S5E2"
```


```r
# Identify only postal codes NOT near the University of Toronto
remove_m5s_codes <- str_remove(postal_codes, "M5S[1-9][A-Z][1-9]")
remove_m5s_codes[remove_m5s_codes != ""]
#>  [1] "M4W3X2" "M5T3T3" "M4V9F6" "M4V6V9" "M4V5K4" "M5T8U1"
#>  [7] "M4V1V6" "M5R6X1" "M4Y7R8" "M4Y7N6" "M4W2S9" "M4V8K3"
#> [13] "M4V8K1" "M5T3B9" "M4V5S4" "M5T1V4" "M4V9U6" "M5R8B8"
#> [19] "M4Y2K9" "M5R7T9" "M4W8M8" "M4Y8T7" "M5T7D1"
```

It is important to note that `str_match()` and `str_detect()` only operate on the first instance of the indicated pattern within each element of a string (this isn't so obvious in our postal code example since each string is rather simple and short). Both `str_match()` and `str_remove()` have accompanying functions `str_match_all()` and `str_remove_all()` which apply their functionality to *every* instance of the inputted pattern within the inputted character vector. Run the code below on a simpler vector to examine the difference.


```r
# Match
rhyme <- c("she", "sells", "sea", "shells")

str_match(rhyme, "s")
#>      [,1]
#> [1,] "s" 
#> [2,] "s" 
#> [3,] "s" 
#> [4,] "s"

str_match_all(rhyme, "s")
#> [[1]]
#>      [,1]
#> [1,] "s" 
#> 
#> [[2]]
#>      [,1]
#> [1,] "s" 
#> [2,] "s" 
#> 
#> [[3]]
#>      [,1]
#> [1,] "s" 
#> 
#> [[4]]
#>      [,1]
#> [1,] "s" 
#> [2,] "s"
```

```r
# Remove
rhyme <- c("she", "sells", "sea", "shells")

str_remove(rhyme, "s")
#> [1] "he"    "ells"  "ea"    "hells"

str_remove_all(rhyme, "s")
#> [1] "he"   "ell"  "ea"   "hell"
```

## Next Steps

Now that you are familiar with some functions that work with strings, you are well set up to explore other features that `stringr` has to offer. A good place to start is the `stringr` [cheatsheet](https://github.com/rstudio/cheatsheets/blob/master/strings.pdf) which outlines a myriad of tools for working with strings and text-based data in R.



## Exercises

These questions will refer to the following data set called `groceries`.


```
#>                                     food
#> 1 bananas,apples,rice,noodles,tofu,pizza
#>                  drinks
#> 1 tea,coffee,juice,wine
```

### Question 1
How many rows will the output of `separate_rows(groceries, drinks)` have?

  a.  4
  b. 5
  c. 6
  d. An error will occur

### Question 2

How many rows will the output of `separate_rows(groceries, food, drinks)` have?

  a. 4
  b. 5
  c. 6
  d.  An error will occur
  
### Question 3
Suppose I execute `separate(groceries, drinks, into=c("A", "B", "C", "D", "E"), fill="left")`. What will the second column ("A") of the outputted data frame contain?
  
  a. "bananas,apples,rice,noodles,tofu,pizza"
  b. "tea"
  c.  NA
  d. An error will occur

### Question 4

Suppose I execute `separate(groceries, drinks, into=c("A", "B", "C"), extra="merge")`. What will the final column of the outputted data frame contain?

  a. "juice"
  b. "wine"
  c.  "juice,wine"
  d. An error will occur

### Question 5

Which of the following lines of code would produce this data frame:

```
#> # A tibble: 6 × 5
#>   food    `1`   `2`    `3`   `4`  
#>   <chr>   <chr> <chr>  <chr> <chr>
#> 1 bananas tea   coffee juice wine 
#> 2 apples  tea   coffee juice wine 
#> 3 rice    tea   coffee juice wine 
#> 4 noodles tea   coffee juice wine 
#> 5 tofu    tea   coffee juice wine 
#> 6 pizza   tea   coffee juice wine
```

  a. `groceries %>% separate_rows(food)`
  b. `groceries %>% separate_rows(drinks, into=c("1", "2", "3", "4"))`
  c. `groceries %>% separate(drinks, into=c("1", "2", "3", "4"))`
  d.  `groceries %>% separate(drinks, into=c("1", "2", "3", "4")) %>% separate_rows(food)`

### Question 6

Using the `postal_codes` data from previous examples, which of the following lines of code would result in an object containing only letters?

  a. `postal_codes %>% str_remove("[1-9]")`
  b. `postal_codes %>% str_remove_all("[1-9]")`
  c. `postal_codes %>% str_match("[1-9]")`
  d. `postal_codes %>% str_match_all("[1-9]")`

### Question 7
Which of the following best describes the output of `postal_codes %>% str_match("M5S[1-9][A-Z][1-9]") %>% str_remove("M5S")`?

  a. A vector that contains only the last three characters of all postal codes beginning with "M5S"
  b.  A vector that contains the last three characters of all postal codes from `postal_codes` beginning with "M5S" and `NA` values at all indices that do not meet this criteria
  c. A vector that contains only entries from `postal_codes` that do not contain "M5S"
  d. A vector that contains only entries from `postal_codes` that do not contain "M5S"  and `NA` values at all indices that do not meet this criteria

