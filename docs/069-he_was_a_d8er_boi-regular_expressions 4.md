


# Regular expressions

*Written by Shirley Deng and last updated on 7 October 2021.*

To use the `stringr` package, we can describe patterns in strings using regular expressions, or regex. This section will outline a variety of regex examples :\^)

For the examples below, we have a grocery list stored as the vector `groceries`.


```r
groceries <- c("Bananas", "strawberries", "Sliced bread", 
               "2 lb ground beef", "blueberries", "frozen raspberry", 
               "red color plums", "frozen Mixed-Berries", "yellow colour plums")
```

## Starting with the basics

Say we're interested in seeing how many different types of berries are on our list. 

We can match exact strings by simply using them as the `pattern` argument in our chosen `stringr` function. Here, we are using `stringr::str_subset()`


```r
str_subset(groceries, "berries")
#> [1] "strawberries" "blueberries"
```

## Wrapping our package

When we use a plain string for the `pattern` argument, R reads it by wrapping it in the `regex()` function.


```r
str_subset(groceries, regex("berries"))
#> [1] "strawberries" "blueberries"
```

Notice that whether we use `stringr::str_subset()` with `"berries"` or `regex("berries")` as our pattern argument, the results are the same.

## Insensitive about cases

Notice that in the above examples, `str_subset()` was case sensitive and did not return the `"Mixed Berries"` item in our `groceries` list.

However, if we include the argument `ignore_case=T` in `regex()`, it will.


```r
str_subset(groceries, regex("Berries", ignore_case=T))
#> [1] "strawberries"         "blueberries"         
#> [3] "frozen Mixed-Berries"
```

Note: if we want to use options other than the default for `regex()`, we have to explicitly wrap our pattern criteria in the `regex()` function.

## Period.

Notice that the item `"frozen raspberry"` is a berry, but was not returned in the earlier examples because we were only searching for the plural spelling `"berries"`.

The period `.` is used to match any character except the newline `\n`, so we can use the common part `"berr"` to include `"frozen raspberry"`.


```r
str_subset(groceries, ".berr.")
#> [1] "strawberries"     "blueberries"      "frozen raspberry"
```

However, if we did want to include the newline `\n`, then we can explicitly state this in the `regex()` arguments as well using `dotall=T`. Here, we use the `stringr` function `str_detect()`:


```r
str_detect("\nGroceries\n", ".G.")
#> [1] FALSE
str_detect("\nGroceries\n", regex(".G.", dotall=T))
#> [1] TRUE
```

## From start to finish

Alternatively, we can also search for strings that start or end with a certain pattern by using anchors.

For example, if we wanted all frozen items in `groceries`, we can use the caret `^` to indicate the start of a string and search for items beginning with "frozen":


```r
str_subset(groceries, "^frozen")
#> [1] "frozen raspberry"     "frozen Mixed-Berries"
```

Or if we wanted all varieties of plums in `groceries`, we can use the dollar sign `$` to indicate the end of a string and search for all items ending with "plums":


```r
str_subset(groceries, "plums$")
#> [1] "red color plums"     "yellow colour plums"
```

Some [additional anchors](https://www.rstudio.com/wp-content/uploads/2016/09/RegExCheatsheet.pdf) are as follows: 

Syntax   |   Use 
---|--- 
`^` | start of the string 
`$` | end of the string 
`\\b` | empty string at either edge of a word 
`\\B` | not the edge of a word 
`\\<` | beginning of a word 
`\\>` | end of a word 

## Or how about...

Or how about we try explicitly searching for all of `"berries"`,  `"Berries"`, and `"berry"`? We can do so with the alternation operator, `|`, which means "or".


```r
str_subset(groceries, "berries|Berries|berry")
#> [1] "strawberries"         "blueberries"         
#> [3] "frozen raspberry"     "frozen Mixed-Berries"
```

Alternatively, we can also use parentheses `()` to write this more concisely. The parantheses essentially do the same thing they do in BEDMAS/PEDMAS for math: indicate grouping.


```r
str_subset(groceries, "(b|B)err(ies|y)")
#> [1] "strawberries"         "blueberries"         
#> [3] "frozen raspberry"     "frozen Mixed-Berries"
```

## Color or colour?

Notice that in we have spelled both "color" and "colour" in `groceries`. Suppose we wanted to find all of the items that had their colour indicated.

There are a variety of ways we could do this using the tools we have so far.

For example, using the alternation operator `|`:


```r
str_subset(groceries, "color|colour")
#> [1] "red color plums"     "yellow colour plums"
```

Or, using parentheses `()` too:


```r
str_subset(groceries, "colo(r|ur)")
#> [1] "red color plums"     "yellow colour plums"
```

Alternatively, we can also use repetition quantifiers.

For example, the question mark `?` indicates that the preceding item is optional, and can be matched up to once. We can thus us `?` to indicate that the "u" in "colour" is optional:


```r
str_subset(groceries, "colou?r")
#> [1] "red color plums"     "yellow colour plums"
```

Below is a list of some of these [repetition operators](https://www.rstudio.com/wp-content/uploads/2016/09/RegExCheatsheet.pdf): 

Syntax   | Use
---|---
`?`   |   The preceding item is optional and will be matched at most once 
`*`   |   The preceding item will be matched zero or more times 
`+`   |   The preceding item will be matched one or more times 
`{n}`   |   The preceding item is matched exactly n times 
`{n,}`   |   The preceding item is matched n or more times 
`{n,m}`   |   The preceding item is matched at least n times, but not more than m times 

## Building character

Suppose we wanted to search for all items in `groceries` that have amounts provided. How many lbs of beef do we need? Is the number of plums specified?

One way we could do this is to search for digits altogether. Using our current knowledge of regex, we could use the following:


```r
str_subset(groceries, "0|1|2|3|4|5|6|7|8|9")
#> [1] "2 lb ground beef"
```

R has syntax for classes of characters, though. And in this case, the class of digits is referred to with `[:digit:]`. 

Below is a list of some [character classes](https://www.rstudio.com/wp-content/uploads/2016/09/RegExCheatsheet.pdf):

Syntax  |  Use
---|---
`[:alnum:]`   |   Alphanumeric characters: `[:alpha:]` and `[:digit:]` 
`[:alpha:]`   |   Alphabetic characters: `[:lower:]` and `[:upper:]`
`[:blank:]`   |   Blank characters: space and tab, and possibly other locale-dependent characters such as non-breaking space 
`[:cntrl:]`   |   Control characters. In ASCII, these characters have octal codes 000 through 037, and 177 (DEL). In another character set, these are the equivalent characters, if any 
`[:digit:]`   |   Digits: `0`, `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, and `9` 
`[:graph:]`   |   Graphical characters: `[:alnum:]` and `[:punct:]` 
`[:lower:]`   |   Lower-case letters in the current locale 
`[:print:]`   |   Printable characters: `[:alnum:]`, `[:punct:]` and space 
`[:punct:]`   |   Punctuation characters: `` ` ``, `!`, `"`, `#`, `$`, `%`, `&`, `'`, `(`, `)`, `*`, `+`, `,`, `-`, `.`, `/`, `:`, `;`, `<`, `=`, `>`, `?`, `@`, `[`, `\`, `]`, `^`, `_`, `{`, `|`, `}`, and `~`
`[:space:]`   |   Space characters: tab, newline, vertical tab, form feed, carriage return, space, and possibly other locale-dependent characters 
`[:upper:]`   |   Upper-case letters in the current locale 
`[:xdigit:]`   |   Hexadecimal digits: `0`, `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`, `A`, `B`, `C`, `D`, `E`, `F`, `a`, `b`, `c`, `d`, `e`, `f`

We can also build our own [character classes](https://www.rstudio.com/wp-content/uploads/2016/09/RegExCheatsheet.pdf), though. For example:

Syntax  |  Use
---|---
`[xyz]`   |   would match `x`, `y`, or `z` 
`[a-z]`   |   would match every character between `a` and `z` in Unicode code point order 
`[^xyz]`  |   would match anything except `x`, `y`, or `z`
`[\~\!]`   |   would match `~` or `!`

Whenever we want to use a pre-built character class like `[:digit:]`, we have to wrap it in an extra set of square brackets `[]`. 

Thus, we can use this:


```r
str_subset(groceries, "[[:digit:]]")
#> [1] "2 lb ground beef"
```

Or this:


```r
str_subset(groceries, "[0123456789]")
#> [1] "2 lb ground beef"
```

To search for all items in `groceries` that have amounts provided:

## Help me escape!

Recall from the R markdown section that there were a number of special characters that we needed to escape with `\` in order to get them to show up, rather than perform some code-y function. These special characters are called **metacharacters**.

Additionally, recall that the newline character is indicated with `\n`. However, it's not the only such character with this kind of special syntax. Below are some more of these special characters, also called [metacharacters](https://www.rstudio.com/wp-content/uploads/2016/09/RegExCheatsheet.pdf): 

Syntax  |  Use
---|---
`\n`   |   new line 
`\r`   |   carriage return 
`\t`   |   tab 
`\v`   |   vertical tab 
`\f`   |   form feed

Now, what if we wanted to match a pattern containing `*`, `+`, or `\t`, for example?

Consider the following list `spam`:


```r
spam <- c("2*2=4", "raining cats and dogs", "they\them", "they/them", "heurex.se", "peanut butter")
```

We can try to match these metacharacters as usual:


```r
str_detect(spam, "*|+|\t")
```

But we get an error.

In order to use these metacharacters as literal characters, we can either escape them by using `\\`:


```r
str_subset(spam, "(\\*)|(\\+)|(\\\t)")
```

Or by enclosing them between `\\Q` and `\\E`:


```r
str_subset(spam, "\\Q*\\E|\\Q+\\E|\\Q\t\\E")
```

## Functioning functions

Alternatively, instead of using the `stringr` package, we can also use some of the following [base R functions](https://www.rstudio.com/wp-content/uploads/2016/09/RegExCheatsheet.pdf): 

Function   |   Use 
---|---
`grep()`, `grepl()`   |   These functions search for matches of a regular expression/pattern in a character vector. `grep()` returns the indices into the character vector that contain a match or the specific strings that happen to have the match. `grepl()` returns a `T`/`F` vector indicating which elements of the character vector contain a match
`regexpr()`, `gregexpr()`   |    Search a character vector for regular expression matches and return the indices of the string where the match begins and the length of the match 
`sub()`, `gsub()`   |    Search a character vector for regular expression matches and replace that match with another string
`regexec()`   |    This function searches a character vector for a regular expression, much like `regexpr()`, but it will additionally return the locations of any parenthesized sub-expressions. Probably easier to explain through demonstration.

## Additional resources and references

- [R regex cheatsheet](https://www.rstudio.com/wp-content/uploads/2016/09/RegExCheatsheet.pdf)
- [stringr cheatsheet](https://github.com/rstudio/cheatsheets/blob/master/strings.pdf)
- [stringr vignette](https://stringr.tidyverse.org/articles/regular-expressions.html)
- [line breaks](https://stackoverflow.com/questions/21781014/remove-all-line-breaks-enter-symbols-from-the-string-using-r)
- [escaping line breaks](https://meta.stackexchange.com/questions/82718/how-do-i-escape-a-backtick-within-in-line-code-in-markdown)
- [Albert Y. Kim's "Regular Expressions in R"](https://rstudio-pubs-static.s3.amazonaws.com/74603_76cd14d5983f47408fdf0b323550b846.html)
- [Hadley Wickham and Garrett Grolemund's *R for Data Science* section "Strings"](https://r4ds.had.co.nz/strings.html)
- [Roger D. Peng's *R Programming for Data Science* section "Regular Expressions"](https://bookdown.org/rdpeng/rprogdatascience/regular-expressions.html)



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
