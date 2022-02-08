


# paste, paste0, glue and stringr

*Written by Marija Pejcinovska and last updated on 6 February 2022.*



## Introduction  

In this lesson we'll cover a couple of ways in which you can paste strings to your data. We'll use the `paste()` and `paste0()` functions, both of which are part of base R,  as well as the `glue()` function in the `glue` package. As part of this tutorial, you will also get a first taste of the `stringr` package, which is a wonderful tool for handling strings.  


Prerequisite skills:

- Familiarity with `tidyverse` functions.  
- Some basic data manipulation.



## Paste strings and data with `pate()` and `paste0()`

`paste()` and `paste0()` are handy R functions used for concatenating strings and/or data. One of the main difference between the two is the default setting in their arguments, specifically the argument used to denote the way in which results should be separated. Both `paste()` and `paste0()` convert all passed objects to character vectors.   

Both functions have the following two arguments: `sep = ` and `collapse = `.

Let's see `paste()` in action first.   

You can pass individual objects to `paste()`

```r

paste(1, "a", "b")
#> [1] "1 a b"
```
 or pass vectors.

```r
paste(1:3, c("a", "b", "c"))
#> [1] "1 a" "2 b" "3 c"
```
Notice that when the arguments passed are vectors, the concatenation happens term-by-term. Vector arguments are recycled as necessary.  
For instance, note the difference between

```r
paste(1:2, "a", "b", "c")
#> [1] "1 a b c" "2 a b c"
```
and 

```r
paste(1:2, c("a", "b", "c"))
#> [1] "1 a" "2 b" "1 c"
```
You can see that in the latter example the concatenation is term-by-term and the sequence `1:2` is getting recycled (i.e. restarted) to match the length of `c("a", "b", "c")`.  

The argument `sep = ` in the function controls which character string is used to separate the terms. By default, the `paste()` function sets `sep = " "`, meaning concatenated terms are separated by empty space. We can set the separator to be any string character we'd like. 


```r
## Leaving no space
paste(1:2, c("a", "b", "c"), sep = "")
#> [1] "1a" "2b" "1c"

## Concatenating with a dash
paste(1:2, c("a", "b", "c"), sep = "-")
#> [1] "1-a" "2-b" "1-c"

## Concatenating with a random letter
paste(1:2, c("a", "b", "c"), sep = "Y")
#> [1] "1Ya" "2Yb" "1Yc"

##..and so on
```

If a value is specified for the argument `collapse = `, the elements in the result are then turned into a single string, with the components being separated by the character string provided in `collapse`. For instance, we can turn 

```r
paste(1:2, c("a", "b", "c"), sep = "-")
#> [1] "1-a" "2-b" "1-c"
```
into a single string as

```r
paste(1:2, c("a", "b", "c"), sep = "-", collapse = ", ")
#> [1] "1-a, 2-b, 1-c"
```

where we've used `,  ` ` ` (comma with a blank space) as a separator.

The most preferred separator tends to be the "no space" one. This is the default setting of `paste0`.

The following code will illustrate the difference between `paste` and `paste0`


```r

paste("I", "Love", "R","!")
#> [1] "I Love R !"

paste0("I", "Love", "R", "!")
#> [1] "ILoveR!"
```

Of course, you might be interested in a more sophisticated collection of objects to paste. For instance, suppose you needed to work with a combination of character strings and existing R objects.


```r
student <- c("Rohan", "Monica")
badges <- c(2,4)
term <- c("Fall", "Spring")

paste(student, "collected", badges, "DoSS tool-kit badges in the", term )
#> [1] "Rohan collected 2 DoSS tool-kit badges in the Fall"   
#> [2] "Monica collected 4 DoSS tool-kit badges in the Spring"
```


## "Gluing" your data with the `glue` package


\
The `glue` package is designed to make it easier to "stitch" or interpolate (or "glue") your data into strings. Its main function is quite similar in flavor to `paste()` (and `paste0()`), but a bit easier to use (this is especially true when compared to `sprintf()` — a function that we have not discussed here, but can similarly be used to concatenate strings and data).  

You can install `glue` the usual way you would any other package, by calling `install.packages("glue")`.

### The functions of `glue`
The glue package has three primary functions, `glue()`, `glue_data()` and `glue_collapse()`.   

The **`glue()` function** works a bit like the `paste()` function. In the case of `glue()`, however, we use `{}` to wrap the R code we wish to reference inside the string. This makes it a bit more manageable compared to all the quotation marks, commas, and separators we need to keep track of when using `paste()`.

Let's refer back to our example from earlier and check out the syntax for `glue()`. Note that now *everything is placed inside a single set of quotation marks* and R objects are referenced within the string by *wrapping them up in curly brackets*. 


```r
# Recycling the code from our previous example
student <- c("Rohan", "Monica")
badges <- c(2,4)
term <- c("Fall", "Spring")

# Call to the glue() function
glue("{student} collected {badges} DoSS tool-kit badges in {term}")
#> Rohan collected 2 DoSS tool-kit badges in Fall
#> Monica collected 4 DoSS tool-kit badges in Spring
```

Here we've called the R objects `student`, `badges`, and `term` by wrapping them up in `{}`. 

If you wish to use something other than `{}`, you can specify different opening and closing delimiters by using the `.open = ` and `.close = ` arguments in the `glue` function. For instance, let's surround the code we wish to evaluate by `<` at the beginning and `]` at the end.


```r
student <- c("Owen", "Monica")
badges <- c(2,4)
term <- c("Fall", "Spring")

glue("<student] collected <badges] DoSS tool-kit badges in <term]", .open = "<", .close = "]")
#> Owen collected 2 DoSS tool-kit badges in Fall
#> Monica collected 4 DoSS tool-kit badges in Spring
```

The function **`glue_data()`** works much like `glue()` but it is easier to use in piped chains (recall the pipe operator, ` %>% `). What's important to note here is that inside the curly braces we pass the column names of the columns in our data we wish to glue in some way (and not the name of the variables or R object as we did with `glue()`). 

As an example we'll look at the `palmer penguins` data in R. You can try this code in your console and note what happens when you change `glue_data()` below with `glue()`.


```r
library(palmerpenguins)
# Check the data out
penguins %>% 
  head(n=4)
#> # A tibble: 4 × 8
#>   species island    bill_length_mm bill_depth_mm
#>   <fct>   <fct>              <dbl>         <dbl>
#> 1 Adelie  Torgersen           39.1          18.7
#> 2 Adelie  Torgersen           39.5          17.4
#> 3 Adelie  Torgersen           40.3          18  
#> 4 Adelie  Torgersen           NA            NA  
#> # … with 4 more variables: flipper_length_mm <int>,
#> #   body_mass_g <int>, sex <fct>, year <int>

# "Glue" some data elements together
penguins %>% 
  slice(1:4) %>% 
  glue_data("This {species} penguin living on {island} \\
            island has flipper length {flipper_length_mm} mm") 
#> This Adelie penguin living on Torgersen island has flipper length 181 mm
#> This Adelie penguin living on Torgersen island has flipper length 186 mm
#> This Adelie penguin living on Torgersen island has flipper length 195 mm
#> This Adelie penguin living on Torgersen island has flipper length NA mm

# note: the "\\" symbol in the string code above is simply to force the string to appear as one line. 
 
```


Finally, the **`glue_collapse()` function** concatenates multiple values into one. This function has a particularly clever and useful argument called `last` which allows you to change the separator for the last value (a feature not available in `paste()`).  

Here is something you can do with `glue_collapse()` that you cannot with `paste()` or `paste0()`. 


```r
glue_collapse({letters[1:3]}, sep = ", ", last = ", and ")
#> a, b, and c
```

This makes `glue_collapse()` a neat function for adding values of R objects inline in an RMarkdown file.  


## First taste of the `stringr` package

\
As a budding data scientist, you may have discovered that data analysis tasks usually involve spending an outsize portion of your time cleaning and processing data (it's a very special tax you have to pay before you get to the "fun" data scienc-y bits and pieces!!).   

On occasion your data may contain lots of text or strings. The `stringr` package, which is part of the core *tidyverse*, is a wonderful collection of functions that make string manipulation easier.   

This section is intended to get you started with the `stringr` package and involves just a brief introduction to the `str_detect()` and `str_replace()` functions in `stringr`.   

All functions in this package begin with the `str_` prefix and have easy to remember, intuitive names. 

For instance, `str_detect()` allows you to check whether a vector of characters contains a particular pattern, in other words, it allows you to *detect* a pattern in a string. The function returns a logical vector of the same length as the input, where `TRUE` indicates the pattern has been matched in that index. 

Let's check this out.

```r

my_vec <- c("r", "R", "I love R", "why?", "what is this?")

my_vec %>% 
  str_detect("r")
#> [1]  TRUE FALSE FALSE FALSE FALSE

my_vec %>% 
  str_detect("wh")
#> [1] FALSE FALSE FALSE  TRUE  TRUE
```

Note that the pattern detection is case sensitive. 

`str_replace()`, on the other hand, allows you to replace a matched pattern with an entirely new string (or an empty string, if what you  wish to do is remove the pattern; see also `str_remove()`). Let's see what that looks like using our object `my_vec` 


```r
# Let's see my_vec again
my_vec 
#> [1] "r"             "R"             "I love R"     
#> [4] "why?"          "what is this?"

# We'll replace every instance of "?" with the word "code"

my_vec %>% 
  str_replace("\\?", " code")
#> [1] "r"                 "R"                
#> [3] "I love R"          "why code"         
#> [5] "what is this code"
```

The first argument is the pattern we are trying to find a match for. In our case that is `?` (note that since ? is a special character we need to escape it by placing `\\` before `?`). The second argument here is the string we wish to replace our matched pattern with. So we replace `?` with the string `code`. 

Let's see the `str_replace()` function applied to our penguins data. We'll use it to slightly modify the name of an island.  


```r

penguins %>% 
  slice(1:4) %>% 
  mutate(new_island = str_replace(island, "Tor", "Mor")) %>% 
  dplyr::select(species, island, new_island)
#> # A tibble: 4 × 3
#>   species island    new_island
#>   <fct>   <fct>     <chr>     
#> 1 Adelie  Torgersen Morgersen 
#> 2 Adelie  Torgersen Morgersen 
#> 3 Adelie  Torgersen Morgersen 
#> 4 Adelie  Torgersen Morgersen
```

Note that if you want to remove a pattern in a string that occurs more than once in that string, you will need to use the function `str_replace_all`. `str_replace` itself will only replace the first occurrence of a matched pattern. 

This is just a small slice of what the `stringr` package has to offer. Be on the lookout for future tutorials with more on strings and regular expressions. 


<!--
## Exercises


Consider the first few rows of the penguin data we saw in an example earlier. For this exercise we'll call the sliced data `small-penguins`. To refresh your memory of what the data frame looks like it's been reproduced here (use the arrows to navigate left and right through the columns). 


```r
small_penguins <- penguins %>% 
  slice(1:10)
small_penguins
#> # A tibble: 10 × 8
#>    species island    bill_length_mm bill_depth_mm
#>    <fct>   <fct>              <dbl>         <dbl>
#>  1 Adelie  Torgersen           39.1          18.7
#>  2 Adelie  Torgersen           39.5          17.4
#>  3 Adelie  Torgersen           40.3          18  
#>  4 Adelie  Torgersen           NA            NA  
#>  5 Adelie  Torgersen           36.7          19.3
#>  6 Adelie  Torgersen           39.3          20.6
#>  7 Adelie  Torgersen           38.9          17.8
#>  8 Adelie  Torgersen           39.2          19.6
#>  9 Adelie  Torgersen           34.1          18.1
#> 10 Adelie  Torgersen           42            20.2
#> # … with 4 more variables: flipper_length_mm <int>,
#> #   body_mass_g <int>, sex <fct>, year <int>
```




```r
small_penguins <- penguins %>% 
  slice(1:7)
small_penguins
#> # A tibble: 7 × 8
#>   species island    bill_length_mm bill_depth_mm
#>   <fct>   <fct>              <dbl>         <dbl>
#> 1 Adelie  Torgersen           39.1          18.7
#> 2 Adelie  Torgersen           39.5          17.4
#> 3 Adelie  Torgersen           40.3          18  
#> 4 Adelie  Torgersen           NA            NA  
#> 5 Adelie  Torgersen           36.7          19.3
#> 6 Adelie  Torgersen           39.3          20.6
#> 7 Adelie  Torgersen           38.9          17.8
#> # … with 4 more variables: flipper_length_mm <int>,
#> #   body_mass_g <int>, sex <fct>, year <int>
```

### Exercise 1

Change this function from the `glue` package to produce the following string "This penguin is of the species XXX from island XXX and has body mass of XXX g" describing the 6th penguin in `small_penguins`, where the three XXX should be species, island name, and body mass respectively.



```r

small_penguins %>% 
  slice(6) %>% 
  glue_data("This penguin is of the species {island} from island {body_mass_g} and has body mass of {species} g" )
#> This penguin is of the species Torgersen from island 3650 and has body mass of Adelie g
```


```r

small_penguins %>% 
  slice(6) %>% 
  glue_data("This penguin is of the species {species} from island {island} and has body mass of {body_mass_g} g" )
#> This penguin is of the species Adelie from island Torgersen and has body mass of 3650 g
```



### Exercise 2

Using `glue()` and `glue_collapse()` manipulate the vectors `quant` and `food` below to get the following single string "1 sushi roll, 2 tacos, and 3 cakes"


```r

quant <- 1:3
food <- c("sushi roll", "tacos", "cakes")

```


```r

quant <- 1:3
food <- c("sushi roll", "tacos", "cakes")

glue_collapse((glue("{quant} {food}")), sep = ", ", last = ", and ")
#> 1 sushi roll, 2 tacos, and 3 cakes

# Or alternatively with the piping syntax
glue("{quant} {food}") %>% 
  glue_collapse(.,sep = ", ", last = ", and")
#> 1 sushi roll, 2 tacos, and3 cakes
```


### Exercise 3 

Back to our `small_penguins` data from Exercise 1.

Use `str_detect()` and `filter()` to subset the `small_penguins` data to include only female penguins. 


```r
small_penguins %>% 
  filter(str_detect(sex, "male"))
#> # A tibble: 6 × 8
#>   species island    bill_length_mm bill_depth_mm
#>   <fct>   <fct>              <dbl>         <dbl>
#> 1 Adelie  Torgersen           39.1          18.7
#> 2 Adelie  Torgersen           39.5          17.4
#> 3 Adelie  Torgersen           40.3          18  
#> 4 Adelie  Torgersen           36.7          19.3
#> 5 Adelie  Torgersen           39.3          20.6
#> 6 Adelie  Torgersen           38.9          17.8
#> # … with 4 more variables: flipper_length_mm <int>,
#> #   body_mass_g <int>, sex <fct>, year <int>
```


```r

small_penguins %>% 
  filter(str_detect(sex, "fe"))
#> # A tibble: 4 × 8
#>   species island    bill_length_mm bill_depth_mm
#>   <fct>   <fct>              <dbl>         <dbl>
#> 1 Adelie  Torgersen           39.5          17.4
#> 2 Adelie  Torgersen           40.3          18  
#> 3 Adelie  Torgersen           36.7          19.3
#> 4 Adelie  Torgersen           38.9          17.8
#> # … with 4 more variables: flipper_length_mm <int>,
#> #   body_mass_g <int>, sex <fct>, year <int>
```





### Exercise 4

Use  `mutate()` to create a new variable `island_short` where with the help of `str_replace` you remove the pattern "ersen" from the island name.


```r

 small_penguins %>% 
  mutate(island_short = str_replace(island, pattern = "island", replacement = ""))
#> # A tibble: 7 × 9
#>   species island    bill_length_mm bill_depth_mm
#>   <fct>   <fct>              <dbl>         <dbl>
#> 1 Adelie  Torgersen           39.1          18.7
#> 2 Adelie  Torgersen           39.5          17.4
#> 3 Adelie  Torgersen           40.3          18  
#> 4 Adelie  Torgersen           NA            NA  
#> 5 Adelie  Torgersen           36.7          19.3
#> 6 Adelie  Torgersen           39.3          20.6
#> 7 Adelie  Torgersen           38.9          17.8
#> # … with 5 more variables: flipper_length_mm <int>,
#> #   body_mass_g <int>, sex <fct>, year <int>,
#> #   island_short <chr>
```


```r

 small_penguins %>% 
  mutate(island_short = str_replace(island, pattern = "ersen", replacement = ""))
#> # A tibble: 7 × 9
#>   species island    bill_length_mm bill_depth_mm
#>   <fct>   <fct>              <dbl>         <dbl>
#> 1 Adelie  Torgersen           39.1          18.7
#> 2 Adelie  Torgersen           39.5          17.4
#> 3 Adelie  Torgersen           40.3          18  
#> 4 Adelie  Torgersen           NA            NA  
#> 5 Adelie  Torgersen           36.7          19.3
#> 6 Adelie  Torgersen           39.3          20.6
#> 7 Adelie  Torgersen           38.9          17.8
#> # … with 5 more variables: flipper_length_mm <int>,
#> #   body_mass_g <int>, sex <fct>, year <int>,
#> #   island_short <chr>
```


-->

## Next Steps

This tutorial only briefly introduced you to the capabilities of the `stringr` package. Future tutorials will revisit this package and dive deeper into some of its functions. In the meantime you can learn more about this package in Hadley Wichkam's book [*R for Data Science*](https://r4ds.had.co.nz/strings.html) . The link here takes you to the chapter on strings which also introduces you to regular expressions (regular expressions are a bit tedious, but you might learn to like them if you end up working with text data a lot).



## Exercises



### Question 1

The main difference between the `paste()` and `paste0()` functions is:  

  a. The default setting for the `collapse` argument.  
  b.  The default setting for the `sep` argument. 
  c. `paste0` allows more flexibility by offering more arguments.
  d. None of the above.

### Question 2  

When concatenating two R objects, say a sequence of numbers and a vector of characters, using `paste()`, the length of the resulting vector will be:  
  
  a. The sum of the length of the two object. 
  b. The length of the shorter object (either the sequence or the vector, whichever has fewer elements).
  c.  The length of the longer object (either the sequence or the vector, whichever has more elements).  
  
### Question 3  

When concatenating the vectors `c("one", "two", "three")` and `c("four", "five")` using the following command `paste0(c("one", "two", "three"), c("four", "five"))`, the elements of which vector will get recycled in the resulting expression?  

  a. The elements of `c("one", "two", "three")` will be recycled through. 
  b.  The elements of `c("four", "five")` will be recycled.   
  c. None will be recycled; they are both vectors.  
  
### Question 4

Using only the vector `c(2:4)` and string `"things"`, which of the following lines of code would create the string "2things, 3things, and 4things"?  

  a. `paste0(c(2:4),"things", sep = ", ")`  
  b. `paste(c(2:4),"things", sep = ", ", collapse = "")`  
  c.  `glue_collapse(glue("{c(2:4)}things"), sep=", ", last = ", and ")`  
  d. `glue("{c(2:4)}things", sep=", ", last = ", and ")`

### Question 5 

Given the vector `fruit` described below, which of the following lines of code correctly replaces the `e`'s with `YEI`?


```r
fruit <- c("apples", "pears", "strawberries")
```

  a. `str_detect(fruit,"e","YEI")` 
  b. `str_remove(fruit,"e")` 
  c. `str_replace(fruit, "e", "YEI")`  
  d.  `str_replace_all(fruit, "e", "YEI")`
  e. `str_replace_all(fruit, "YEI", "e")`  
  


### Question 6

Consider the following R objects, `quant` and `food`

```r
quant <- 1:3
food <- c("sushi roll", "tacos", "cakes")
```

Which line of code below would have created the string "1 sushi roll, 2 tacos, and 3 cakes"  

  a. `glue("{quant} {food}",sep=", ", last=", and ")`  
  b. `glue_collapse((glue("{quant} {food}")),sep=", ")`   
  c. `glue("{quant} {food}", last=", and ")`   
  d. `glue_data((glue("{quant} {food}")),sep=", ", last=", and ")`
  e.  `glue_collapse((glue("{quant} {food}")),sep=", ", last=", and ")`

### Question 7

Using the objects `quant` and `food` from Question 6, what would the line of code `glue_collapse(glue("{quant} {food[2]}"), sep =", ")`generate?  

  a. The string: `1 sushi roll, 2 sushi roll`  
  b. The string: `2 sushi roll, 2 tacos, 2 cakes`  
  c.  The string: `1 tacos, 2 tacos, 3 tacos`  
  
### Question 8  

Consider the first few rows of the penguin data we saw in earlier examples. We'll call a 10-row slice of the data `small_penguins`. To refresh your memory of what the data frame looks like it's been reproduced here (use the arrows to navigate left and right through the columns). 


```r
small_penguins <- penguins %>% 
  slice(1:10)
small_penguins
#> # A tibble: 10 × 8
#>    species island    bill_length_mm bill_depth_mm
#>    <fct>   <fct>              <dbl>         <dbl>
#>  1 Adelie  Torgersen           39.1          18.7
#>  2 Adelie  Torgersen           39.5          17.4
#>  3 Adelie  Torgersen           40.3          18  
#>  4 Adelie  Torgersen           NA            NA  
#>  5 Adelie  Torgersen           36.7          19.3
#>  6 Adelie  Torgersen           39.3          20.6
#>  7 Adelie  Torgersen           38.9          17.8
#>  8 Adelie  Torgersen           39.2          19.6
#>  9 Adelie  Torgersen           34.1          18.1
#> 10 Adelie  Torgersen           42            20.2
#> # … with 4 more variables: flipper_length_mm <int>,
#> #   body_mass_g <int>, sex <fct>, year <int>
```


Which of the following lines of code will produce the string "This penguin is of the species XYZ" describing the 6th penguin in `small_penguins`, where XYZ is a placeholder for the specific species of the 6th penguin.  

  a. `small_penguins %>% slice(1:6) %>% glue("This penguin is of the species {species}")`  
  b. `small_penguins %>% slice(6) %>% glue_collapse("This penguin is of the species {species}")`  
  c. `small_penguins %>% slice(1:6) %>% glue_data("This penguin is of the species {species}")` 
  d.  `small_penguins %>% slice(6) %>% glue_data("This penguin is of the species {species}")` 


### Question 9 

Referring to the `small_penguins` data from Question 8, using only appropriate functions from the `stringr` package (i.e. no other explicit logical statements) and functions you are familiar with from the `tidyverse`, which of the following lines of code will correctly subset the data to include only female penguins? 

  a. `small_penguins %>% filter(str_remove(sex,"fe"))`  
  b. `small_penguins %>% filter(str_replace(sex,"fe", " "))`  
  c.  `small_penguins %>% filter(str_detect(sex,"fe"))`

### Question 10 

Referring once more to the `small_penguins` data. Which of the following lines of code will create a new variable called `island_short` with the name of the island shortened to `Torg`?  

  a. `small_penguins %>% filter(island_short = str_detect(island, "Torg"))`  
  b. `small_penguins %>% mutate(island_short = str_detect(island, "Torg"))`  
  c. `small_penguins %>% mutate(island_short = str_replace(island, "Torg", "ersen"))`  
  d.  `small_penguins %>% mutate(island_short = str_replace(island, "ersen", ""))`

