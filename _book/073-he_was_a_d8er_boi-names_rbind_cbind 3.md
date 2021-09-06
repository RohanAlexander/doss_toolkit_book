







# head, tail, glimpse and summary

*Written by Haoluan Chen.*

## Introduction

In this lesson, you will learn how to:

- Get an overview of your dataset using `head()`, `tail()`, `glimpse()`, and `summary()`

Prerequisite skills include:

- setup RStudio
- run R code in the console
- Install and load packages

Highlights:

- Using `head()`, `tail()`, `glance()`, and `summary()` to understand your dataset

After you load your dataset into R, you should start looking into the data to see what kinds of data you are working with.

Here are some useful functions that can help you to understand your dataset. 


## `head()`

The `head()` function takes in two parameters. The first parameter is the data frame, and the second parameter is the first number of rows you want to look at. (The "head" of your dataset.)


```r
head(mtcars, n = 3)
#>                mpg cyl disp  hp drat    wt  qsec vs am gear
#> Mazda RX4     21.0   6  160 110 3.90 2.620 16.46  0  1    4
#> Mazda RX4 Wag 21.0   6  160 110 3.90 2.875 17.02  0  1    4
#> Datsun 710    22.8   4  108  93 3.85 2.320 18.61  1  1    4
#>               carb
#> Mazda RX4        4
#> Mazda RX4 Wag    4
#> Datsun 710       1
```

Here I have set 'n' to 3, so we are looking at the first three rows of the mtcars dataset. 



## `tail()`

The `tail()` function also takes in two parameters. The first parameter is the data frame, and the second parameter is the last number of rows you want to look at. (The "tail" of your dataset.)



```r
tail(mtcars, n = 3)
#>                mpg cyl disp  hp drat   wt qsec vs am gear
#> Ferrari Dino  19.7   6  145 175 3.62 2.77 15.5  0  1    5
#> Maserati Bora 15.0   8  301 335 3.54 3.57 14.6  0  1    5
#> Volvo 142E    21.4   4  121 109 4.11 2.78 18.6  1  1    4
#>               carb
#> Ferrari Dino     6
#> Maserati Bora    8
#> Volvo 142E       2
```

Here I have set 'n' to 3, so we are looking at the last three row of the mtcars dataset. 

## `glimpse()`

The `glimpse()` function takes in one parameter, which is the data frame. This function can tell you the number of rows and columns for your dataset. Additionally, you can get the name, data type, and first few observations of each variable.  


```r
glimpse(mtcars)
#> Rows: 32
#> Columns: 11
#> $ mpg  <dbl> 21.0, 21.0, 22.8, 21.4, 18.7, 18.1, 14.3, 24.…
#> $ cyl  <dbl> 6, 6, 4, 6, 8, 6, 8, 4, 4, 6, 6, 8, 8, 8, 8, …
#> $ disp <dbl> 160.0, 160.0, 108.0, 258.0, 360.0, 225.0, 360…
#> $ hp   <dbl> 110, 110, 93, 110, 175, 105, 245, 62, 95, 123…
#> $ drat <dbl> 3.90, 3.90, 3.85, 3.08, 3.15, 2.76, 3.21, 3.6…
#> $ wt   <dbl> 2.620, 2.875, 2.320, 3.215, 3.440, 3.460, 3.5…
#> $ qsec <dbl> 16.46, 17.02, 18.61, 19.44, 17.02, 20.22, 15.…
#> $ vs   <dbl> 0, 0, 1, 1, 0, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, …
#> $ am   <dbl> 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
#> $ gear <dbl> 4, 4, 4, 3, 3, 3, 3, 4, 4, 4, 4, 3, 3, 3, 3, …
#> $ carb <dbl> 4, 4, 1, 1, 2, 1, 4, 2, 2, 4, 4, 3, 3, 3, 4, …
```

Here, we see that the table mtcars contains 32 rows and 11 columns of data. All of the variables in this table are double-precision floating-point number, because <dbl> represents the double data type.

## `summary()`

Next, you may want to look at the summary statistics of your data set. The function summary can produce the following summary statistics for each of the variables. 

- Min. : minimum value of the variable 
- 1st.Qu. : the first quartile of the variable
- Median: median of the variable
- Mean: mean of the variable
- 3rd Qu. : the third quartile of the variable
- Max. maximum value of the variable



```r
summary(mtcars)
#>       mpg             cyl             disp      
#>  Min.   :10.40   Min.   :4.000   Min.   : 71.1  
#>  1st Qu.:15.43   1st Qu.:4.000   1st Qu.:120.8  
#>  Median :19.20   Median :6.000   Median :196.3  
#>  Mean   :20.09   Mean   :6.188   Mean   :230.7  
#>  3rd Qu.:22.80   3rd Qu.:8.000   3rd Qu.:326.0  
#>  Max.   :33.90   Max.   :8.000   Max.   :472.0  
#>        hp             drat             wt       
#>  Min.   : 52.0   Min.   :2.760   Min.   :1.513  
#>  1st Qu.: 96.5   1st Qu.:3.080   1st Qu.:2.581  
#>  Median :123.0   Median :3.695   Median :3.325  
#>  Mean   :146.7   Mean   :3.597   Mean   :3.217  
#>  3rd Qu.:180.0   3rd Qu.:3.920   3rd Qu.:3.610  
#>  Max.   :335.0   Max.   :4.930   Max.   :5.424  
#>       qsec             vs               am        
#>  Min.   :14.50   Min.   :0.0000   Min.   :0.0000  
#>  1st Qu.:16.89   1st Qu.:0.0000   1st Qu.:0.0000  
#>  Median :17.71   Median :0.0000   Median :0.0000  
#>  Mean   :17.85   Mean   :0.4375   Mean   :0.4062  
#>  3rd Qu.:18.90   3rd Qu.:1.0000   3rd Qu.:1.0000  
#>  Max.   :22.90   Max.   :1.0000   Max.   :1.0000  
#>       gear            carb      
#>  Min.   :3.000   Min.   :1.000  
#>  1st Qu.:3.000   1st Qu.:2.000  
#>  Median :4.000   Median :2.000  
#>  Mean   :3.688   Mean   :2.812  
#>  3rd Qu.:4.000   3rd Qu.:4.000  
#>  Max.   :5.000   Max.   :8.000
```

What happens if you have other data types in your dataset? Here is a dataset called scores. It contains three variables student_ID, gender, and test_score. 



```r
scores <- tibble(student_ID = c("1", "2", "3", "4", "5", "6"),
                 gender = as.factor(c("male", "male", "male","female","female","female")),
               test_score = c(87, 76, 61, 80, 72, 69),
               )
scores
#> # A tibble: 6 × 3
#>   student_ID gender test_score
#>   <chr>      <fct>       <dbl>
#> 1 1          male           87
#> 2 2          male           76
#> 3 3          male           61
#> 4 4          female         80
#> 5 5          female         72
#> 6 6          female         69
```


```r
glimpse(scores)
#> Rows: 6
#> Columns: 3
#> $ student_ID <chr> "1", "2", "3", "4", "5", "6"
#> $ gender     <fct> male, male, male, female, female, female
#> $ test_score <dbl> 87, 76, 61, 80, 72, 69
```

Using the glimpse function, we know that student_ID is a character data type, gender is a factor data type, and test_score is a double data type.


```r
summary(scores)
#>   student_ID           gender    test_score   
#>  Length:6           female:3   Min.   :61.00  
#>  Class :character   male  :3   1st Qu.:69.75  
#>  Mode  :character              Median :74.00  
#>                                Mean   :74.17  
#>                                3rd Qu.:79.00  
#>                                Max.   :87.00
```

For character data type (student_ID), we see the length, class, and Mode of this variable. Length tells us the number of observations, class, and Mode tells us the data type. 

For factor data type(gender), we have the count of each factor. In this dataset, there are three female students and three male students. 

For double data type(test_score), we have the summary statistics as we have seen before. 

## Exercises

### Exercise 1


<!-- ```{r headex2, echo = FALSE} -->
<!-- question("If you want to look at the first 5 rows of the mtcars dataset, which code should you use?", -->
<!--           answer("head(mtcars,3)", correct = TRUE), -->
<!--           answer("tail(mtcars, 3)"), -->
<!--           answer("glimpse(mtcars)"), -->
<!--           answer("summary(mtcars)"), -->
<!--           allow_retry = TRUE) -->

<!-- ```  -->

<!-- ### Exercise 2 -->

<!-- ```{r summaryex, echo = FALSE} -->
<!-- question("What is the output of summary() function for factor data type?", -->
<!--           answer("Summary statistics such as min and max"), -->
<!--           answer("Data type"), -->
<!--           answer("Count of each factor", correct = TRUE), -->
<!--           answer("Number of factors in the variable"), -->
<!--           allow_retry = TRUE) -->

<!-- ```  -->

### Exercise 3

Here, we have a book dataset from Alex Cookson. This dataset contains 9,000 children's books that have been rated from 1-5 stars. Run the following code to your R and use the functions you learned in this tutorial to explore this dataset!


```r
books <- 
  read_tsv("https://raw.githubusercontent.com/tacookson/data/master/childrens-book-ratings/childrens-books.txt")
```


## Next Steps

Once you have fully understood the dataset you are working with you may start using plots to get a graphical representation of your dataset. You may like to read this chapter for more information: https://r4ds.had.co.nz/data-visualisation.html.














# `paste()`, `paste0()`, `glue::glue()` and `stringr`

*Written by Marija Pejcinovska*


## Introduction  

In this lesson we'll cover a couple of ways in which you can paste strings to your data. We'll use the `paste()` and `paste0()` functions, both of which are part of base R,  as well as the `glue()` function in the `glue` package. As part of this tutorial, you will also get a first taste of the `stringr` package, which is a wonderful tool for handling strings.  

Prerequisite skills:

- Exposure to most of the material in the yellow-level tutorials would be helpful.



## Paste strings and data with `paste()` and `paste0()`

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

Run the following code to see the difference between `paste` and `paste0`


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

paste(student, "collected", badges, "DoSS toolkit badges in the", term )
#> [1] "Rohan collected 2 DoSS toolkit badges in the Fall"   
#> [2] "Monica collected 4 DoSS toolkit badges in the Spring"
```


## "Gluing" your data with the `glue` package

The `glue` package is designed to make it easier to "stitch" or interpolate (or "glue") your data into strings. Its main function is quite similar in flavor to `paste()` (and `paste0()`), but a bit easier to use (this is especially true when compared to `sprintf()`; a function that we have not discussed here, but can similarly be used to concatenate strings and data).  

You can download `glue` the usual way you would install all your other packages, that is, by calling `install.packages("glue")`.

### The functions of `glue`
The glue package has three primary functions, `glue()`, `glue_data()` and `glue_collapse()`.   

The **`glue()` function** works a bit like the `paste()` function. In the case of `glue()`, however, we use `{}` to wrap the R code we wish to reference inside the string. This makes it a bit more manageable compared to all the quotation marks, commas, and separators we need to keep track of when using `paste()`.

Let's refer back to our example from earlier and check out the syntax for `glue()`. Note that now everything is placed inside a single set of quotation marks and R objects are referenced within the string by wrapping them up in curly brackets. 


```r
student <- c("Rohan", "Monica")
badges <- c(2,4)
term <- c("Fall", "Spring")

glue("{student} collected {badges} DoSS toolkit badges in {term}")
#> Rohan collected 2 DoSS toolkit badges in Fall
#> Monica collected 4 DoSS toolkit badges in Spring
```

Here we've called the R objects `student`, `badges`, and `term` by wrapping them up in `{}`. 

If you wish to use something other than `{}`, you can specify different opening and closing delimiters by using the `.open = ` and `.close = ` arguments in the `glue` function. For instance, let's surround the code we wish to evaluate by `<` at the beginning and `]` at the end.


```r
student <- c("Owen", "Monica")
badges <- c(2,4)
term <- c("Fall", "Spring")

glue("<student] collected <badges] DoSS toolkit badges in <term]", .open = "<", .close = "]")
#> Owen collected 2 DoSS toolkit badges in Fall
#> Monica collected 4 DoSS toolkit badges in Spring
```

The function **`glue_data()`** works much like `glue()` but it is designed to be used in piped chains (recall the pipe operator, ` %>% `). What's important to note here is that inside the curly braces we pass the column names of the columns in our data we wish to glue in some way (and not the name of the variables or R objects as we did with `glue()`). 

As an example run the following code. See what happens if you change `glue_data()` below with `glue()`.


```r

library(palmerpenguins)
# Check the data out
penguins %>% 
  head()
#> # A tibble: 6 × 8
#>   species island    bill_length_mm bill_depth_mm
#>   <fct>   <fct>              <dbl>         <dbl>
#> 1 Adelie  Torgersen           39.1          18.7
#> 2 Adelie  Torgersen           39.5          17.4
#> 3 Adelie  Torgersen           40.3          18  
#> 4 Adelie  Torgersen           NA            NA  
#> 5 Adelie  Torgersen           36.7          19.3
#> 6 Adelie  Torgersen           39.3          20.6
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


```r
glue_collapse({letters[1:3]}, sep = ", ", last = ", and ")
#> a, b, and c
```


## First taste of the `stringr` package

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

`str_replace()`, on the other hand, allows you to replace a matched pattern with an entirely new string (or an empty string, if what you  wish to do is remove the pattern; see also `str_remove()`). 

```r
my_vec 
#> [1] "r"             "R"             "I love R"     
#> [4] "why?"          "what is this?"

my_vec %>% 
  str_replace("\\?", " code")
#> [1] "r"                 "R"                
#> [3] "I love R"          "why code"         
#> [5] "what is this code"
```

The first argument is the pattern we are trying to find a match for (note that since ? is a special character we need to escape it by placing `\\` before `?`). The second argument here is the string we wish to replace our matched pattern with (in our case that's the string "code"). 

Let's see the `str_replace()` function applied to our penguins data. We'll use the function to slightly modify the name of an island


```r

penguins %>% 
  slice(1:4) %>% 
  mutate(new_island = str_replace(island, "Tor", "Mor"))
#> # A tibble: 4 × 9
#>   species island    bill_length_mm bill_depth_mm
#>   <fct>   <fct>              <dbl>         <dbl>
#> 1 Adelie  Torgersen           39.1          18.7
#> 2 Adelie  Torgersen           39.5          17.4
#> 3 Adelie  Torgersen           40.3          18  
#> 4 Adelie  Torgersen           NA            NA  
#> # … with 5 more variables: flipper_length_mm <int>,
#> #   body_mass_g <int>, sex <fct>, year <int>,
#> #   new_island <chr>
```


This is just a small slice of what the `stringr` package has to offer. Be on the lookout for future tutorials with more on strings and regular expressions. 


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




## Next Steps


This tutorial only briefly introduced you to the capabilities of the `stringr` package. Future tutorials will revisit this package and dive deeper into some of its functions. In the meantime, you can learn more about this package in Hadley Wickham's book *"R for Data Science"*. The link here takes you to the chapter on strings which also introduces you to regular expressions (regular expressions are a bit tedious, but you might learn to like them if you end up working with text data a lot). https://r4ds.had.co.nz/strings.html 











# `names()`, `rbind()` and `cbind()`

*Written by Isaac Ehrlich.*

## Introduction

For certain tasks, you may need to combine data frames and find information about them.

In this lesson, you will learn how to

* Use `names()` to find the column names of data frames
* Use `rbind()` to combine two or more data frames (or matrices) by row
* Use `cbind()` to combine two or more data frames (or matrices) by column

Prerequisites:

* Understanding how to data frames and their basic principles

## Arguments

### `names()`

The primary purpose of `names()` is to return the column names of a data frame. The only argument that `names()` takes is the data frame. `colnames()` is a similar function which outputs the same information, and works for matrices as well.


```r
head(starwars)
#> # A tibble: 6 × 14
#>   name           height  mass hair_color skin_color eye_color
#>   <chr>           <int> <dbl> <chr>      <chr>      <chr>    
#> 1 Luke Skywalker    172    77 blond      fair       blue     
#> 2 C-3PO             167    75 <NA>       gold       yellow   
#> 3 R2-D2              96    32 <NA>       white, bl… red      
#> 4 Darth Vader       202   136 none       white      yellow   
#> 5 Leia Organa       150    49 brown      light      brown    
#> 6 Owen Lars         178   120 brown, gr… light      blue     
#> # … with 8 more variables: birth_year <dbl>, sex <chr>,
#> #   gender <chr>, homeworld <chr>, species <chr>,
#> #   films <list>, vehicles <list>, starships <list>
names(starwars)
#>  [1] "name"       "height"     "mass"       "hair_color"
#>  [5] "skin_color" "eye_color"  "birth_year" "sex"       
#>  [9] "gender"     "homeworld"  "species"    "films"     
#> [13] "vehicles"   "starships"
table(colnames(starwars) == names(starwars))
#> 
#> TRUE 
#>   14
```

Using indexing, `names()` can also be used to change the column names of a data frame.


```r
# Change the homeworld column name (the tenth column) to home-planet
names(starwars)[10] <- "home-planet"
names(starwars)
#>  [1] "name"        "height"      "mass"        "hair_color" 
#>  [5] "skin_color"  "eye_color"   "birth_year"  "sex"        
#>  [9] "gender"      "home-planet" "species"     "films"      
#> [13] "vehicles"    "starships"
```

The tidyverse `rename()` function can also be used to change column names, and avoids indexing by specifying the column to rename, using the syntax `new_name = old_name`.


```r
# Change the starships column name to spaceships
starwars <- 
  starwars %>% 
  rename(spaceships = starships)
names(starwars)
#>  [1] "name"        "height"      "mass"        "hair_color" 
#>  [5] "skin_color"  "eye_color"   "birth_year"  "sex"        
#>  [9] "gender"      "home-planet" "species"     "films"      
#> [13] "vehicles"    "spaceships"
```
 

### `rbind()`

The purpose of `rbind()` is to combine two (or more) data frames by row. The arguments to `rbind()` are two (or more) data frames. These data frames must have the same number of columns, and must have the same column names as well. `rbind()` can also be used to combine matrices which match the same requirements.


```r
letter_df <- data.frame(numbers = 1:26, strings = letters)
words_df <- data.frame(numbers = 27:1006, strings = words)

character_df <- rbind(letter_df, words_df)
names(character_df)
#> [1] "numbers" "strings"
dim(character_df) # shows the number of rows and columns
#> [1] 1006    2
```

### `cbind()`

The purpose of `cbind()` is to combine two (or more) data frames by column. The arguments to `cbind()` are two (or more) data frames. These data frames must have the same number of rows, or the number of rows must be multiples of one another. `cbind()` can also be used to combine matrices which match the same requirements. 

Note, in the case that the number of rows are multiples, the rows in the smaller data frame are repeated so they match the longer data frame.


```r
index_df <- data.frame(numbers = 1:5, letters = c("a", "b", "c", "d", "e"))
names_df <- data.frame(vegetables = c("arugula", "broccoli", "cauliflower", "dill", "endive"),
                       fruits = c("apricot", "banana", "cherry", "date", "elderberry"),
                       flowers = c("aster", "begonia", "crocus", "daffodil", "echium"))

combined_df <- cbind(index_df, names_df)
names(combined_df)
#> [1] "numbers"    "letters"    "vegetables" "fruits"    
#> [5] "flowers"
dim(combined_df) # shows the number of rows and columns
#> [1] 5 5
```


## Questions and Exercises

### Question 1

Using the `presidential` data frame, save the column names, and then change the name of the second column to `inauguration-date`.


```
#> [1] "name"  "start" "end"   "party"
```


```r
presidential_col_names <- names(presidential)

names(presidential)[2] <- "inauguration-date"
```


### Question 2




<!-- ```{r rbind-q2, echo = FALSE} -->
<!-- question("If you were to rbind() a data frame to itself, ", -->
<!-- answer("the number of columns would double"), -->
<!-- answer("the number of rows would double", correct = TRUE), -->
<!-- answer("both the number of rows and the number of columns would double"), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

<!-- #### Question 3 -->

<!-- ```{r rbind-q3, echo = FALSE} -->
<!-- question("Select the following true statements about rbind() arguments", -->
<!-- answer("The data frames must have the same number of columns", correct = TRUE), -->
<!-- answer("The data frames must have the same number of rows"), -->
<!-- answer("The column names of the data frames must be the same", correct = TRUE), -->
<!-- answer("The data frames must have the same name"), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

<!-- #### Question 4 -->

<!-- Bind the `presidential` data set to itself using `rbind()`. -->

<!-- ```{r rbind-q4, echo = FALSE, exercise = TRUE} -->
<!-- # Enter your code below -->

<!-- # double_presidential <-  -->

<!-- dim(presidential) -->
<!-- # dim(double_presidential) -->
<!-- ``` -->

<!-- ```{r rbind-q4-solution} -->
<!-- double_presidential <- rbind(presidential, presidential) -->
<!-- ``` -->


<!-- #### Question 5 -->

<!-- ```{r cbind-q5, echo = FALSE} -->
<!-- question("If you were to cbind() a data frame to itself, ", -->
<!-- answer("the number of columns would double", correct = TRUE), -->
<!-- answer("the number of rows would double"), -->
<!-- answer("both the number of rows and the number of columns would double"), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

<!-- #### Question 6 -->

<!-- Bind the `presidential` data set to itself using `cbind()`. -->

<!-- ```{r cbind-q6, echo = FALSE, exercise = TRUE} -->
<!-- # Enter your code below -->

<!-- double_presidential <- -->

<!-- dim(presidential) -->
<!-- # dim(double_presidential) -->
<!-- ``` -->

<!-- ```{r cbind-q6-solution} -->
<!-- double_presidential <- cbind(presidential, presidential) -->
<!-- ``` -->

## Special Cases & Common Mistakes

The most common error with `rbind()` and `cbind()` occurs when the data frames do not meet the requirements (e.g. data frames have different number of columns for `rbind()` or different number of rows for `cbind()`). These will result in error messages such as "numbers of columns of arguments do not match" or "arguments imply differing number of rows". 

Similarly, if the names of the columns do not match, `rbind()` will give a "names do not match previous names" error. You can use `names()` to check against this error.


## Overview & Next Steps

`names()` will return the column names of data frames and can be used to change column names as well. `rbind()` and `cbind()` combine data frames either by row or by column.

In the next section, we will continue learning how to manipulate data frames.












# `left_join()`, `anti_join()`, `full_join()`, etc

*Written by Haoluan Chen.*

## Introduction

In this lesson, you will learn how to:

- Join two tables by using `left_join()`, `right_join()`, `full_join()`, `inner_join` and `anti_join()`

Prerequisite skills include:

- Install and load dplyr package

Highlights:

- Learn how two join two tables  

Sometimes you may want to combine two data frames into a single table. Here we have one table which contains data such as the student id and their grade. And we have another table that includes demographic information about the student.


```r
test_score <- tribble(~student_id, ~grade
                  ,'1',  94
                  ,'2',  90
                  ,'3',  88
                  ,'4',  75
                  ,'5',  66
                  )
student_info <- tribble(~student_id, ~age,~gender
                  ,'1', 18, 'F'
                  ,'2', 20, 'F'
                  ,'4', 25, 'M'
                  ,'6', 21, 'M'
                  ,'7', 23, 'F'
                  )
test_score
#> # A tibble: 5 × 2
#>   student_id grade
#>   <chr>      <dbl>
#> 1 1             94
#> 2 2             90
#> 3 3             88
#> 4 4             75
#> 5 5             66
student_info
#> # A tibble: 5 × 3
#>   student_id   age gender
#>   <chr>      <dbl> <chr> 
#> 1 1             18 F     
#> 2 2             20 F     
#> 3 4             25 M     
#> 4 6             21 M     
#> 5 7             23 F
```

Using `dplyr` within R, we can easily import our data and join these tables, using the following join types.

- Left Join (`left_join()`)
- Right Join (`right_join()`)
- Full Join (`full_join()`)
- Inner Join (`inner_join()`)
- Anti Join (`anti_join()`)

The general syntax of these joins is as follows:

join_type(firstTable, secondTable, by=columnTojoinOn)

We'll now run through an example of using each of these join types on our two tables.


## `left_join()`

`left_join()` will take all of the values from the table we specify as left (e.g., the first one) and match them to records from the table on the right (e.g., the second one) by the variable we specified. If there is no match in the second table, it will show NULL for the values in the second table. For example, if we left joined 'test_score' to 'student_info', our data would look as follows:


```r
leftJoinDf <- 
  left_join(test_score,student_info, by='student_id')

leftJoinDf
#> # A tibble: 5 × 4
#>   student_id grade   age gender
#>   <chr>      <dbl> <dbl> <chr> 
#> 1 1             94    18 F     
#> 2 2             90    20 F     
#> 3 3             88    NA <NA>  
#> 4 4             75    25 M     
#> 5 5             66    NA <NA>
```


## `right_join()`

One of the easiest ways to consider a right join is the opposite of a left join! In this instance, the table specified second within the join statement will be the one that the new table takes all of its values from. If there is no match in the first table (the table specified first in the argument), it will return NULL for the values in the first table that did not find a match. In this instance, if we right joined student_info to test_score, our data would look as follows:


```r
rightJoinDf <- right_join(test_score,student_info,by='student_id')
rightJoinDf
#> # A tibble: 5 × 4
#>   student_id grade   age gender
#>   <chr>      <dbl> <dbl> <chr> 
#> 1 1             94    18 F     
#> 2 2             90    20 F     
#> 3 4             75    25 M     
#> 4 6             NA    21 M     
#> 5 7             NA    23 F
```

## `full_join()`

The full join returns all of the data in a new table, whether it matches on either the left or right tables. If the specified variable match on two tables, then a join will be executed. Otherwise, it will return NULL in places where a matching row does not exist.


```r
FullJoinDf <- full_join(test_score,student_info,by='student_id')
FullJoinDf
#> # A tibble: 7 × 4
#>   student_id grade   age gender
#>   <chr>      <dbl> <dbl> <chr> 
#> 1 1             94    18 F     
#> 2 2             90    20 F     
#> 3 3             88    NA <NA>  
#> 4 4             75    25 M     
#> 5 5             66    NA <NA>  
#> 6 6             NA    21 M     
#> 7 7             NA    23 F
```

## `inner_join()`

inner_join creates a new table that only contains matched rows in both tables. 
For example, if we decided to join by student_id, the new table would contain rows 1 and 2:


```r
InnerJoinDf <- inner_join(test_score,student_info,by='student_id')
InnerJoinDf
#> # A tibble: 3 × 4
#>   student_id grade   age gender
#>   <chr>      <dbl> <dbl> <chr> 
#> 1 1             94    18 F     
#> 2 2             90    20 F     
#> 3 4             75    25 M
```

## `anti_join()`

An anti join will return all of the rows from the first table where there are no matching values from the second.

An example of this is shown below:


```r
AntiJoinDf <- anti_join(test_score,student_info,by='student_id')
AntiJoinDf
#> # A tibble: 2 × 2
#>   student_id grade
#>   <chr>      <dbl>
#> 1 3             88
#> 2 5             66
```





## Exercises


```r
test_score <- tribble(~student_id, ~grade
                  ,'1',  94
                  ,'2',  90
                  ,'3',  88
                  ,'4',  75
                  ,'5',  66
                  )
student_info <- tribble(~student_id, ~age,~gender
                  ,'1', 18, 'F'
                  ,'3', 20, 'F'
                  ,'5', 25, 'M'
                  ,'7', 21, 'M'
                  ,'9', 23, 'F'
                  )
test_score
#> # A tibble: 5 × 2
#>   student_id grade
#>   <chr>      <dbl>
#> 1 1             94
#> 2 2             90
#> 3 3             88
#> 4 4             75
#> 5 5             66
student_info
#> # A tibble: 5 × 3
#>   student_id   age gender
#>   <chr>      <dbl> <chr> 
#> 1 1             18 F     
#> 2 3             20 F     
#> 3 5             25 M     
#> 4 7             21 M     
#> 5 9             23 F
```

### Exercises 1

<!-- ```{r joinex2, echo = FALSE} -->
<!-- question("Which set of student id is in the output of left_join(test_score, student_info)", -->
<!--           answer("1, 2, 3, 4, 5", correct = TRUE), -->
<!--           answer("1, 3, 5"), -->
<!--           answer("7, 9"), -->
<!--           answer("1, 2, 3, 4, 5, 7, 9"), -->
<!--           allow_retry = TRUE) -->

<!-- ```  -->

<!-- ### Exercises 2 -->

<!-- ```{r joinex3, echo = FALSE} -->
<!-- question("Which set of student id is in the output of right_join(test_score, student_info)", -->
<!--           answer("1, 3, 5"), -->
<!--           answer("7, 9"), -->
<!--           answer("1, 3, 5, 7, 9", correct = TRUE), -->
<!--           answer("1, 2, 3, 4, 5, 7, 9"), -->
<!--           allow_retry = TRUE) -->

<!-- ```  -->

<!-- ### Exercises 3 -->

<!-- ```{r joinex4, echo = FALSE} -->
<!-- question("Which set of student id is in the output of inner_join(test_score, student_info)", -->
<!--           answer("1, 3, 5", correct = TRUE), -->
<!--           answer("7, 9"), -->
<!--           answer("1, 3, 5, 7, 9"), -->
<!--           answer("1, 2, 3, 4, 5, 7, 9"), -->
<!--           allow_retry = TRUE) -->

<!-- ```  -->


<!-- ### Exercises 4 -->

<!-- ```{r joinex5, echo = FALSE} -->
<!-- question("Which set of student id is in the output of full_join(test_score, student_info)", -->
<!--           answer("1, 3, 5"), -->
<!--           answer("7, 9"), -->
<!--           answer("1, 3, 5, 7, 9"), -->
<!--           answer("1, 2, 3, 4, 5, 7, 9", correct = TRUE), -->
<!--           allow_retry = TRUE) -->

<!-- ```  -->


## Common Mistakes & Errors

- Make sure there is at least one common variable in the tables you are joining.
- Think about how you want to join the table and use the appropriate join function.

## Next Steps

You can read through R for Data Science Chapter 13 Relational(working with multiple tables) data (https://r4ds.had.co.nz/relational-data.html) for a more detailed explanation and visualization. 

Here is the documentation for all the joins function in dplyr package: https://dplyr.tidyverse.org/reference/join.html














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
#>  1          1 STA130    86
#>  2          1 CSC108    85
#>  3          1 MAT137    88
#>  4          2 STA130    76
#>  5          2 CSC108    75
#>  6          3 STA130    78
#>  7          4 STA130    84
#>  8          4 CSC108    78
#>  9          4 MAT137    78
#> 10          5 STA130    76
#> 11          5 MAT137    75
#> 12          6 MAT137    76
```

As you can see, our data is missing some rows that would correspond to courses that 
students have yet to complete. Suppose, for some reason, that you want to count the number 
of courses that are left for all students to take until they have completed all their 
requirements, or maybe you want to try predicting the grades a student will get on their 
remaining courses. Regardless, you will need to "manipulate" this data set to make it so 
that you can see which courses students have yet to complete. The `complete()` function is 
right tool to do this and we can do this as follows.



<pre><code class='language-r'><code>first_year %>%<br>&nbsp;&nbsp;<span style='color:hotpink'>complete</span>(student_id, course)<br>#> # A tibble: 18 × 3<br>#> &nbsp;&nbsp;&nbsp;student_id course grade<br>#> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<dbl> <chr> &nbsp;<dbl><br>#> &nbsp;1 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1 CSC108 &nbsp;&nbsp;&nbsp;85<br>#> &nbsp;2 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1 MAT137 &nbsp;&nbsp;&nbsp;88<br>#> &nbsp;3 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1 STA130 &nbsp;&nbsp;&nbsp;86<br>#> &nbsp;4 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2 CSC108 &nbsp;&nbsp;&nbsp;75<br>#> &nbsp;5 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2 MAT137 &nbsp;&nbsp;&nbsp;NA<br>#> &nbsp;6 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2 STA130 &nbsp;&nbsp;&nbsp;76<br>#> &nbsp;7 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3 CSC108 &nbsp;&nbsp;&nbsp;NA<br>#> &nbsp;8 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3 MAT137 &nbsp;&nbsp;&nbsp;NA<br>#> &nbsp;9 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3 STA130 &nbsp;&nbsp;&nbsp;78<br>#> 10 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;4 CSC108 &nbsp;&nbsp;&nbsp;78<br>#> 11 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;4 MAT137 &nbsp;&nbsp;&nbsp;78<br>#> 12 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;4 STA130 &nbsp;&nbsp;&nbsp;84<br>#> 13 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5 CSC108 &nbsp;&nbsp;&nbsp;NA<br>#> 14 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5 MAT137 &nbsp;&nbsp;&nbsp;75<br>#> 15 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;5 STA130 &nbsp;&nbsp;&nbsp;76<br>#> 16 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;6 CSC108 &nbsp;&nbsp;&nbsp;NA<br>#> 17 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;6 MAT137 &nbsp;&nbsp;&nbsp;76<br>#> 18 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;6 STA130 &nbsp;&nbsp;&nbsp;NA</code></code></pre>

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













# `set.seed()`, `runif()`, `rnorm()`, and `sample()`

*Written by Haoluan Chen.*


## Introduction


In this lesson, you will learn how to:

- Generate numbers from a uniform distribution or normal distribution 
- Sample from a collection of numbers

Prerequisite skills include:

- Run code in R
- Basic knowledge of uniform distribution and normal distribution and sampling

Highlights:

- Generate random value from a uniform distribution and normal distribution
- Generate random value from a set
- `set.seed()` for reproducibility 


## The content


Simulation is an important topic in statistics because it helps you understand how random data might be generated. For some experiments, you may want to simulate values from probability distributions. In R, we can use `runif()` and `rnorm()` function to generate random number from uniform distribution or normal distributionr. Also, we can randomly sample from a set of numbers by using the `sample()` function. 

### runif()


The `runif()` function generate random numbers from a uniform distribution.  

#### Arguments

It takes in three parameters: `n`, `min` and `max`. The parameter `n` specifies the number of random values you want to generate. The parameter `min` and `max` specify the range of the uniform distribution. The default of min and max are 0 and 1.

Arguments | What does it mean
------------- | -------------
n (required) | number of random values you want to generate (numeric)
min (optional) | the minimum value of the uniform distribution you are sampling from (numeric)
max (optional)| the maximum value of the uniform distribution you are sampling from (numeric)


#### Example



```r
runif(n = 3)
#> [1] 0.5555288 0.2072858 0.4850260
```
The above code means to generate three random numbers from unif(0,1) where unif is a uniform distribution with a minimum value of 0 and maximum value of 1.

What if you want to generate number from `unif(2,8)` uniformly?

In `runif()` function, we can specify the min and max to be 2 and 8 to generate three numbers from unif(2,8):


```r
runif(n = 3, min = 2, max = 8)
#> [1] 7.361089 4.075998 7.155979
```

### rnorm()


In R, we can use `rnorm()` function to generate numbers from a normal distribution. 

#### Arguments

It takes in three parameters: `n`, `mean`, and `sd`. The parameter `n` specifies the number of random values you want to generate. The parameter `mean` and `sd` specifies the mean and standard deviation of the normal distribution you wish to sample. The default of `mean` and `sd` are 0 and 1.

Arguments | What does it mean
------------- | -------------
n (required) | number of random values you want to generate (numeric)
mean (optional) | the mean value of the normal distribution you are sampling from (numeric)
sd (optional)| the standard deviation of the normal distribution you are sampling from (numeric)

#### Example

Let's say we want to generate 5 random number from a normal distribution with `mean = 0` and `sd = 2`.


```r
rnorm(n = 5, sd = 2)
#> [1] -0.6660864 -1.6968260  2.4074416  1.3968147 -1.6857693
```

Here, we set the `n` to be 5 and `sd` to be 2, because we want to generate five random numbers from a normal distribution with a standard deviation of 2. We do not have to specify the mean value here because the default of the mean parameter is 0, which is exactly what we want. 

What if we want to generate 5 number from normal(10,2)?


```r
rnorm(n = 5, mean = 10, sd = 2)
#> [1] 11.978603 12.571888 11.315085 10.714173  9.733362
```
Here, we generated 5 numbers from normal(10,2) distribution.

### sample()

In R, we can using `sample()` to randomly sample numbers from a collection of numbers. 

#### Arguments

It takes in three parameters: x, size, and replace. The x is the vector of one or more elements that you wish to sample. The parameter size specifies the number of random values you want to generate. The parameter replace is a logical variable; true if you want to sample with replacement. 

When replace is set to true, you will be sampling from the same set of numbers for each generation. When replace is set to false, every time you sample a number, it will be taken out of the vector x for the next number generation. 

Arguments | What does it mean
------------- | -------------
x (required) | vector of one or more elements that you are sampling from
size (required) | number of random values you want to generate (numeric)
replace (optional)| true if you want to sample with replacement (logical)
prob (optional) | a vector of probability weights for obtaining the elements of the vector being sampled.

#### Examples




Here, we have a vector containing 6 numbers to simulate rolling dice. Let's roll the dice 6 times and see what we get:



```r
x <- c(1, 2, 3, 4, 5, 6)
set.seed(2)
sample(x = x, size = 6, replace = TRUE)
#> [1] 5 6 6 1 5 1
```

**Don't worry about set.seed(1), you will learn in this tutorial!**
What if we set the replace to `FALSE`? 



```r
set.seed(1)
sample(x = x, size = 6, replace = FALSE)
#> [1] 1 4 3 6 2 5
```

As we see that when `replace = TRUE`, we obtain repeated sample of 6 and 1. However, when `replace = FALSE`, there is no repeated sample in the output. 

When setting the replace to `FALSE`, the numbers are taken out for each round of sampling. Here, our first number is 5, which means that the second number will only be a sample from the set {2,3,4,5,6}. The 1 will be taken out of the vector for this sampling process. So, that is why we always get each number to appear once in the simulation.  

Using the prob argument, we can assign the probability of each elements the vector being sampled.
For example, for a unfair dice, The probability of getting a 6 is 40% and the probability of getting any other number are 12%. We may simulate this unfair dice using sample() function and setting the prob argument. 


```r
set.seed(2)
sample(x = x, size = 6, replace = TRUE, prob = c(0.12, 0.12, 0.12, 0.12, 0.12, 0.4))
#> [1] 6 5 4 6 1 1
```



### set.seed()




Let's run our dice simulation twice and see what happens (run the following code twice)


```r
x <- c(1, 2, 3, 4, 5, 6)
sample(x = x, size = 6, replace = TRUE)
#> [1] 4 6 6 3 5 5
```

We get different results every time we run the simulation, because we randomly sampled from 1-6 with replacement. What if you want to reuse the result from one simulation? Sometimes you do not want your result to change every time you run the function. This is what `set.seed()` does. 

When you use `set.seed()` function before your simulation, the simulation output will be the same every time. 

#### Arguments


The `set.seed()` function takes in a number, and it can be any number.

#### Example


Let's use `set.seed()` before we do the dice simulation

Please run the following code twice. 


```r
set.seed(2)
x <- c(1, 2, 3, 4, 5, 6)
sample(x = x, size = 6, replace = TRUE)
#> [1] 5 6 6 1 5 1
```

This also works for `runif()`, `rnorm()` and other simulation functions. Once you use `set.seed()` your simulation will always produce the same result. 

## Exercises


### Exercise 1


Please generate 10 random values from unif(-1,1) 



### Exercise 2

Please generate 10 random values from normal(0,5)



### Exercise 3


<!-- ```{r exercise3, echo = FALSE} -->
<!-- question("Which of the following code simulates rolling a fair dice 5 times?", -->
<!--           answer("sample(c(1, 2, 3, 4, 5, 6), 5, replace = TRUE)", correct = TRUE), -->
<!--           answer("sample(c(1, 2, 3, 4, 5, 6), 5, replace = FALSE)"), -->
<!--           answer("sample(c(1, 2, 3, 4, 5, 6), 5)"), -->
<!--           answer("runif(5, 1, 6)"), -->
<!--           allow_retry = TRUE) -->

<!-- ``` -->

<!-- ### Exercise 4 -->


<!-- Please generate 10 random values from normal(10,5) and calculate the mean. -->
<!-- ```{r exercise4, exercise=TRUE, exercise.lines = 2} -->

<!-- ``` -->

<!-- ### Exercise 5 -->


<!-- Please generate 1000 random values from normal(10,5) and calculate the mean.  -->
<!-- ```{r exercise5, exercise=TRUE, exercise.lines = 2} -->

<!-- ``` -->

<!-- ### Exercise 6 -->


<!-- Run your code from exercise 4 and 5 few times and compare the results, what did you notice? -->

<!-- ```{r exercise6} -->

<!-- ``` -->


<!-- ### Exercise 7 -->


<!-- ```{r exercise7, echo = FALSE} -->
<!-- question("How would you ensure that the simulations in Exercises 4 and 5 give the same result every time?", -->
<!--           answer("You do not have to do anything, the simulation result will always be the same"), -->
<!--           answer("Use set.seed() function before you run the simulation", correct = TRUE), -->
<!--           answer("Set the set.seed parameter to TRUE"), -->
<!--           answer("Use sample() function instead of rnorm"), -->
<!--           allow_retry = TRUE) -->

<!-- ``` -->


![Exercise 1 & 2](https://youtu.be/2HMfMnvSVkg)
![Exercise 4 & 5 & 6](https://youtu.be/HJtZfqgc6fY)


## Common Mistakes & Errors


- Make sure you have input parameter in the right order!

## Next Steps


Sometimes you need to do additional things to make your simulated more similar to your data. You can take a look on this book: R Programming for Data Science: https://bookdown.org/rdpeng/rprogdatascience/simulation.html. It has videos that explains simulation concepts and simulating a linear model. 

You can also generate binomial random variables using `rbinom()`, and Poisson random variables using `rpois()`, among others!
















# Simulating datasets for regression

*Written by Mariam Walaa.*

## Introduction

In this lesson, you will learn how to:

- Simulate data for regression 

Prerequisite skills include:

- Familiarity with `set.seed()`, `runif()`, `rnorm()`, `sample()` 

Highlights

- We can recover the linear regression model from simulated data

## Overview

In the previous section, we learned about how to simulate data. We can build
regression models from this simulated data. However, another thing we can do with these
functions is build simulated data _for_ regression models.

For example, suppose you were not given a data set but instead was told of the
distributions of some variables and given their coefficients for a linear regression
model. We can use this information to _create_ the simulated data.

## Idea
*Written by Michael Chong*

To simulate a data set, try writing it down on paper first, and then
think about which parts are random, then translate it to code! For example, if you think
some number $y$ is related *linearly* to $x$ with a slope of 0.3, with some random
measurement error, you could write it down on paper like this:

$$
y = 0.3\cdot x + error
$$

Translating it to code might look like:


```r
x <- 2 # set some value of x
measurement_error <- rnorm(1) # normally distributed measurement error

y <- 0.3*x + rnorm(1) # calculate value of y
```

## Example

Suppose we are given distributions of weights and heights for a population of 50 people, 
and a linear regression equation for this data, which is the slope and intercept. We can 
then use this information to simulate the data _from_ the slope and intercept. Lets start 
with loading the tidyverse.


```r
library(tidyverse)
```

We can simulate the data as follows.



<pre><code class='language-r'><code>set.seed(2)<br><br>data <- tibble(weight = rnorm(n = 50, mean = 125, sd = 5),<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;error = rnorm(n = 50, mean = 0, sd = 1),<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style='color:hotpink'>height = weight * 1.2 + error</span>)</code></code></pre>

Lets see what this relationship looks like with the regression line and data points plotted.


```r
data %>% 
  ggplot(aes(x = weight, y = height)) +
  geom_point() + 
  geom_smooth(method = "lm", se = FALSE, formula = 'y ~ x')
```

<img src="073-he_was_a_d8er_boi-names_rbind_cbind_files/figure-html/simulating-data-5-1.png" width="672" />

We may use this data set to build a regression models using the `lm()` function as follows.


```r
lm(height ~ weight, data = data)
#> 
#> Call:
#> lm(formula = height ~ weight, data = data)
#> 
#> Coefficients:
#> (Intercept)       weight  
#>      0.9387       1.1915
```

As we expect, building this linear regression model successfully recovers the original
slope of 1.2.

## Exercises

There are many functions involved when it comes to trying to simulate a data set. These
exercises will help you better learn which functions to use for which parts of the
simulation.

### Exercise 1

When simulating a data set, you will likely need to work with various types of variables
-- continuous variables, discrete variables, numeric variables, and non-numeric variables.

When it comes to discrete variables (whether numeric, non-numeric, or a mix of both), you
will likely want to see a repetition of a finite set of values. There is a certain
function out of the handful of functions we learned about for simulating datasets that
will be helpful for this task.

For this exercise, youll try to simulate data points for a discrete variable representing
the number of times you might pick out a red ball from a jar full of blue, red, and yellow
balls. Suppose youll pick out a ball 10 times and put it back every time, and that each
ball has equal probability of being picked.

Fill in the blanks for the code below to create data that represents the above scenario.



<pre><code class='language-r'><code>sample(<span style='background-color:#ffff7f'> </span> = c("Red", "Blue", "Yellow"),<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style='background-color:#ffff7f'> &nbsp;&nbsp;&nbsp;</span> = 10,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style='background-color:#ffff7f'> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>= TRUE,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style='background-color:#ffff7f'> &nbsp;&nbsp;&nbsp;</span> = c(0.33, 0.33, 0.33))</code></code></pre>

You'll notice that there are 4 blanks in total that you'll need to fill.

<!-- ```{r simulate-fill-in-sample-2, echo = FALSE} -->
<!-- quiz(question("What should the first blank be?", -->
<!--               answer("n"), -->
<!--               answer("x", correct = TRUE), -->
<!--               answer("c"), -->
<!--               answer("size"), -->
<!--               answer("replace"), -->
<!--               answer("prob"), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("What should the second blank be?", -->
<!--               answer("n"), -->
<!--               answer("x"), -->
<!--               answer("c"), -->
<!--               answer("size", correct = TRUE), -->
<!--               answer("replace"), -->
<!--               answer("prob"), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("What should the third blank be?", -->
<!--               answer("n"), -->
<!--               answer("x"), -->
<!--               answer("c"), -->
<!--               answer("size"), -->
<!--               answer("replace", correct = TRUE), -->
<!--               answer("prob"), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("What should the fourth blank be?", -->
<!--               answer("n"), -->
<!--               answer("x"), -->
<!--               answer("c"), -->
<!--               answer("size"), -->
<!--               answer("replace"), -->
<!--               answer("prob", correct = TRUE), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE)) -->
<!-- ``` -->

### Exercise 2

Suppose we are given a regression model with a slope of 1.2, and we want to simulate a 
dataset from the regression model similar to the previous scenario. We have the below code
to generate the data. What is wrong with this data-generating code below?

<!-- ```{r simulate-data-exercise-2, exercise = TRUE, exercise.eval = TRUE} -->
<!-- set.seed(2) -->
<!-- data <- tibble(weight = rnorm(n = 50, mean = 125, sd = 5), -->
<!--                height = rnorm(n = 50, mean = 150, sd = 4)) -->
<!-- ``` -->

<!-- ```{r simulate-data-exercise-2-hint-1} -->
<!-- # It works in the sense that we get meaningful output, but it is not the output we want for this problem -->
<!-- ``` -->
<!-- ```{r simulate-data-exercise-2-hint-2} -->
<!-- # If you are stuck, try looking at the code we used for this above, and determine what's different -->
<!-- ``` -->

<!-- ```{r simulate-data-exercise-2-solution, exercise = FALSE} -->
<!-- set.seed(2) -->
<!-- data <- tibble(weight = rnorm(n = 50, mean = 125, sd = 5), -->
<!--                error = rnorm(n = 50, mean = 0, sd = 1), -->
<!--                height = weight * 1.2 + error) -->
<!-- ``` -->

## Common Mistakes & Errors

Here are some common mistakes and errors you may come across:

- You may be confusing some of the arguments for different distribution functions. Make
sure youre using `runif()` to sample points from the _uniform_ distribution and `rnorm()`
to sample points from the _normal_ distribution.
- You may be misusing some of the arguments for a function like `sample()`. Make sure you
read the argument descriptions as well as the given examples in the documentation.
- You may forget to set the seed before running a chunk of code, or you may be using a
different value for a seed to obtain results you previously got with your code.

## Next Steps

If you would like to learn more about these functions, read the documentation associated
with each of the functions. But if you would like to learn more about simulating datasets
from a regression model, please take a look at the following:

- [Telling Stories With Data -- Its Just a Linear Model](https://www.tellingstorieswithdata.com/its-just-a-linear-model.html#overview)

















# Conditional mutating and summarising

*Written by Mariam Walaa.*

## Introduction

In this lesson, you will learn how to:

- Use across() with summarise() 
- Use mutate_if() 
- Use if_else() and na_if() 

Prerequisite skills include:

- Familiarity with summarize() and mutate()
- Familiarity with conditional statements if_else()

Highlights:

- Use across() to summarize across a defined selection of columns
- Mutate column types based on conditions using mutate_if()
- Mutate columns based on conditions using if_else() and na_if() within mutate()

## Overview

This section will demonstrate how to use the `summarise()` function with `across()` to 
summarize variables and groups within a variable in a data set. We will be looking at a
data set of Broadway shows with variables about the performances, attendance, and revenue
for theaters that are part of The Broadway League. You can learn more about the data set
provided by Alex Cookson in [the dataset repository](https://github.com/tacookson/data) as
well as this corresponding [blog
post](https://www.alexcookson.com/post/most-successful-broadway-show-of-all-time/).

### Video

![](https://youtu.be/3mmbPjgzzeY)

## Questions

Lets start with loading the tidyverse and looking at the data.


```r
library(tidyverse)
```


```r
broadway
#> # A tibble: 47,524 × 8
#>    week_ending show   theatre  weekly_gross avg_ticket_price
#>    <date>      <chr>  <chr>           <dbl>            <dbl>
#>  1 1985-06-09  42nd … St. Jam…       282368             30.4
#>  2 1985-06-09  A Cho… Sam S. …       222584             27.2
#>  3 1985-06-09  Aren'… Brooks …       249272             33.8
#>  4 1985-06-09  Arms … Circle …        95688             20.9
#>  5 1985-06-09  As Is  Lyceum …        61059             20.8
#>  6 1985-06-09  Big R… Eugene …       255386             32.0
#>  7 1985-06-09  Bilox… Neil Si…       306839             28.3
#>  8 1985-06-09  Brigh… 46th St…       107392             18.9
#>  9 1985-06-09  Cats   Winter …       461880             38.4
#> 10 1985-06-09  Doubl… Ritz Th…        47452             17.5
#> # … with 47,514 more rows, and 3 more variables:
#> #   top_ticket_price <dbl>, performances <dbl>,
#> #   previews <dbl>
```

### Question 1

What is the minimum and maximum number of performances _and_ previews per week? We can use
`across()` to select specific columns to summarize them with multiple summary functions.



<pre><code class='language-r'><code>broadway %>%<br>&nbsp;&nbsp;group_by(week_ending) %>%<br>&nbsp;&nbsp;summarise(<span style='color:blue'>across</span>(<span style='color:deeppink'>.cols</span> = c("performances", "previews"),<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style='color:orange'>.fns</span> = list(min = min, max = max)),<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.groups = 'drop')<br>#> # A tibble: 1,812 × 5<br>#> &nbsp;&nbsp;&nbsp;week_ending performances_min performances_max<br>#> &nbsp;&nbsp;&nbsp;<date> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<dbl> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<dbl><br>#> &nbsp;1 1985-06-09 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> &nbsp;2 1985-06-16 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8<br>#> &nbsp;3 1985-06-23 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> &nbsp;4 1985-06-30 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> &nbsp;5 1985-07-07 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;7 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> &nbsp;6 1985-07-14 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> &nbsp;7 1985-07-21 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> &nbsp;8 1985-07-28 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> &nbsp;9 1985-08-04 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> 10 1985-08-11 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;8 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;9<br>#> # … with 1,802 more rows, and 2 more variables:<br>#> # &nbsp;&nbsp;previews_min <dbl>, previews_max <dbl></code></code></pre>

Here is what the above chunk of code does:

* Groups the data by week using `group_by()` 
* Selects columns to summarize by passing a vector to `.cols` in `across()` (Highlighted in pink) 
* Defines summary functions by passing a list to `.fns` in `across()` (Highlighted in orange)

You can also learn more about `across()` by running `?across` in your console.

### Question 2

How do we provide a numeric summary for every show happening in a particular week?


```r
broadway %>%
  group_by(week_ending, show) %>%
  summarise(across(where(is.numeric), mean, na.rm = TRUE),
            .groups = 'drop')
#> # A tibble: 47,524 × 7
#>    week_ending show                   weekly_gross avg_ticket_price
#>    <date>      <chr>                         <dbl>            <dbl>
#>  1 1985-06-09  42nd Street                  282368             30.4
#>  2 1985-06-09  A Chorus Line                222584             27.2
#>  3 1985-06-09  Aren't We All?               249272             33.8
#>  4 1985-06-09  Arms and the Man              95688             20.9
#>  5 1985-06-09  As Is                         61059             20.8
#>  6 1985-06-09  Big River                    255386             32.0
#>  7 1985-06-09  Biloxi Blues                 306839             28.3
#>  8 1985-06-09  Brighton Beach Memoirs       107392             18.9
#>  9 1985-06-09  Cats                         461880             38.4
#> 10 1985-06-09  Doubles                       47452             17.5
#> # … with 47,514 more rows, and 3 more variables:
#> #   top_ticket_price <dbl>, performances <dbl>,
#> #   previews <dbl>
```

This chunk of code summarizes every show happening in some particular week by every
numeric variable that is available in the data set. This helps us compute things like
the average ticket price and the number of performances each show had in a particular
week.

### Question 3

We can use mutate() and if_else() to change values within a column. For example, here
is what we would write if we wanted to change all rows with theatre Studio 54 to be 
called Studio 54 Theatre.


```r
broadway %>% 
    mutate(theatre = if_else(theatre == "Studio 54", "Studio 54 Theatre", theatre))
#> # A tibble: 47,524 × 8
#>    week_ending show   theatre  weekly_gross avg_ticket_price
#>    <date>      <chr>  <chr>           <dbl>            <dbl>
#>  1 1985-06-09  42nd … St. Jam…       282368             30.4
#>  2 1985-06-09  A Cho… Sam S. …       222584             27.2
#>  3 1985-06-09  Aren'… Brooks …       249272             33.8
#>  4 1985-06-09  Arms … Circle …        95688             20.9
#>  5 1985-06-09  As Is  Lyceum …        61059             20.8
#>  6 1985-06-09  Big R… Eugene …       255386             32.0
#>  7 1985-06-09  Bilox… Neil Si…       306839             28.3
#>  8 1985-06-09  Brigh… 46th St…       107392             18.9
#>  9 1985-06-09  Cats   Winter …       461880             38.4
#> 10 1985-06-09  Doubl… Ritz Th…        47452             17.5
#> # … with 47,514 more rows, and 3 more variables:
#> #   top_ticket_price <dbl>, performances <dbl>,
#> #   previews <dbl>
```

We can confirm this by filtering for these theatre names.


```r
broadway %>%
  mutate(theatre = if_else(theatre == "Studio 54", "Studio 54 Theatre", theatre)) %>%
  filter(theatre %in% c("Studio 54", "Studio 54 Theatre"))
#> # A tibble: 787 × 8
#>    week_ending show    theatre weekly_gross avg_ticket_price
#>    <date>      <chr>   <chr>          <dbl>            <dbl>
#>  1 1998-02-15  Cabaret Studio…        48008             58.4
#>  2 1998-02-22  Cabaret Studio…       172373             51.5
#>  3 1998-03-01  Cabaret Studio…       174178             50.8
#>  4 1998-03-08  Cabaret Studio…       177623             49.3
#>  5 1998-03-15  Cabaret Studio…       147752             48.3
#>  6 1998-03-22  Cabaret Studio…       151753             49.1
#>  7 1998-03-29  Cabaret Studio…       183802             48.7
#>  8 1998-04-05  Cabaret Studio…       194515             50.8
#>  9 1998-04-12  Cabaret Studio…       219786             54.2
#> 10 1998-04-19  Cabaret Studio…       196320             48.1
#> # … with 777 more rows, and 3 more variables:
#> #   top_ticket_price <dbl>, performances <dbl>,
#> #   previews <dbl>
```

Notice that we did not save the initial modified data frame. We are also using a new
operator %in% which checks for the value Studio 54 in a vector of values including
Studio 54 and Studio 54 Theatre.

## Arguments

### `across()`

The `across()` function takes the following as arguments:

| Argument | Parameter | Details                                           |
| -------- | --------- | ------------------------------------------------- |
| .fns     |           | can pass a list of functions or a single function |
| .cols    | vector    | vector with column names to apply functions to    |

You can read more about the arguments in the `across()` function documentation
[here](https://dplyr.tidyverse.org/reference/across.html). Please note that the arguments 
for across() will also depend on your use case.

### `mutate_if()`

The `mutate_if()` function takes the following as arguments:

| Argument  | Details                                            |
| --------- | -------------------------------------------------- |
| selection | selection of variables by type, i.e., is.character |
| function  |  function to apply to the selection of variables   |

You can read more about the arguments in the `mutate_if()` function documentation
[here](https://dplyr.tidyverse.org/reference/mutate_all.html). 

### `na_if()`

The `na_if()` function takes the following as arguments:

| Argument  | Details                                            |
| --------- | -------------------------------------------------- |
| vector    | vector to look for values we want to change        |
| value     | value in the vector that we want to change to NA   |

You can read more about the arguments in the `na_if()` function documentation
[here](https://dplyr.tidyverse.org/reference/na_if.html).

You can read more about `if_else()` in the corresponding tutorial on conditional
statements.

## Exercises

### Exercise 1

Count the number of distinct shows and distinct theatres using summarise() and across().
As a tip, try to use the data type for shows and theatres columns.





### Exercise 2

Use the mutate_if() function to select all the variables of type double and convert them
to character.





### Exercise 3

There are some shows with a value of [title of show] under the show column. Use the
na_if() conditional statement within mutate() to convert this to NA.






## Next Steps

If you would like to learn more about the functions in this tutorial, you may find the
following resource helpful:

- [dplyr: Apply a function (or functions) across multiple
columns](https://dplyr.tidyverse.org/reference/across.html)
- [Mutate multiple columns](https://dplyr.tidyverse.org/reference/mutate_all.html)
- [Convert values to NA](https://dplyr.tidyverse.org/reference/na_if.html)










# Tidying up datasets

*Written by Mariam Walaa.*

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












# `pull()`, `pluck()`, and `unnest()`

*Written by Isaac Ehrlich.*

## Introduction

Indexing, manipulating, or handling data frames and tibbles can be messy and tricky, especially when these objects are organized in complex data structures. Tidyverse functions `pull()`, `pluck()`, and, `unnest()` can make dealing with these data structures easier and neater. 

In this lesson, you will learn how to:

- Use `pull()` to access a single column of a data frame
- Use `pluck()` for deep indexing and to access elements of data structures
- Use `unnest()` to flatten data frames


Prerequisite skills include:

- Knowledge of tibbles and other data structures
- Knowledge of indexing using special characters such as `[]` and `$`


## pull()
`pull()` is essentially the `$` indexing operator formatted as a function, allowing for neat indexing of data frames. As input, `pull()` takes the data frame, as well as `var`, which is information on the element you want to extract. `var` can either be the name of the column or an index. If the index is negative, `pull()` will count the indices from the right side (i.e. `var = 1` will pull the first column and `var = -1` will pull the last).

Let's take a look at some examples using a Caribou Location Tracking data set.

### Examples

```r
# Load csv file
locations <- read_csv("https://raw.githubusercontent.com/tacookson/data/master/caribou-location-tracking/locations.csv", n_max = 1000)

# Extract the 'event_id' column
event_id_col <- locations %>% pull(var = "event_id")

# We can do this with positive and negative indexing as well
# event_id is the first column out of 7
event_id_pos_idx <- locations %>% pull(var = 1)
event_id_neg_idx <- locations %>% pull(var = -7)

# Verify positive and negative indexing returned the same column using 'table()'
table(event_id_pos_idx == event_id_neg_idx)
#> 
#> TRUE 
#> 1000
```


## pluck()
`pluck()` is similar to `pull()`, but is more robust, and can handle complex data structures, such as lists of data frames. While `pull()` takes only one input to specify a column, `pluck()` can accept multiple, and therefore also allows for neat and flexible indexing of deep data structures. Similar to `pull()`, the output of `pluck` can also be achieved using traditional indexing, but `pluck()` is often simpler to use, and may make your code more readable.

The main arguments of `pluck()` are the data structure that contains the elements you want to access, and then the elements themselves. If the element does not exist, `pluck()` by default will return `NULL`, though this can be changed by adjusting the `.default` argument.

Let's take a look at some examples using multiple data sets on Broadway Weekly Grosses. 

### Examples

The simplest use of `pluck()` is in place of `pull()` - to extract a single column from a data frame object. Without using `pull()`, `[]`, or `$` to index, let's extract the `weekly_gross` column from the following file.

```r
# Load data
grosses <- read_csv("https://raw.githubusercontent.com/tacookson/data/master/broadway-grosses/grosses.csv", n_max = 1000)

# Use 'pluck()' to access a single column
weekly_gross_col <- grosses %>% pluck("weekly_gross")

# This can also be done using indices rather than column names
weekly_gross_idx <- grosses %>% pluck(6)

# Use 'table()' to verify the outputs are the same
table(weekly_gross_col == weekly_gross_idx)
#> 
#> TRUE 
#> 1000
```

`pluck()` can similarly use indices to grab elements of vectors and lists.

```r
# Create list and grab the fourth element
letters <- list("a", "b", "c", "d", "e")
element <- letters %>% pluck(4)
element
#> [1] "d"
```


However, because `pluck()` can take multiple arguments, it is also capable extracting columns from more complex data structures, such as a list of data frames. This is often referred to as "deep indexing" - indexing that requires multiple index calls, brackets, or elements. Let's download a few more data frames and see how this works.

```r
# Load data
grosses <- read_csv("https://raw.githubusercontent.com/tacookson/data/master/broadway-grosses/grosses.csv", n_max = 1000)
early_starts <- read_csv("https://raw.githubusercontent.com/tacookson/data/master/broadway-grosses/pre-1985-starts.csv", n_max = 1000)
synopses <- read_csv("https://raw.githubusercontent.com/tacookson/data/master/broadway-grosses/synopses.csv", n_max = 1000)

# Create list of data frames
broadway_data <- list(grosses, early_starts, synopses)

# Select `synopsis` column from `synopses` table
synopsis_col <- broadway_data %>% pluck(3, "synopsis")

# Use table() to verify the output is correct
table(synopsis_col == broadway_data[[3]][,2])
#> 
#> TRUE 
#>  835
```
Similarly, `pluck()` can be used for other data structures like lists of lists as well.

## `unnest()`
The main purpose of `unnest()` is to flatten existing data frames. Like `pluck()`, `unnest()` handles complex data structures, but these complex structures are now made up of lists (or other structures) contained within a single data frame (known as list-columns). In other words, if a column of a data frame contains other data structures, such as other tibbles, `unnest()` can flatten the data frame to remove these structures.

The arguments that `unnest()` takes are the data frame, as well as the columns to flatten, or unnest. For additional arguments, see documentation. 

Let's construct some toy data frames and take look at some examples.

### Examples
Even without nesting tibbles within tibbles, `unnest()` can be used in cases such as flattening long strings using `strsplit()` or other functions.

```r
# Create toy data
# Even though the 'color' and 'shades' column are of the same length, we can see that two entries in the 'shades' column contain elements separated by a comma
color_shades <- tibble(color = c("red", "orange", "yellow"), shades = c("red,cherry,scarlet", "orange,apricot", "yellow"))
head(color_shades)
#> # A tibble: 3 × 2
#>   color  shades            
#>   <chr>  <chr>             
#> 1 red    red,cherry,scarlet
#> 2 orange orange,apricot    
#> 3 yellow yellow


# We can use 'strsplit()' to unnest the elements in the shades column
color_shades <- color_shades %>% unnest(shades = strsplit(shades, ","))
head(color_shades)
#> # A tibble: 6 × 2
#>   color  shades 
#>   <chr>  <chr>  
#> 1 red    red    
#> 2 red    cherry 
#> 3 red    scarlet
#> 4 orange orange 
#> 5 orange apricot
#> 6 yellow yellow
```


However, `unnest()` is typically meant to be used with lists-columns held within data frames.

```r
# Create toy data
# 'rgb' column is a list of tibbles containing rgb values
color_rgb <- tibble(
  color = c("red", "orange", "yellow"),
  rgb = list(
    tibble(r = 255, g = 0, b = 0),
    tibble(r = 255, g = 70, b = 0),
    tibble(r = 255, g = 255, b = 0)
  )
)
head(color_rgb)
#> # A tibble: 3 × 2
#>   color  rgb             
#>   <chr>  <list>          
#> 1 red    <tibble [1 × 3]>
#> 2 orange <tibble [1 × 3]>
#> 3 yellow <tibble [1 × 3]>

# Flatten the 'rgb' column to create a column for each color component
color_rgb <- color_rgb %>% unnest(rgb)
head(color_rgb)
#> # A tibble: 3 × 4
#>   color      r     g     b
#>   <chr>  <dbl> <dbl> <dbl>
#> 1 red      255     0     0
#> 2 orange   255    70     0
#> 3 yellow   255   255     0
```
We can see that once the rgb column is unnested, it is easier to read and grab each component individually.

## Practice questions


<!-- ```{r pullq1, echo = FALSE} -->
<!-- question("Using a negative index in 'pull()' will", -->
<!-- answer("return an error"), -->
<!-- answer("create a new column"), -->
<!-- answer("return NULL"), -->
<!-- answer("index from the right side instead of the left", correct = TRUE), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

<!-- ```{r pullq2, echo = FALSE} -->
<!-- question("'pull()' and 'pluck()' perform functions no other operators in R are capable of", -->
<!-- answer("True", message = "Remember there are many ways to index!"), -->
<!-- answer("False", correct = TRUE, message = "Correct! Using 'pull()' and 'pluck()' is mostly a stylistic choice, but they are great for pipes and can definitely make your code neater!"), -->
<!-- allow_retry = TRUE) -->

<!-- ``` -->

<!-- ```{r pullq3, echo = FALSE} -->
<!-- question("Which of the following are true?", -->
<!-- answer("'pluck()' is a robust alternative to 'pull()' - it can handle complex data structures", correct = TRUE), -->
<!-- answer("'pull()' is a robust alternative to 'pluck()' - it can handle complex data structures"), -->
<!-- answer("'pull()' takes in one index argument ('var') as input", correct = TRUE), -->
<!-- answer("'pluck()' can take multiple index arguments as input", correct = TRUE), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

## Practice coding
It's your turn to try! In the code below, we've created a complex data structure, where `colors` is a list of the data frames `red`, `orange`, and `yellow`, where `yellow` also has nested data frames. See if you can complete the following questions!

```r
red <- tibble(shade = c("brick", "bright", "burgundy", "cardinal", "cherry"),
              r = c(170, 238, 128, 196, 210),
              g = c(74, 75, 0, 30, 4),
              b = c(68, 43, 32, 58, 45))
orange <- tibble(shade = c("papaya", "coral", "dark", "apricot", "topaz"),
              r = c(255, 255, 255, 251, 255),
              g = c(239, 127, 140, 206, 200),
              b = c(213, 80, 0, 177, 124))
yellow <- tibble(shade = c("amber", "brass", "bright", "canary", "cream"),
                 rgb = list(tibble(r = 255, g = 191, b = 0),
                            tibble(r = 225, g = 193, b = 110),
                            tibble(r = 255, g = 234, b = 0),
                            tibble(r = 255, g = 255, b = 143),
                            tibble(r = 255, g = 253, b = 208)))


colors <- list(red, orange, yellow)
```

**1. Use `pull()` to extract the `shade` column from the `red` data frame**

<!-- ```{r pull-coding1, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r pull-coding1-solution} -->
<!-- red %>% pull(shade) -->
<!-- # OR -->
<!-- red %>% pull(1) -->
<!-- # OR -->
<!-- red %>% pull(-4) -->
<!-- ``` -->

<!-- **2. Use `pluck()` to extract the `shade` column from the `red` data frame from within the `colors` list** -->
<!-- ```{r pull-coding2, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r pull-coding2-solution} -->
<!-- colors %>% pluck(1, "shade") -->
<!-- ``` -->

<!-- **3. Use `pluck()` to extract the yellow data frame, and then use `pull()` to grab just the `b` column. Remember that the `yellow` data frame has a nested tibble so you may have to use `unnest()`! -->
<!-- ```{r pull-coding3, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r pull-coding3-solution} -->
<!-- colors %>% pluck(3) %>% unnest(rgb) %>% pull(b) -->
<!-- ``` -->

## Overview and Next Steps
- `pull()` allows for a simple way to extract single columns from data frames
- `pluck()` performs similar functions as `pull()` but is also capable of handling complex data structures, such as lists of data frames (and lists of lists of data frames, and lists of lists of lists of data frames and...) 
- Although the use of `pull()` and `pluck()` is generally a stylistic choice, these functions let you avoid multiple special characters like `[[]]` and `$` and can make your code neater too!
- `unnest()` flattens data frames that contain other lists or data frames (known as list-columns)

In the next lesson, we will continue looking into different ways of storing and handling data in R - this time with factors!












# `forcats` and factors

*Written by Matthew Wankiewicz.*






## Introduction

In this lesson, you will learn about:

- Factors in R, how they work, what they do.
- The `forcats` package.

Highlights:

- Factors are a way of storing data in R. Instead of having many different combinations like a list of names or numbers, factors are usually created to represent a fixed number of values, such as levels (high, low, medium) or times (early, late, on-time). In other words, factors represent categorical data in R.
- `forcats` contains many functions that allow you to work with factors for plotting or further data analysis.


## The Content

Factors represent categorical variables in R. Factors are stored as integer levels in R, meaning that each level of a factor will be represented by an integer so R knows which one represents the maximum and minimum. Factors can be comprised of both integers and characters but the levels of these factors will be displayed as characters. The `factor` function can be used to create factors in R, it takes a vector of data and will turn it into a factor. This function can be used on columns in datasets to convert a column of data from numeric/character to a factor. 

`forcats` is a package that contains various functions to manipulate factors, it exists as its own package but is also included in the `tidyverse` package as well. The main goals of these functions are to help reorder and change factor levels, this is done by changing which levels appear at the front/back and also combining levels into other ones. 

A helpful cheatsheet for `forcats` can be found [here.](https://github.com/rstudio/cheatsheets/blob/master/factors.pdf)

## Factors

The `factor` function allows you to take a vector and turn it into a factor. The vector used can be made up of characters or integers. Its main argument is the vector that you want to turn into a factor. An example of this is shown below. 


```r
factor_vector <- c(1,2,3)
factor(x = factor_vector)
#> [1] 1 2 3
#> Levels: 1 2 3
```

In addition to the main argument, `factor` also has some optional arguments. These include `levels`, `labels` and `exclude`. `levels` tells R what the order of the levels are of your factor (which is highest/lowest), if you leave it empty it will make the levels in alphabetical order or increasing order for integers. `labels` will create labels for your factor and will set the order of your factor. `exclude` will take out a level that appears in your factor and replace those values with `<NA>`. 

We can change the levels of our `factor_vector` from earlier using the `levels` argument.

```r
factor_vector <- c(1,2,3)
factor(x = factor_vector, levels = c(2,1,3)) ## set levels to 2,1,3
#> [1] 1 2 3
#> Levels: 2 1 3
```


Using the `labels` argument, we can rename the levels of `factor_vector`. This will rename 1 to 'one', 2 to 'two' and 3 to 'three'.

```r
factor_vector <- c(1,2,3)
factor(x = factor_vector, labels = c('one', 'two', 'three')) ## set labels to 'one', 'two', 'three'
#> [1] one   two   three
#> Levels: one two three
```

Using `exclude` we can exclude the number two from our factor.

```r
factor_vector <- c(1,2,3)
factor(x = factor_vector, exclude = 2)
#> [1] 1    <NA> 3   
#> Levels: 1 3
```

If you want to test if a column or set of data is a factor, you can use `is.factor`.


```r
factor_vector <- c(1,2,3)
new_factor <- factor(x = factor_vector, exclude = 2)

is.factor(x = new_factor)
#> [1] TRUE
```

You can also check the levels of a factor using `levels`


```r
factor_vector <- c(1,2,3)
new_factor <- factor(x = factor_vector)

levels(x = new_factor)
#> [1] "1" "2" "3"
```


## Forcats

There are many useful functions in the `forcats` library but this lesson will mainly focus on `fct_relevel` and `fct_reorder` while also looking briefly at `fct_count`, `fct_c` and `fct_lump`.

### `fct_count`

This function can be used to count the number of values in each level of your factor. It takes one main argument, the factor you want to count. The other optional arguments (`sort`, `prop`) sort the most common levels to the top and can compute the proportion of the levels represented.


```r
random_factor <- factor(x = c(1,1,1,2,3,4,2,3,2,1,4,3,3,3,2,1))
fct_count(random_factor)
#> # A tibble: 4 × 2
#>   f         n
#>   <fct> <int>
#> 1 1         5
#> 2 2         4
#> 3 3         5
#> 4 4         2

fct_count(random_factor, sort = TRUE)
#> # A tibble: 4 × 2
#>   f         n
#>   <fct> <int>
#> 1 1         5
#> 2 3         5
#> 3 2         4
#> 4 4         2

fct_count(random_factor, sort = TRUE, prop = TRUE)
#> # A tibble: 4 × 3
#>   f         n     p
#>   <fct> <int> <dbl>
#> 1 1         5 0.312
#> 2 3         5 0.312
#> 3 2         4 0.25 
#> 4 4         2 0.125
```

### `fct_c` 

This function takes factors with different levels and can combine them into one factor with the levels from the other factors. The only argument it takes are the factors you want to combine. We see that when using it on factors with levels 'a' and 'b' it will combine them into one factor with levels 'a' and 'b'. 


```r
factor_a <- factor(x = "a")
factor_b <- factor(x = "b")

fct_c(factor_a, factor_b)
#> [1] a b
#> Levels: a b
```

### `fct_lump` functions

This group of functions takes levels and brings them together to form a level called "other". The functions include:

  - `fct_lump_min:` This function takes a factor and a number which tells R whether to include the level in other. An optional argument is called `other_level`, this will change the name of the "other" level.
  - `fct_lump_prop:` This function will lump levels that appear less than a certain proportion of times. For example, you can lump functions that make up less than 15% of your data. 
  - `fct_lump_n:` This function lumps all of the levels except the n most frequent ones.
  

```r
random_factor <- factor(x = c(1,1,1,2,3,4,2,3,2,1,4,3,3,3,2,1,1))

fct_lump_n(random_factor, n = 2) # keep the 2 most frequent levels
#>  [1] 1     1     1     Other 3     Other Other 3     Other
#> [10] 1     Other 3     3     3     Other 1     1    
#> Levels: 1 3 Other
fct_lump_prop(random_factor, prop = .25) # lump levels which appear less than 25 % of time
#>  [1] 1     1     1     Other 3     Other Other 3     Other
#> [10] 1     Other 3     3     3     Other 1     1    
#> Levels: 1 3 Other
fct_lump_min(random_factor, min = 3) # lump levels which appear less than 3 times
#>  [1] 1     1     1     2     3     Other 2     3     2    
#> [10] 1     Other 3     3     3     2     1     1    
#> Levels: 1 2 3 Other
```


### `fct_reorder` 
This function is useful when working with factors because it allows you to reorder a factor you are working with by another variable. For example, you can reorder a factor with levels of different sports by the average height for the sports listed. The first argument for this function is the factor/variable you plan to re-order and the second will be the variable you are sorting the factor by.

Using the `expeditions` data which looks at Himalayan expeditions, we can reorder the levels of the seasons by the average peak height for each season. As you can see, by adding the `mutate` line we can change the order of the levels depending on the mean height reached that season.

```r
data_ex <- expeditions %>% 
  group_by(season) %>% 
  summarise(mean_height = mean(highpoint_metres, na.rm = T))

data_ex %>% 
  ggplot(aes(x = season, y = mean_height)) +
  geom_col() +
  labs(title = "Plot without fct_reorder")
```

<img src="073-he_was_a_d8er_boi-names_rbind_cbind_files/figure-html/reorder-expedition-1.png" width="672" />

```r

data_ex %>% 
  mutate(season = fct_reorder(season, mean_height)) %>% 
  ggplot(aes(x = season, y = mean_height)) +
  geom_col() +
  labs(title = "Plot with fct_reorder")
```

<img src="073-he_was_a_d8er_boi-names_rbind_cbind_files/figure-html/reorder-expedition-2.png" width="672" />

```r

data_sorted <- data_ex %>% 
  mutate(season = fct_reorder(season, desc(mean_height)))

levels(as.factor(data_ex$season))
#> [1] "Autumn"  "Spring"  "Summer"  "Unknown" "Winter"
levels(data_sorted$season)
#> [1] "Spring"  "Autumn"  "Winter"  "Summer"  "Unknown"
```
We can see that the original order was alphabetical while the new sorted one is not.


`fct_reorder` can also be used to sort factors in descending order. We will use the same dataset, but this time we will order the levels of seasons decreasing by number of staff hired

```r
crew_group <-expeditions %>% 
  group_by(season) %>% 
  summarise(mean_staff = mean(hired_staff, na.rm = T))

crew_group %>% 
  ggplot(aes(x = season, y = mean_staff)) +
  geom_col() +
  labs(title = "Plot without fct_reorder")
```

<img src="073-he_was_a_d8er_boi-names_rbind_cbind_files/figure-html/fct-reorder-desc-1.png" width="672" />

```r

crew_group %>% 
  mutate(season = fct_reorder(season, desc(mean_staff))) %>% 
  ggplot(aes(x = season, y = mean_staff)) +
  geom_col() +
  labs(title = "Plot with fct_reorder")
```

<img src="073-he_was_a_d8er_boi-names_rbind_cbind_files/figure-html/fct-reorder-desc-2.png" width="672" />

```r

data_sorted <- crew_group %>% 
  mutate(season = fct_reorder(season, desc(mean_staff)))

levels(as.factor(crew_group$season))
#> [1] "Autumn"  "Spring"  "Summer"  "Unknown" "Winter"
levels(data_sorted$season)
#> [1] "Spring"  "Winter"  "Summer"  "Autumn"  "Unknown"
```
Once again we see that the order of levels has switched from alphabetical to a different order.



### `fct_relevel`

This function is used to change the levels of a factor. When R deals with levels in a factor, it sorts the levels of the factor in alphabetical order. This means that if your factor includes temperatures like "hot", "cold" and "medium", R will make the levels "cold", "hot", "medium". This can be tricky when classifying the factor because you may want it in increasing temperature or certain order. 

  - `fct_relevel` takes three arguments: the factor you want to relevel, the new order of the levels and `after` which tells R where you want the new order to occur (you can set `after=Inf` to bring your order to the end.)
  
If you have a factor with levels "hot", "cold" and "medium", R will sort the levels alphabetically, meaning the order will be "cold", "hot" and then "medium". `fct_relevel` is one way to put the levels in the correct order. There are many ways to change the order, you can either write the order yourself or just move hot to the end using `after = Inf`.


```r
temperatures <- factor(x = c("hot", "cold", "medium"))
levels(x = temperatures)
#> [1] "cold"   "hot"    "medium"

# use fct_relevel

fct_relevel(temperatures, "hot", after = Inf)
#> [1] hot    cold   medium
#> Levels: cold medium hot
```

Another example of using `fct_relevel` is with the expedition data. We can use it to change the levels of the `termination_reason` to place Successful expeditions at the top of the levels.

```r
termination_levels <- levels(as.factor(expeditions$termination_reason))
reordered_levels <- fct_relevel(termination_levels, "Success (claimed)", "Success (main peak)",
            "Success (subpeak)")

levels(x = reordered_levels)
#>  [1] "Success (claimed)"                                                           
#>  [2] "Success (main peak)"                                                         
#>  [3] "Success (subpeak)"                                                           
#>  [4] "Accident (death or serious injury)"                                          
#>  [5] "Attempt rumoured"                                                            
#>  [6] "Bad conditions (deep snow, avalanching, falling ice, or rock)"               
#>  [7] "Bad weather (storms, high winds)"                                            
#>  [8] "Did not attempt climb"                                                       
#>  [9] "Did not reach base camp"                                                     
#> [10] "Illness, AMS, exhaustion, or frostbite"                                      
#> [11] "Lack (or loss) of supplies or equipment"                                     
#> [12] "Lack of time"                                                                
#> [13] "Other"                                                                       
#> [14] "Route technically too difficult, lack of experience, strength, or motivation"
#> [15] "Unknown"
```
Now we have successes at the top.

You can also include a function in `fct_relevel` to change up the order of your levels. You can use functions like `sample`, `sort` or `rev` to change the order. 

```r
termination_levels <- levels(as.factor(expeditions$termination_reason))
# use sample to make the order of levels randomized

levels(fct_relevel(termination_levels, sample))
#>  [1] "Attempt rumoured"                                                            
#>  [2] "Unknown"                                                                     
#>  [3] "Did not reach base camp"                                                     
#>  [4] "Bad conditions (deep snow, avalanching, falling ice, or rock)"               
#>  [5] "Did not attempt climb"                                                       
#>  [6] "Success (subpeak)"                                                           
#>  [7] "Bad weather (storms, high winds)"                                            
#>  [8] "Success (claimed)"                                                           
#>  [9] "Other"                                                                       
#> [10] "Success (main peak)"                                                         
#> [11] "Illness, AMS, exhaustion, or frostbite"                                      
#> [12] "Accident (death or serious injury)"                                          
#> [13] "Route technically too difficult, lack of experience, strength, or motivation"
#> [14] "Lack (or loss) of supplies or equipment"                                     
#> [15] "Lack of time"
```


## Exercises

These next exercises will use a dataset which looks at the various countries who have given gifts to the United States, along with the monetary value of these gifts. While the original dataset has almost every country in the world, we will focus on a smaller portion of the countries. 


```
#> Rows: 747
#> Columns: 10
#> $ id               <dbl> 3, 5, 6, 7, 13, 29, 51, 52, 57, 6…
#> $ recipient        <chr> "President", "President", "Presid…
#> $ agency_name      <chr> NA, NA, NA, NA, NA, NA, NA, NA, N…
#> $ year_received    <dbl> 1999, 1999, 1999, 1999, 1999, 199…
#> $ date_received    <date> NA, NA, NA, NA, NA, NA, NA, NA, …
#> $ donor            <chr> "Sr. Victor Cervera Pacheco, Gove…
#> $ donor_country    <chr> "Mexico", "Spain", "France", "Ita…
#> $ gift_description <chr> "49\" tall wood chair with a blac…
#> $ value_usd        <dbl> 1000, 660, 1200, 1400, 250, 800, …
#> $ justification    <chr> "Non-acceptance would cause embar…
```


Using `fct_reorder` change the order of the `donor_country` levels to be in order of `mean_value`.


```r
gifts_grouped <- gifts %>% 
  group_by(donor_country) %>% 
  summarise(mean_value = mean(value_usd, na.rm = T))
## Enter solution below
```


```r
gifts_grouped <- gifts %>% 
  group_by(donor_country) %>% 
  summarise(mean_value = mean(value_usd, na.rm = T))
## Enter solution below
fct_reorder(gifts_grouped$donor_country, gifts_grouped$mean_value)
#> [1] Australia Brazil    Canada    France    Germany  
#> [6] Italy     Mexico    Spain    
#> 8 Levels: Spain Canada Mexico Australia Germany ... Italy
```

Now, using `fct_reorder` change the order of the `donor_country` levels to be decreasing by `mean_value`. (Bonus: use the new order to make a plot, steps are very similar to the earlier examples) 


```r
gifts_grouped <- gifts %>% 
  group_by(donor_country) %>% 
  summarise(mean_value = mean(value_usd, na.rm = T))
## Enter solution below
```


```r
gifts_grouped <- gifts %>% 
  group_by(donor_country) %>% 
  summarise(mean_value = mean(value_usd, na.rm = T))
## Enter solution below
fct_reorder(gifts_grouped$donor_country, desc(gifts_grouped$mean_value))
#> [1] Australia Brazil    Canada    France    Germany  
#> [6] Italy     Mexico    Spain    
#> 8 Levels: Italy Brazil France Germany Australia ... Spain

## BONUS
gifts_grouped %>% 
  mutate(donor_country = fct_reorder(donor_country, desc(mean_value))) %>% 
  ggplot(aes(donor_country, mean_value)) +
  geom_col()
```

<img src="073-he_was_a_d8er_boi-names_rbind_cbind_files/figure-html/forcats-test-2-solution-1.png" width="672" />


Using `fct_relevel`, change the order of the levels for `gifts$donor_country` to be randomly sampled.




```r
fct_relevel(gifts$donor_country, sample)
#>   [1] Mexico    Spain     France    Italy     France   
#>   [6] Canada    Mexico    Mexico    Canada    France   
#>  [11] France    Germany   France    France    Italy    
#>  [16] Canada    Italy     Canada    Australia Australia
#>  [21] Mexico    Germany   Italy     Australia Australia
#>  [26] Spain     Italy     Italy     Italy     France   
#>  [31] Mexico    Mexico    Germany   Mexico    Italy    
#>  [36] France    Spain     Italy     Spain     Spain    
#>  [41] France    Mexico    Mexico    Australia Mexico   
#>  [46] Canada    Mexico    Mexico    Germany   Canada   
#>  [51] Canada    Mexico    Italy     Italy     Italy    
#>  [56] Italy     Italy     Italy     Italy     Italy    
#>  [61] Italy     Italy     Canada    Australia France   
#>  [66] Italy     France    Spain     Mexico    Canada   
#>  [71] Canada    Mexico    Canada    Spain     Spain    
#>  [76] Italy     Australia Australia Spain     Spain    
#>  [81] Italy     Italy     Italy     Italy     Mexico   
#>  [86] Italy     Mexico    Mexico    France    Italy    
#>  [91] Italy     Italy     Italy     France    Mexico   
#>  [96] Spain     Germany   Germany   France    Italy    
#> [101] Italy     Canada    Italy     Italy     Mexico   
#> [106] Germany   Italy     Mexico    Italy     Italy    
#> [111] Germany   Italy     France    Mexico    Italy    
#> [116] Australia Italy     Australia France    Italy    
#> [121] Spain     France    Brazil    Italy     Australia
#> [126] Italy     Italy     France    Australia Italy    
#> [131] Italy     Italy     Spain     Australia Australia
#> [136] Italy     France    Italy     Italy     Italy    
#> [141] Italy     Canada    Canada    Canada    Canada   
#> [146] Italy     Canada    Italy     Italy     France   
#> [151] France    Spain     Canada    Italy     Spain    
#> [156] Italy     France    Mexico    Canada    Spain    
#> [161] Mexico    Canada    Italy     Italy     Italy    
#> [166] Italy     Italy     Italy     Italy     France   
#> [171] Italy     Italy     Italy     Italy     Italy    
#> [176] Italy     Italy     France    Mexico    Mexico   
#> [181] Brazil    Canada    France    Italy     Italy    
#> [186] France    Italy     France    Germany   France   
#> [191] Canada    France    France    Canada    Mexico   
#> [196] Germany   Italy     France    Italy     Brazil   
#> [201] Brazil    Italy     Italy     Italy     Italy    
#> [206] Italy     Italy     France    Canada    Italy    
#> [211] Spain     Mexico    Mexico    Italy     Mexico   
#> [216] Italy     Germany   France    Italy     Canada   
#> [221] Germany   Italy     Italy     Australia Italy    
#> [226] Canada    Italy     Germany   Italy     Canada   
#> [231] Mexico    Germany   Australia Australia Canada   
#> [236] Germany   France    Germany   France    Mexico   
#> [241] Italy     Italy     Italy     Mexico    Germany  
#> [246] Germany   Germany   Germany   Italy     Germany  
#> [251] Italy     Australia Germany   Mexico    Mexico   
#> [256] Italy     Italy     France    France    France   
#> [261] Brazil    Australia France    France    France   
#> [266] Italy     Italy     Australia Australia Australia
#> [271] Australia Australia Australia Australia Australia
#> [276] Australia Australia Australia Australia Australia
#> [281] Australia Australia Australia Australia Australia
#> [286] Australia Australia Australia Australia Australia
#> [291] Australia Canada    Italy     Italy     Italy    
#> [296] Mexico    Mexico    Brazil    France    Mexico   
#> [301] Mexico    Mexico    Mexico    Mexico    Mexico   
#> [306] Italy     Italy     Italy     Australia Italy    
#> [311] France    Brazil    Italy     Italy     Italy    
#> [316] Italy     France    France    Australia Australia
#> [321] Australia France    France    France    France   
#> [326] France    Italy     Germany   Mexico    Mexico   
#> [331] France    France    France    France    Italy    
#> [336] Italy     Italy     Australia Germany   Mexico   
#> [341] France    Italy     Italy     France    Canada   
#> [346] Italy     Italy     Italy     Italy     Italy    
#> [351] Italy     Italy     Italy     France    Brazil   
#> [356] Brazil    Brazil    Brazil    Spain     Mexico   
#> [361] Mexico    Mexico    Brazil    Mexico    Mexico   
#> [366] Germany   France    France    Mexico    Italy    
#> [371] Spain     Italy     Mexico    Germany   Brazil   
#> [376] Germany   Germany   Italy     Italy     Mexico   
#> [381] Italy     Italy     France    Spain     France   
#> [386] Germany   Italy     Germany   France    France   
#> [391] Italy     France    Italy     Italy     Australia
#> [396] Italy     Italy     Italy     Italy     Italy    
#> [401] Italy     Italy     Italy     Brazil    Brazil   
#> [406] Germany   Spain     Germany   France    France   
#> [411] Germany   Spain     France    Canada    Canada   
#> [416] Canada    Canada    Germany   Germany   Germany  
#> [421] Australia Brazil    Germany   Canada    Brazil   
#> [426] Brazil    Germany   Brazil    France    France   
#> [431] Germany   Australia Mexico    France    France   
#> [436] France    Mexico    Brazil    France    Spain    
#> [441] France    Germany   France    Italy     Italy    
#> [446] Canada    Canada    Australia Canada    Australia
#> [451] Germany   France    Canada    Mexico    Australia
#> [456] Brazil    Brazil    Brazil    France    Germany  
#> [461] Italy     France    Australia Mexico    France   
#> [466] France    France    France    Mexico    France   
#> [471] Mexico    Brazil    France    Germany   France   
#> [476] Australia France    Brazil    Brazil    Brazil   
#> [481] Germany   Italy     Italy     Italy     Italy    
#> [486] Australia Brazil    Mexico    Mexico    Mexico   
#> [491] Mexico    Italy     Mexico    Mexico    Mexico   
#> [496] Spain     Spain     Italy     Italy     Italy    
#> [501] Mexico    Spain     Italy     Italy     France   
#> [506] Brazil    Canada    Germany   Italy     Canada   
#> [511] Italy     Italy     Italy     Italy     Italy    
#> [516] Canada    Canada    Mexico    Canada    Canada   
#> [521] Spain     Italy     Mexico    Spain     France   
#> [526] Canada    France    Mexico    Spain     Spain    
#> [531] France    Canada    Spain     Italy     Italy    
#> [536] Canada    Canada    Mexico    France    Germany  
#> [541] France    Brazil    Italy     France    Italy    
#> [546] Italy     Italy     Mexico    Mexico    Italy    
#> [551] Canada    Brazil    France    Australia Mexico   
#> [556] Mexico    Germany   Italy     Canada    Mexico   
#> [561] Australia Brazil    Mexico    Canada    Mexico   
#> [566] Mexico    Germany   Mexico    Italy     Spain    
#> [571] Australia Australia Italy     Germany   Germany  
#> [576] Italy     France    Italy     France    France   
#> [581] France    Canada    Italy     Italy     Germany  
#> [586] France    Mexico    Brazil    Mexico    Germany  
#> [591] Germany   Germany   Germany   Germany   Germany  
#> [596] Germany   Germany   Germany   Brazil    Brazil   
#> [601] France    Mexico    France    Mexico    Mexico   
#> [606] Italy     Australia Spain     France    Germany  
#> [611] France    Germany   Mexico    France    Italy    
#> [616] Australia France    Mexico    Italy     France   
#> [621] Australia France    Australia Italy     France   
#> [626] Mexico    Brazil    Spain     Mexico    France   
#> [631] France    Italy     Brazil    Canada    Australia
#> [636] Italy     Canada    France    Australia Canada   
#> [641] Canada    Spain     Germany   Italy     Italy    
#> [646] Mexico    Italy     Germany   Italy     Brazil   
#> [651] Germany   Mexico    Spain     Italy     Germany  
#> [656] Italy     France    Australia Canada    Canada   
#> [661] Italy     France    Spain     Italy     Canada   
#> [666] Italy     Mexico    Mexico    Australia France   
#> [671] Canada    Canada    Canada    France    Mexico   
#> [676] France    Brazil    France    Italy     Brazil   
#> [681] Mexico    Australia Australia Italy     Canada   
#> [686] Germany   Canada    Spain     Spain     Mexico   
#> [691] Italy     Germany   Canada    Canada    Italy    
#> [696] Spain     Brazil    Canada    Mexico    France   
#> [701] Mexico    Germany   Canada    Canada    Canada   
#> [706] Italy     Germany   Germany   France    Australia
#> [711] Italy     Germany   Germany   Canada    Germany  
#> [716] Germany   Germany   Germany   Germany   Germany  
#> [721] Germany   Germany   Germany   France    France   
#> [726] Germany   Mexico    Mexico    Mexico    Mexico   
#> [731] Mexico    France    Spain     Australia France   
#> [736] Canada    Italy     France    Australia France   
#> [741] Germany   Germany   Germany   Germany   Germany  
#> [746] Germany   Spain    
#> 8 Levels: Canada Spain Italy Mexico Brazil ... Germany
```

This final exercise will combine the uses of different `forcats` functions and will still use the `gifts` data. 
Using one of the `fct_lump_` functions, lump all but 5 of the `donor_country` levels into other (save it under `gifts_lumped`). Next, using `fct_relevel` change the order to be in a random order (save under `gifts_lumped` again). Finally, using a `forcats` function count how many entries are in each level.




```r
gifts_lumped <- fct_lump_n(gifts$donor_country, 5)
gifts_lumped <- fct_relevel(gifts_lumped, rev)
fct_count(gifts_lumped)
#> # A tibble: 6 × 2
#>   f             n
#>   <fct>     <int>
#> 1 Other       156
#> 2 Mexico      104
#> 3 Italy       199
#> 4 Germany      89
#> 5 France      125
#> 6 Australia    74
```




```r
factor_example <- factor(c(rep("dog", 20), rep("cat", 19), 
                    rep("fish", 12), rep("cow", 9),
                    rep("bird", 24)))

fct_relevel(factor_example, "fish", "dog") 

fct_lump_n(factor_example, 2)
```


<!-- ```{r forcats-mult-choice-1, echo=F} -->
<!-- question("What is the order of the levels before we run `fct_relevel`?", -->
<!--          answer("dog, cat, fish, cow, bird"), -->
<!--          answer("bird, cat, cow, dog, fish", correct = TRUE), -->
<!--          answer("bird, dog, cat, fish, cow"), -->
<!--          answer("The order is random"), -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r forcats-mult-choice-2, echo=F} -->
<!-- question("After running `fct_relevel` what is the new order of the levels?", -->
<!--          answer("fish, dog, bird, cat, cow", correct = TRUE), -->
<!--          answer("bird, cat, cow, dog, fish"), -->
<!--          answer("fish, dog, other"), -->
<!--          answer("The order is still random"), -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r forcats-mult-choice-3, echo=F} -->
<!-- question("After running `fct_lump_n`, which 2 levels are kept out of other?", -->
<!--          answer("bird", correct = TRUE), -->
<!--          answer("cat"), -->
<!--          answer("cow"), -->
<!--          answer("dog", correct = TRUE), -->
<!--          answer("fish"), -->
<!--          allow_retry = T) -->
<!-- ``` -->


## Common Mistakes & Errors

- `Error: "f" must be a factor (or character vector).`
  - This error will occur if you try to call `forcats` functions on non-factors. To fix this, ensure you are using a factor. 
  
- `argument ".x" is missing, with no default`
  - This error will occur if you are missing an argument in your function call. Double check that you have filled out all arguments.

## Next Steps

Now that you're familiar with the `forcats` package, here are some additional resources to help continue your learning:

- The `forcats` website which includes more examples and information about the most important functions: https://forcats.tidyverse.org/

- R for Data Science's chapter about factors. This chapter gives another lesson on factors and also uses the `forcats` package to work with factors: https://r4ds.had.co.nz/factors.html

- The factors chapter from Jenny Bryan's STAT 545 book: https://stat545.com/factors-boss.html












# More on strings

*Written by Annie Collins.*

## More on strings

*Written by Annie Collins.*

### Introduction

In this lesson, we will be covering some additional functions that will help us work with text data. If you have not already done so, please feel free to look through the previous lesson "Strings with paste and glue and stringr" for more functions and examples of working with strings that might help your understanding of this lesson's content.

In this lesson, you will learn how to:

- Expand deliminated text data in a data frame using `separate()` and`separate_rows()`; and,
- Extract and manipulate text data in character vectors using `str_match()`, and `str_remove()`

Prerequisite skills include:

- Some knowledge from the previous strings lesson in this module, as well as the `stringr` and `tidyr` packages.

### Separate text-based data frames using separate() and separate_rows()

`separate()` and `separate_rows()` allow you to split up a single column of text data in different ways.

`separate()` divides a single column of text data into multiple columns. There are several arguments that allow you to specify how this is done. We will focus on a the most significant ones to start:

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

Right now the guests' orders are listed together in the column called `food`, but the data might be easier to read if each person's order for each course was in its own column. Run the code below to see how this can be accomplished.


```
#>     guest             soup   salad main course
#> 1   Annie butternut squash  ceasar     lasagna
#> 2  Mariam  italian wedding  garden     chicken
#> 3 Haoluan  italian wedding  ceasar     lasagna
#> 4 Shirley  italian wedding  ceasar     lasagna
#> 5   Rohan butternut squash  garden     chicken
#> 6     Sam butternut squash  garden     lasagna
```

Using `separate()`, we now can see each course as its own column and all the commas have been removed. Note that it's important to specify `sep = ","` in this case, since the default option would separate by spaces as well and split soup orders into separate columns which is not what we intended.

We can split up the information contained in the `food` column in a different way using `separate_rows()`. As the name might suggest, this function will split each string into distinct rows instead of columns. The syntax and arguments are similar to `separate()`:

| Argument | Parameter | Details
| -------- | --------- | ----------------------------------------- |
| data     | data frame | A data frame |
| ... | string | The name(s) of the column(s) containing the data to be separated. Multiple columns can be inputted if their lengths are compatible (i.e. the same number of new rows will be created once they are separated). Otherwise, an error will be raised. |
| sep | number OR string | Character between values to be separated. Defaults to any non-alpha-numeric characters. |

Notice that we don't need to worry about the name or number of new columns since none will be created. Once the data in the indicated column(s) has separated into additional rows, the data from accompanying columns will be duplicated to fill in the new row's remaining cells.

Run the code below and observe the difference between `separate()` and `separate_rows()`.


```
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

### Trouble Shooting separate()

Sometimes it is hard to know exactly how many columns your data will create when using `separate()`, which can lead to errors or unintended results when specifying the `into` argument. The function comes with a few *additional* arguments to help you control what happens in these scenarios. Note that this applies only when `sep` is a string, since if `sep` is numeric the column in question is always separated into two columns at the indicated location.

| Argument | Parameter | Details
| -------- | --------- | ----------------------------------------- |
| extra | string | Used to control what happens if there are extra columns created once all the names from `sep` are used. There are two options (not including the default, "warn"): **"drop"**, which will exclude any additional columns created, or **"merge"**, which will split the text at most `length(into)` times (so the last column indicated by `into` will contain unseparated data). |
| fill | string | Used to control what happens if there are not enough columns created to match the names indicated in `into`. There are two options (not including the default, "warn"): **"right"**, which fills the data frame with missing values on the right, and **"left"**, which fills the data frame with missing values on the left of the actual data. |

Run and edit the code below and observe the difference between the scenarios.

<!-- ```{r separate-exercise-3, exercise=TRUE} -->
<!-- letters <- data.frame(x = c("a.b", "a.b.c", "a.b.c.d")) -->
<!-- letters -->

<!-- # Too many columns created - try "drop" and "merge" in place of "warn" -->
<!-- separate(letters, x, c("A", "B"), extra = "warn") -->

<!-- # Not enough columns created - try "left" and "right" in place of "warn" -->
<!-- separate(letters, x, c("A", "B", "C", "D"), fill = "warn") -->

<!-- ``` -->


### Working with text data using str_match() and str_remove()

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

We now have a vector containing only the postal codes of interest, and we could manipulate it further to remove the NA's if desired. Now suppose we actually wanted to remove these postal codes from the original data. This is where we could use `str_remove()`.


```r
str_remove(postal_codes, "M5S[1-9][A-Z][1-9]")
#>  [1] ""       ""       "M4W3X2" "M5T3T3" "M4V9F6" "M4V6V9"
#>  [7] "M4V5K4" "M5T8U1" "M4V1V6" "M5R6X1" "M4Y7R8" ""      
#> [13] "M4Y7N6" "M4W2S9" ""       "M4V8K3" "M4V8K1" "M5T3B9"
#> [19] ""       ""       "M4V5S4" "M5T1V4" ""       "M4V9U6"
#> [25] "M5R8B8" "M4Y2K9" "M5R7T9" "M4W8M8" "M4Y8T7" "M5T7D1"
```

We now have a vector with blank strings instead of postal codes that begin with "M5S".

It is important to note that `str_match()` and `str_detect()` only operate on the first instance of the indicated pattern within each element of a string (this isn't so obvious in our postal code example since each string is rather simple and short). Both `str_match()` and `str_remove()` have accompanying functions `str_match_all()` and `str_remove_all()` which apply their functionality to *every* instance of the inputted pattern within the inputted character vector. Run the code below on a simpler vector to examine the difference.

<!-- ```{r all-exercise-, exercise = TRUE} -->
<!-- # Match -->
<!-- rhyme <- c("she", "sells", "sea", "shells") -->

<!-- str_match(rhyme, "s") -->

<!-- str_match_all(rhyme, "s") -->
<!-- ``` -->
<!-- ```{r all-exercise-2, exercise = TRUE} -->
<!-- # Remove -->
<!-- rhyme <- c("she", "sells", "sea", "shells") -->

<!-- str_remove(rhyme, "s") -->

<!-- str_remove_all(rhyme, "s") -->
<!-- ``` -->

### Questions

These questions will refer to the following data set called `groceries`.


```
#>                                   food
#> 1 bananas,apples,rice,pasta,tofu,pizza
#>                  drinks
#> 1 tea,coffee,juice,wine
```

<!-- ```{r separate-q-1, echo=FALSE} -->
<!-- question("How many rows will the output of \"separate_rows(groceries, drinks)\" have?", -->
<!--          answer("4", correct=TRUE), -->
<!--          answer("5"), -->
<!--          answer("6"), -->
<!--          answer("Error")) -->
<!-- ``` -->
<!-- ```{r separate-q-2, echo=FALSE} -->
<!-- question("How many rows will the output of \"separate_rows(groceries, food, drinks)\" have?", -->
<!--          answer("4"), -->
<!--          answer("5"), -->
<!--          answer("6"), -->
<!--          answer("Error", correct = TRUE), -->
<!--          correct = "Correct! Given the default \"sep\" value, \"drinks\" would separate into four new rows while \"food\" would separate into six, causing an error to be raised") -->
<!-- ``` -->
<!-- ```{r separate-q-3, echo=FALSE} -->
<!-- question("Suppose I execute \"separate(groceries, drinks, into=c(\"A\", \"B\", \"C\", \"D\", \"E\"), fill=\"left\")\". What will the second column of the outputted data frame contain?", -->
<!--          answer("bananas,apples,rice,pasta,tofu,pizza"), -->
<!--          answer("tea"), -->
<!--          answer("NA", correct = TRUE), -->
<!--          answer("Error") -->
<!--          ) -->
<!-- ``` -->
<!-- ```{r separate-q-4, echo=FALSE} -->
<!-- question("Suppose I execute \"separate(groceries, drinks, into=c(\"A\", \"B\", \"C\"), extra=\"merge\")\". What will the final column of the outputted data frame contain?", -->
<!--          answer("juice"), -->
<!--          answer("wine"), -->
<!--          answer("juice,wine", correct = TRUE), -->
<!--          answer("Error") -->
<!--          ) -->
<!-- ``` -->

### Exercises

#### Exercise 1

Replicate the following data set, beginning with `groceries` as above.

```
#> # A tibble: 6 × 5
#>   food    `1`   `2`    `3`   `4`  
#>   <chr>   <chr> <chr>  <chr> <chr>
#> 1 bananas tea   coffee juice wine 
#> 2 apples  tea   coffee juice wine 
#> 3 rice    tea   coffee juice wine 
#> 4 pasta   tea   coffee juice wine 
#> 5 tofu    tea   coffee juice wine 
#> 6 pizza   tea   coffee juice wine
```

<!-- ```{r separate-exercise-1, exercise=TRUE} -->

<!-- ``` -->
<!-- ```{r separate-exercise-1-solution} -->
<!-- groceries %>% separate(drinks, into=c("1", "2", "3", "4")) %>% separate_rows(food) -->
<!-- # Can switch order of the functions for the same result -->
<!-- ``` -->

#### Exercise 3

Using the `postal_codes` data from previous examples, remove every number from the data.

<!-- ```{r remove-exercise-1, exercise=TRUE} -->

<!-- ``` -->
<!-- ```{r remove-exercise-1-solution} -->
<!-- postal_codes %>% str_remove_all("[1-9]") -->
<!-- ``` -->


#### Exercise 2

Using the `postal_codes` data from previous examples, create a vector that contains only the last three characters of all postal codes beginning with "M5S".

<!-- ```{r remove-exercise-2, exercise=TRUE} -->

<!-- ``` -->
<!-- ```{r remove-exercise-2-solution} -->
<!-- postal_codes %>% str_match("M5S[1-9][A-Z][1-9]") %>% str_remove("M5S") -->
<!-- ``` -->

### Next Steps

Now that you are familiar with some functions that work with strings, you are well set up to explore other features that `stringr` has to offer. A good place to start is the `stringr` [cheatsheet](https://github.com/rstudio/cheatsheets/blob/master/strings.pdf) which outlines a myriad of tools for working with strings and text-based data in R.

















# Regular expressions

*Written by Shirley Deng.*

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











# Working with dates

*Written by Mariam Walaa.*

## Introduction

In this lesson, you will learn how to:

- Work with dates using the `lubridate` library

Prerequisite skills include:

- Installing and loading packages
- Using `mutate()` and `summarise()`

Highlights:

- Loading the `lubridate` library separately from `tidyverse`
- Using the `today()` and `now()` functions
- Learning how to extract information from a date-time column


## Overview

Let's start by loading the `tidyverse`.


```r
library(tidyverse)
```

Notice that `lubridate` is not listed as one of the libraries loaded into your R session
when you load `tidyverse` (which you can view in your output on your own RStudio), and
this is because it is not part of the core `tidyverse` so it will need to be loaded
separately.


```r
library(lubridate)
#> 
#> Attaching package: 'lubridate'
#> The following objects are masked from 'package:base':
#> 
#>     date, intersect, setdiff, union
```

Two of the functions the `lubridate` library will give us is `today()` and `now()`, which
we can immediately start to use, without data or parameters.


```r
today()
#> [1] "2021-09-06"
```


```r
now()
#> [1] "2021-09-06 11:26:15 EDT"
```

You may want to use these functions today() and now() for various reasons, such as 
including the date and time in a file name. You can do that as follows.


```r
paste0(today(), "_datafile.csv")
#> [1] "2021-09-06_datafile.csv"
```

### Example

We will look at Caribou data from Alex Cooksons dataset repository for this tutorial.




```r
glimpse(caribou)
#> Rows: 249,450
#> Columns: 7
#> $ event_id   <dbl> 2259197332, 2259197333, 2259197334, 225…
#> $ animal_id  <chr> "GR_C01", "GR_C01", "GR_C01", "GR_C01",…
#> $ study_site <chr> "Graham", "Graham", "Graham", "Graham",…
#> $ season     <chr> "Winter", "Winter", "Winter", "Winter",…
#> $ timestamp  <dttm> 2001-02-21 05:00:00, 2001-02-21 09:00:…
#> $ longitude  <dbl> -122.5200, -122.5224, -122.5232, -122.5…
#> $ latitude   <dbl> 56.23950, 56.23985, 56.24000, 56.23187,…
```

We can see that the timestamp column has an associated data type 'dttm.' This stands for
datetime. Given that this is already the correct data type, we can extract a lot of
information from it using `lubridate` functions.


```r
# extracting year
caribou %>% mutate(year = year(timestamp))
#> # A tibble: 249,450 × 8
#>      event_id animal_id study_site season timestamp          
#>         <dbl> <chr>     <chr>      <chr>  <dttm>             
#>  1 2259197332 GR_C01    Graham     Winter 2001-02-21 05:00:00
#>  2 2259197333 GR_C01    Graham     Winter 2001-02-21 09:00:00
#>  3 2259197334 GR_C01    Graham     Winter 2001-02-21 13:00:00
#>  4 2259197335 GR_C01    Graham     Winter 2001-02-21 17:01:00
#>  5 2259197336 GR_C01    Graham     Winter 2001-02-21 21:00:00
#>  6 2259197337 GR_C01    Graham     Winter 2001-02-22 01:00:00
#>  7 2259197338 GR_C01    Graham     Winter 2001-02-22 05:00:00
#>  8 2259197339 GR_C01    Graham     Winter 2001-02-22 09:00:00
#>  9 2259197340 GR_C01    Graham     Winter 2001-02-22 13:00:00
#> 10 2259197341 GR_C01    Graham     Winter 2001-02-22 17:00:00
#> # … with 249,440 more rows, and 3 more variables:
#> #   longitude <dbl>, latitude <dbl>, year <dbl>

# extracting week day
caribou %>% mutate(week_day = wday(timestamp))
#> # A tibble: 249,450 × 8
#>      event_id animal_id study_site season timestamp          
#>         <dbl> <chr>     <chr>      <chr>  <dttm>             
#>  1 2259197332 GR_C01    Graham     Winter 2001-02-21 05:00:00
#>  2 2259197333 GR_C01    Graham     Winter 2001-02-21 09:00:00
#>  3 2259197334 GR_C01    Graham     Winter 2001-02-21 13:00:00
#>  4 2259197335 GR_C01    Graham     Winter 2001-02-21 17:01:00
#>  5 2259197336 GR_C01    Graham     Winter 2001-02-21 21:00:00
#>  6 2259197337 GR_C01    Graham     Winter 2001-02-22 01:00:00
#>  7 2259197338 GR_C01    Graham     Winter 2001-02-22 05:00:00
#>  8 2259197339 GR_C01    Graham     Winter 2001-02-22 09:00:00
#>  9 2259197340 GR_C01    Graham     Winter 2001-02-22 13:00:00
#> 10 2259197341 GR_C01    Graham     Winter 2001-02-22 17:00:00
#> # … with 249,440 more rows, and 3 more variables:
#> #   longitude <dbl>, latitude <dbl>, week_day <dbl>

# extracting whether it's a leap year!
caribou %>% mutate(leap_year = leap_year(timestamp))
#> # A tibble: 249,450 × 8
#>      event_id animal_id study_site season timestamp          
#>         <dbl> <chr>     <chr>      <chr>  <dttm>             
#>  1 2259197332 GR_C01    Graham     Winter 2001-02-21 05:00:00
#>  2 2259197333 GR_C01    Graham     Winter 2001-02-21 09:00:00
#>  3 2259197334 GR_C01    Graham     Winter 2001-02-21 13:00:00
#>  4 2259197335 GR_C01    Graham     Winter 2001-02-21 17:01:00
#>  5 2259197336 GR_C01    Graham     Winter 2001-02-21 21:00:00
#>  6 2259197337 GR_C01    Graham     Winter 2001-02-22 01:00:00
#>  7 2259197338 GR_C01    Graham     Winter 2001-02-22 05:00:00
#>  8 2259197339 GR_C01    Graham     Winter 2001-02-22 09:00:00
#>  9 2259197340 GR_C01    Graham     Winter 2001-02-22 13:00:00
#> 10 2259197341 GR_C01    Graham     Winter 2001-02-22 17:00:00
#> # … with 249,440 more rows, and 3 more variables:
#> #   longitude <dbl>, latitude <dbl>, leap_year <lgl>
```

You can see there are many additional variables we can extract with the `lubridate` 
package. You can check out the [lubridate
cheatsheet](https://raw.githubusercontent.com/rstudio/cheatsheets/master/lubridate.pdf) to
learn more.

## Exercises

### Exercise 1

Extract month, day, and year into separate columns at the same time using mutate.






### Exercise 2

Find the earliest and latest dates in the timestamp column.






**Hint**: Remember the summary functions you learned in `summarize()` tutorial!

## Common Mistakes & Errors

- You might try to apply `lubridate` functions on to a column that looks like a timestamp
column, but it may still not be of the appropriate data type, which is either 'dt', 'tm',
or 'dttm'. Be sure to convert to the proper data type first!

## Next Steps

If you would like to learn more about handling dates and times in R, as well as the
`lubridate` package, please read the following:

- [R For Data Science:  16 Dates and times](https://r4ds.had.co.nz/dates-and-times.html)
- [Lubridate Package Documentation](https://lubridate.tidyverse.org/)













# `janitor` package

*Written by Mariam Walaa.*

## Introduction

In this lesson, you will learn how to:

- Tidy up variable names that are in your dataset
- Deal with duplicate or partially duplicate data

Prerequisite skills include:

- Installing and loading packages
- Understanding duplicate data
- Working with column names, such as `names()` and `rename()`

Highlights:

- You can make column names cleaner using janitors clean_names() function
- You can handle duplicate or partially duplicate data using janitors get_dupes() function

## Overview

> "The [janitor](https://garthtarr.github.io/meatR/janitor.html) package is a R package
that has simple functions for examining and cleaning dirty data. The main janitor
functions: perfectly format data frame column names; isolate partially-duplicate records;
and provide quick tabulations (i.e., frequency tables and crosstabs)."

As the description says, the `janitor` package will help you with cleaning your data. 
It is not part of the `tidyverse` so you will have to install it and then load it 
separately as follows.


```r
library(janitor)
#> 
#> Attaching package: 'janitor'
#> The following objects are masked from 'package:stats':
#> 
#>     chisq.test, fisher.test
```

In data analysis, you will frequently across across the issue of duplication, as well as 
the issue of having difficult column names to work with. One way to deal with difficult
column names is to rename them using `rename()` but you can also use the janitor package
to perform multiple cleaning steps on the column names.

## Arguments

## `clean_names()`

The `clean_names()` function takes the following as arguments:

| Argument | Parameter            | Details                                        |
| -------- | -------------------- | ---------------------------------------------- |
| dat*     | input data frame     |                                                |
| case     | 'title' for big caps | default is 'snake'; see to_any_case for detail |

You can read more about the arguments in the `clean_names()` function documentation
[here](https://garthtarr.github.io/meatR/janitor.html#clean_names()).

## `get_dupes()`

The `get_dupes()` function takes the following as arguments:

| Argument | Parameter        | Details                                         |
| -------- | ---------------- | ----------------------------------------------- |
| dat*     | input data frame |                                                 |
| …        | vector           | vector containing column names we want to check |

You can read more about the arguments in the `get_dupes()` function documentation
[here](https://garthtarr.github.io/meatR/janitor.html#get_dupes()).

## Exercises

Lets start by loading `tidyverse` since we will be using the pipe %>% operator and more.


```r
library(tidyverse)
```



Consider this small dataset of grades.


```r
grades
#> # A tibble: 5 × 4
#>   `Student Initials` `Grade Midterm 1` `Grade Midterm 2`
#>   <chr>                          <dbl>             <dbl>
#> 1 AH                               100                90
#> 2 AE                                86                83
#> 3 HS                                90                79
#> 4 ES                                64                64
#> 5 BT                               100                90
#> # … with 1 more variable: Final Grade % <dbl>
```

Using the `clean_names()` function from janitor, we get:


```r
grades %>% clean_names()
#> # A tibble: 5 × 4
#>   student_initials grade_midterm_1 grade_midterm_2
#>   <chr>                      <dbl>           <dbl>
#> 1 AH                           100              90
#> 2 AE                            86              83
#> 3 HS                            90              79
#> 4 ES                            64              64
#> 5 BT                           100              90
#> # … with 1 more variable: final_grade_percent <dbl>
```

Notice how now everything is lowercased with _ as a separator, and any special characters
like % are converted to words to retain their meaning. `clean_names()` would also handle
column names that are duplicated, but that is not demonstrated here since we already had
unique columns.

### Exercise 1

If, for some reason, you wanted to preserve some existing columns from being cleaned, how
would you use the `clean_names()` function on only the columns you want to clean? For
example, supposed you wanted to keep the Final Grade % column as is. As a hint, you will
need to use functions outside of the janitor package to help with this. Remember the
`dplyr` functions.




```r
grades %>%
  select(-`Final Grade %`) %>%
  clean_names()
#> # A tibble: 5 × 3
#>   student_initials grade_midterm_1 grade_midterm_2
#>   <chr>                      <dbl>           <dbl>
#> 1 AH                           100              90
#> 2 AE                            86              83
#> 3 HS                            90              79
#> 4 ES                            64              64
#> 5 BT                           100              90
```


### Exercise 2

If you wanted to restore the upper casing for some columns, how would you do that? As a
tip, take a look at the Arguments section and see what you can use. Make sure you store
the cleaned data from above in an object called clean, and then apply the new cleaning
step to it.

<!-- ```{r janitor-exercise-2, exercise = TRUE} -->
<!-- clean <-  -->
<!-- clean %>% -->
<!-- ``` -->

<!-- ```{r janitor-exercise-2-solution, exercise = FALSE} -->
<!-- clean <- grades %>% clean_names() -->
<!-- clean %>% clean_names(case = "title") -->
<!-- ``` -->


### Exercise 3

Try using the `get_dupes()` function to get duplicate rows from the cleaned grades data
`clean`.



<!-- ```{r janitor-exercise-3, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r janitor-exercise-3-solution, exercise = FALSE} -->
<!-- clean %>% get_dupes() -->
<!-- ``` -->

What was the result? Did you get anything?

### Exercise 4

Look at the data above and try to see why you did not get anything even though it looks
like two rows are very similar. How can you modify the function call so that you get the
_partially_ duplicate data?

<!-- ```{r janitor-exercise-4, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r janitor-exercise-4-solution, exercise = FALSE} -->
<!-- clean %>% get_dupes(c("grade_midterm_1", "grade_midterm_2", "final_grade_percent")) -->
<!-- ``` -->



## Next Steps

If you would like to learn more, please read about the janitor package in its
documentation [here](https://garthtarr.github.io/meatR/janitor.html).















# `tidyr` package

*Written by Mariam Walaa.*


## Introduction

In this lesson, you will learn how to:

- Use additional `tidyr` functions, such as `unnest_wider()` and `unnest_longer()`

Prerequisite skills include:

- Previous tutorials involving `tidyr` functions

Highlights:

- We can use `tidyr` functions to put a non-tidy dataset into tidy format.
- unnest_wider() and unnest_longer() give flexibility in terms of how to unnest data.

## Overview

A common theme across working with datasets is standardizing the dataset format. Datasets
must be standardized. If every dataset was unique in its format, it would be difficult for
data scientists and data analysts to work on them. Everyone would have a vastly
different workflow needed to reach the analysis step, and people would have a harder time
collaborating with each other and evaluating each other's results. That is why datasets
must be *standardized*.

You may wonder how we can standardize a dataset when we have one, and to what extent we 
can standardize it. In [Hadley Wickham's Tidy Data
paper](https://vita.had.co.nz/papers/tidy-data.html) from 2014, Hadley introduces 3 rules
every dataset must follow in order to be considered tidy: Every row must be an observation,
every column must be a variable, and every cell is a single measurement. Here is an 
illustration that summarizes these 3 rules, by Allison Horst.

<img src="images/59_tidy-data.jpg" width="90%" />

Credits: Allison Horst

As the title says, this section will provide you with a summary of some functions you have
seen in previous tutorials, as well as introduce you to more functions from tidyr that
you have not seen yet.

<img src="images/59_tidy-data-2.jpg" width="90%" />

Credits: Allison Horst

## Example 

Suppose you are given this data that is not in tidy format. 




```r
nontidy_data
#> # A tibble: 3 × 4
#>   variable  `1`       `2`       `3`      
#>   <chr>     <list>    <list>    <list>   
#> 1 n_lines   <dbl [1]> <dbl [1]> <dbl [1]>
#> 2 n_figures <dbl [1]> <dbl [1]> <dbl [1]>
#> 3 n_scripts <dbl [1]> <dbl [1]> <dbl [1]>
```

First, the columns and rows are switched, and second, the cells are all hidden.

Here is the code we need to tidy it:


```r
nontidy_data %>%
  pivot_longer(cols = -variable, names_to = "name", values_to = "value") %>%
  pivot_wider(names_from = "variable") %>%
  unnest(everything())
#> # A tibble: 3 × 4
#>   name  n_lines n_figures n_scripts
#>   <chr>   <dbl>     <dbl>     <dbl>
#> 1 1         100         4        10
#> 2 2         200         5        20
#> 3 3         300         6        30
```

Lets go through this step by step and check the output each time.

To clean it, we will use our functions pivot_longer(), pivot_wider(), and unnest() from
tidyr.


```r
# 1. Convert to long format
nontidy_data_l <- nontidy_data %>%
  pivot_longer(cols = -variable, names_to = 'name', values_to = 'value')
nontidy_data_l
#> # A tibble: 9 × 3
#>   variable  name  value    
#>   <chr>     <chr> <list>   
#> 1 n_lines   1     <dbl [1]>
#> 2 n_lines   2     <dbl [1]>
#> 3 n_lines   3     <dbl [1]>
#> 4 n_figures 1     <dbl [1]>
#> 5 n_figures 2     <dbl [1]>
#> 6 n_figures 3     <dbl [1]>
#> 7 n_scripts 1     <dbl [1]>
#> 8 n_scripts 2     <dbl [1]>
#> 9 n_scripts 3     <dbl [1]>
```

Our dataset is in a long format now.


```r
# 2. Convert to wide format
nontidy_data_w <- nontidy_data_l %>%
  pivot_wider(names_from = 'variable')
nontidy_data_w
#> # A tibble: 3 × 4
#>   name  n_lines   n_figures n_scripts
#>   <chr> <list>    <list>    <list>   
#> 1 1     <dbl [1]> <dbl [1]> <dbl [1]>
#> 2 2     <dbl [1]> <dbl [1]> <dbl [1]>
#> 3 3     <dbl [1]> <dbl [1]> <dbl [1]>
```

Notice how step 2 brings the variable names to the top.


```r
# 3. Unnest (or unfold) the cells
tidy_data <- nontidy_data_w %>%
  unnest(everything())
tidy_data
#> # A tibble: 3 × 4
#>   name  n_lines n_figures n_scripts
#>   <chr>   <dbl>     <dbl>     <dbl>
#> 1 1         100         4        10
#> 2 2         200         5        20
#> 3 3         300         6        30
```

Now it is tidy data. You can also clean it up as follows:


```r
tidy_data %>%
  column_to_rownames('name')
#>   n_lines n_figures n_scripts
#> 1     100         4        10
#> 2     200         5        20
#> 3     300         6        30
```

## Exercises



We will be looking at a data set of Broadway shows with variables about the performances,
attendance, and revenue for theaters that are part of The Broadway League. You can learn
more about the data set provided by Alex Cookson in this [Git
repository](https://github.com/tacookson/data) as well as this corresponding [blog
post](https://www.alexcookson.com/post/most-successful-broadway-show-of-all-time/). Take a
look at a subset of this data for the Winter Garden Theatre.


```r
winter_garden
#> # A tibble: 44 × 2
#> # Groups:   week_number [2]
#>    week_number show 
#>          <dbl> <chr>
#>  1           1 Cats 
#>  2           2 Cats 
#>  3           1 Cats 
#>  4           2 Cats 
#>  5           1 Cats 
#>  6           2 Cats 
#>  7           1 Cats 
#>  8           2 Cats 
#>  9           1 Cats 
#> 10           2 Cats 
#> # … with 34 more rows
```

You can Click Next to look through the observations.

### Exercise 1

<!-- ```{r tidyr-exercise-1, echo = FALSE} -->
<!-- question("Without using the nest() function, how many rows and columns do we have after nesting?", -->
<!--          answer("2 rows and 2 columns", correct = TRUE), -->
<!--          answer("44 rows and 2 columns"), -->
<!--          answer("44 rows and 3 columns"), -->
<!--          answer("2 rows and 3 columns"), -->
<!--          allow_retry = TRUE, -->
<!--          random_answer_order = TRUE) -->
<!-- ``` -->

<!-- #### Exercise 2 -->

<!-- Try the nest() function. Do you get the expected result? -->

<!-- ```{r tidyr-exercise-2, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r tidyr-exercise-2-sol, echo = FALSE} -->
<!-- tidyr_ex2_sol <- winter_garden %>% nest(data = c(show)) -->
<!-- ``` -->


<!-- #### Exercise 3 -->

<!-- ```{r tidyr-exercise-3, echo = FALSE} -->
<!-- question("Consider the code from Exercise 2. What would the sizes of each of the nested data frames be?", -->
<!--          answer("22 rows by 1 column", correct = TRUE), -->
<!--          answer("1 row by 22 columns"), -->
<!--          answer("44 rows by 1 column"), -->
<!--          answer("1 row by 44 columns"), -->
<!--          allow_retry = TRUE, -->
<!--          random_answer_order = TRUE) -->
<!-- ``` -->

<!-- #### Exercise 4 -->

<!-- ```{r tidyr-exercise-4, echo = FALSE} -->
<!-- question("Consider the code from Exercise 2. Without using the unnest_longer() function, how many rows and columns are in this dataset after unnesting longer?", -->
<!--          answer("22 rows by 1 column"), -->
<!--          answer("1 row by 22 columns"), -->
<!--          answer("44 rows by 2 columns", correct = TRUE), -->
<!--          answer("1 row by 44 columns"), -->
<!--          allow_retry = TRUE, -->
<!--          random_answer_order = TRUE) -->
<!-- ``` -->

<!-- #### Exercise 5 -->

<!-- Take a look at another subset of the data set, for Palace Theatre this time.  -->

<!-- ```{r tidyr-data-2-1} -->
<!-- palace -->
<!-- ``` -->

<!-- ```{r tidyr-exercise-5, echo = FALSE} -->
<!-- question("Which of these functions gives us 12 rows and 2 columns?", -->
<!--          answer("nest()", correct = TRUE), -->
<!--          answer("unnest()"), -->
<!--          answer("unnest_wider()"), -->
<!--          answer("unnest_longer()"), -->
<!--          allow_retry = TRUE, -->
<!--          random_answer_order = TRUE) -->
<!-- ``` -->

## Next Steps

- Try looking at `vignette("rectangle")`! This is more advanced than what you have seen in
this tutorial, but if you are interested, then this might be helpful.







