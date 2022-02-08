


# head, tail, glimpse and summary

*Written by Haoluan Chen and last updated on 7 October 2021.*

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
