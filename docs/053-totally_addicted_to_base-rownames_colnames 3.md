


# row and column names

*Written by Leuven Wang and last updated on 7 October 2021.*

## Introduction

Data frames can be very well organized and if you're anything like me, you might sometimes even find them aesthetically pleasing in their clean simplicity. But sometimes, their rows and columns can be named with unintelligible or extremely long headings not meant for human review. This may be undesirable in cases where you need to present your data frame in tables or would like to understand them more intuitively during the analytics stage.

In this lesson, you will learn how to:

- Use `colnames()` to retrieve and set column names.
- Use `row.names()` to retrieve and set row names.

Prerequisites:

- Basic understanding of vectors `c()`.
- General knowledge of basic data frame structures i.e. what records and columns are.
- Indexing and subsets of vectors and data frames.

Let's stick with a dataset we're familiar with: `mtcars`. For simplicity, we will use only the first 5 columns of the dataset.


```r
data <- mtcars[1:5]
head(data)
#>                    mpg cyl disp  hp drat
#> Mazda RX4         21.0   6  160 110 3.90
#> Mazda RX4 Wag     21.0   6  160 110 3.90
#> Datsun 710        22.8   4  108  93 3.85
#> Hornet 4 Drive    21.4   6  258 110 3.08
#> Hornet Sportabout 18.7   8  360 175 3.15
#> Valiant           18.1   6  225 105 2.76
```
The column names are the headers at the top of the column. In this case they are mpg, cyl, disp, hp, and drat. The row names are the unique identifiers that head each record. It is important to know that row names do not exist under a column variable the same way that the rest of their record does. In this case, our row names are the models of cars: Mazda RX4, Mazda RX4 Wag, etc...


## Using `colnames()`

Now, if you work a lot with this dataset or you just happen to be a car aficionado you may know what these column headings mean. But for us mere plebes, this isn't so intuitive! A full description of the column variables can be found [here](https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/mtcars.html).

Using `colnames` and a vector of names of length matching the number of columns, we can change each column's name. 


```r
colnames(data) <- c("Miles/Gallon", "Cylinders", "Displacement", "Horsepower", "Rear Axle Ratio")
head(data)
#>                   Miles/Gallon Cylinders Displacement
#> Mazda RX4                 21.0         6          160
#> Mazda RX4 Wag             21.0         6          160
#> Datsun 710                22.8         4          108
#> Hornet 4 Drive            21.4         6          258
#> Hornet Sportabout         18.7         8          360
#> Valiant                   18.1         6          225
#>                   Horsepower Rear Axle Ratio
#> Mazda RX4                110            3.90
#> Mazda RX4 Wag            110            3.90
#> Datsun 710                93            3.85
#> Hornet 4 Drive           110            3.08
#> Hornet Sportabout        175            3.15
#> Valiant                  105            2.76
```
Note that using the `colnames()` function on our `data` variable automatically changes the column names inside! If we use a vector with less elements than the the number of columns, the first few column names will change and the others will become nameless. Using a vector with a length that exceeds the number of columns results in an error.

```r
colnames(data) <- c("Miles/Gallon", "Cylinders")
head(data)
#>                   Miles/Gallon Cylinders  NA  NA   NA
#> Mazda RX4                 21.0         6 160 110 3.90
#> Mazda RX4 Wag             21.0         6 160 110 3.90
#> Datsun 710                22.8         4 108  93 3.85
#> Hornet 4 Drive            21.4         6 258 110 3.08
#> Hornet Sportabout         18.7         8 360 175 3.15
#> Valiant                   18.1         6 225 105 2.76
```
If you want to change a single specific column's name, you can reference it by index and use characters instead of vectors:

```r
colnames(data)[3] <- "Displacement"
head(data)
#>                   Miles/Gallon Cylinders Displacement  NA
#> Mazda RX4                 21.0         6          160 110
#> Mazda RX4 Wag             21.0         6          160 110
#> Datsun 710                22.8         4          108  93
#> Hornet 4 Drive            21.4         6          258 110
#> Hornet Sportabout         18.7         8          360 175
#> Valiant                   18.1         6          225 105
#>                     NA
#> Mazda RX4         3.90
#> Mazda RX4 Wag     3.90
#> Datsun 710        3.85
#> Hornet 4 Drive    3.08
#> Hornet Sportabout 3.15
#> Valiant           2.76
```
And of course, if you want to change a subset of column names, you can reference it with index and use vectors:

```r
colnames(data)[4:5] <- c("Horsepower","Rear Axle Ratio")
head(data)
#>                   Miles/Gallon Cylinders Displacement
#> Mazda RX4                 21.0         6          160
#> Mazda RX4 Wag             21.0         6          160
#> Datsun 710                22.8         4          108
#> Hornet 4 Drive            21.4         6          258
#> Hornet Sportabout         18.7         8          360
#> Valiant                   18.1         6          225
#>                   Horsepower Rear Axle Ratio
#> Mazda RX4                110            3.90
#> Mazda RX4 Wag            110            3.90
#> Datsun 710                93            3.85
#> Hornet 4 Drive           110            3.08
#> Hornet Sportabout        175            3.15
#> Valiant                  105            2.76
```


Conversely, if we wanted to retrieve the current column names in the table, we can also call upon `colnames()`:

```r
colnames(data)
#> [1] "Miles/Gallon"    "Cylinders"       "Displacement"   
#> [4] "Horsepower"      "Rear Axle Ratio"
```
The same can be done for singular or subsets of columns.

`colnames()` also applies to tibbles:


```r
colnames(tibble(data))
#> [1] "Miles/Gallon"    "Cylinders"       "Displacement"   
#> [4] "Horsepower"      "Rear Axle Ratio"
```

## Using `row.names()`

Similarly, `row.names()` is used to handle row names. Most of the time, row names are just unique ordered numbers. In the case of our dataset, our row names are car models. The problem with row names is that because they are not grouped under a column variable, they can't be subjected to the same `filter()`, `select()` or handling functions that the rest of the data is. This may be problematic at times.

Let's say we need the car model names to be a column variable. We can first use `row.names()` to retrieve them:


```r
car_models <- row.names(data)
car_models
#>  [1] "Mazda RX4"           "Mazda RX4 Wag"      
#>  [3] "Datsun 710"          "Hornet 4 Drive"     
#>  [5] "Hornet Sportabout"   "Valiant"            
#>  [7] "Duster 360"          "Merc 240D"          
#>  [9] "Merc 230"            "Merc 280"           
#> [11] "Merc 280C"           "Merc 450SE"         
#> [13] "Merc 450SL"          "Merc 450SLC"        
#> [15] "Cadillac Fleetwood"  "Lincoln Continental"
#> [17] "Chrysler Imperial"   "Fiat 128"           
#> [19] "Honda Civic"         "Toyota Corolla"     
#> [21] "Toyota Corona"       "Dodge Challenger"   
#> [23] "AMC Javelin"         "Camaro Z28"         
#> [25] "Pontiac Firebird"    "Fiat X1-9"          
#> [27] "Porsche 914-2"       "Lotus Europa"       
#> [29] "Ford Pantera L"      "Ferrari Dino"       
#> [31] "Maserati Bora"       "Volvo 142E"
```

As `car_models` preserves the same order as before, we can add easily add it to the rest of the data frame as a normal column:

```r
data <- cbind(car_models, data)
#cbind() is used to combine columns and datasets together to form a new dataset. Other methods exist but for the purposes of our demonstration we shall use it here. It's not important for you to understand it thus far but it is useful.
head(data)
#>                          car_models Miles/Gallon Cylinders
#> Mazda RX4                 Mazda RX4         21.0         6
#> Mazda RX4 Wag         Mazda RX4 Wag         21.0         6
#> Datsun 710               Datsun 710         22.8         4
#> Hornet 4 Drive       Hornet 4 Drive         21.4         6
#> Hornet Sportabout Hornet Sportabout         18.7         8
#> Valiant                     Valiant         18.1         6
#>                   Displacement Horsepower Rear Axle Ratio
#> Mazda RX4                  160        110            3.90
#> Mazda RX4 Wag              160        110            3.90
#> Datsun 710                 108         93            3.85
#> Hornet 4 Drive             258        110            3.08
#> Hornet Sportabout          360        175            3.15
#> Valiant                    225        105            2.76
```
The problem now is that we have the car models both within the table as a variable and outside of it as row names. We can now use `row.names()` to fix this redundancy and maintain a guaranteed unique identifier for rows. Using an empty vector numbers the row names in ascending order:

```r
row.names(data) <- c()
head(data)
#>          car_models Miles/Gallon Cylinders Displacement
#> 1         Mazda RX4         21.0         6          160
#> 2     Mazda RX4 Wag         21.0         6          160
#> 3        Datsun 710         22.8         4          108
#> 4    Hornet 4 Drive         21.4         6          258
#> 5 Hornet Sportabout         18.7         8          360
#> 6           Valiant         18.1         6          225
#>   Horsepower Rear Axle Ratio
#> 1        110            3.90
#> 2        110            3.90
#> 3         93            3.85
#> 4        110            3.08
#> 5        175            3.15
#> 6        105            2.76
```
See how the rows are now numbered as their names? Of course, you can also customarily name your rows and use subsetting:

```r
row.names(data)[1:2] <- c("Hot Wheels","Not so Hot Wheels")
head(data)
#>                          car_models Miles/Gallon Cylinders
#> Hot Wheels                Mazda RX4         21.0         6
#> Not so Hot Wheels     Mazda RX4 Wag         21.0         6
#> 3                        Datsun 710         22.8         4
#> 4                    Hornet 4 Drive         21.4         6
#> 5                 Hornet Sportabout         18.7         8
#> 6                           Valiant         18.1         6
#>                   Displacement Horsepower Rear Axle Ratio
#> Hot Wheels                 160        110            3.90
#> Not so Hot Wheels          160        110            3.90
#> 3                          108         93            3.85
#> 4                          258        110            3.08
#> 5                          360        175            3.15
#> 6                          225        105            2.76
```


## Common Mistakes and Errors

- Incorrect indexing when working with specific or subsets of columns/rows. In R, indexing begins at 1.
- Trying to set row names with a vector of length shorter than the number of rows you're changing.


## Exercises

### Question 1

Given the dataset `iris`, change the column names such that the periods are replaced with spaces."

<!-- ```{r q1_colnames, exercise.eval = TRUE, exercise = TRUE} -->
<!-- head(iris) -->
<!-- ``` -->

<!-- ```{r q1_colnames-solution} -->
<!-- colnames(iris) <- c("Sepal Length", "Sepal Width", "Petal Length", "Petal Width", "Species") -->
<!-- ``` -->

### Question 2

<!-- ```{r q2_rowname, echo=FALSE} -->
<!-- question("True or false: Just as with columns, setting row names using a vector of length shorter than the number of records results in any outstanding rows to have no name assigned.",  -->
<!--          answer("True"),  -->
<!--          answer("False", correct= TRUE, message = "Unlike with column names, setting row names with a vector shorter than the number of selected rows results in an error.")) -->
<!-- ``` -->

### Question 3

<!-- ```{r q3_rownames, echo = FALSE} -->
<!-- question("True or false: `colname` can be used to retrieve and change the name of singular columns.", -->
<!--          answer("True", message = "There is no such thing as `colname`. "), -->
<!--          answer("False", correct= TRUE, message = "There is no such thing as `colname`. ") -->
<!--          ) -->


<!-- ``` -->

<!-- ### Question 4 -->
<!-- ```{r include=FALSE} -->
<!-- iris <- og_iris -->
<!-- ``` -->



Given an unmodified version of `iris`, fix the mistake in the code below such that it successfully changes the column of the first two columns to "Sepal Length" and "Sepal Width".

<!-- ```{r q4_colnames, exercise.eval = TRUE, exercise = TRUE} -->
<!-- colnames(iris)[0:1] <- c("Sepal Length", "Sepal Width") -->
<!-- head(iris) -->
<!-- ``` -->

<!-- ```{r q4_colnames-solution} -->
<!-- colnames(iris)[1:2] <- c("Sepal Length", "Sepal Width") -->
<!-- ``` -->


### Question 5
For each car in `mtcars`, print a string which says "I want to drive the 'car_name'". Your final output should look something like this:

I want to drive the Mazda RX4  
I want to drive the Mazda Rx4 Wag  
I want to drive the Datsun 710  
...

Tip: use `cat("I want to drive the ", car_name, "\n")` to print your outputs.


<!-- ```{r q5_rownames, exercise.eval = TRUE, exercise = TRUE} -->
<!-- head(mtcars) -->
<!-- ``` -->


<!-- ```{r q5_rownames-solution} -->
<!-- car_names <- row.names(mtcars) -->

<!-- for(car_name in car_names){ -->
<!--   cat("I want to drive the", car_name, "\n") -->
<!-- } -->
<!-- ``` -->

### Question 6

Change the row name of the second record of `mtcars` to be the exact same as the first record without changing the first record. See what happens and read the message. Then, figure out a way to swap the two row names without prompting an error.


<!-- ```{r q6_rownames, exercise.eval = TRUE, exercise = TRUE} -->
<!-- head(mtcars) -->
<!-- ``` -->


<!-- ```{r q6_rownames-solution} -->
<!-- a <- row.names(mtcars)[1] -->
<!-- b <- row.names(mtcars)[2] -->
<!-- row.names(mtcars)[1:2] <- c(b,a) -->
<!-- ``` -->

## References

- [row.names()](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/row.names)
- [Row and Column Names](https://stat.ethz.ch/R-manual/R-devel/library/base/html/colnames.html)

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
