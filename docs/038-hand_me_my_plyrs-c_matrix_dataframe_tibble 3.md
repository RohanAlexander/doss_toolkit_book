


# Representations of data

*Written by Matthew Wankiewicz and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn:

- What a vector is and how to create one in R.
- The difference between matrices, dataframes and tibbles.
- How to create matrices, dataframes and tibbles in R.

Prerequisite skills include:

- R installed on your computer/RStudio cloud account

Highlights:

- Vectors are data structures in R which can contain numbers, words, or logical operators among others.
  - The `c()` function is usually the main way of creating vectors.
- Matrices are objects in R that contain rows and columns. These matrices can be added and subtracted along with other matrices.
  - The `matrix()` function helps with creating matrices.
- Dataframes are objects in R which are similar to matrices. Dataframes can be built out of multiple vectors.
  - The `data.frame()` function allows us to create dataframes in R.
- Tibbles are dataframes, but they are easier to use with functions in R. Since R has been in use for many years, tibbles allow us to do more with data, when compared to dataframes.
  - The `tibble()` function creates tibbles in R.

## The content

- Vectors are a type of data structure in R which contains observations of the same type. Vectors can include sets of numbers, a group of names or a group of randomly selected logical operators (True or False). When creating a vector, R requires all elements of the vector to be the same type, this means that it is possible to create vectors with numbers and words, but the numbers will be stored as characters. 

- Matrices are two dimensional and are similar to the structure of vectors. Matrices can contain words and numbers, but are mainly used with numbers. Matrices are usually created with numbers because there is the ability to conduct matrix operations like addition, subtraction, division and multiplication between different matrices. Matrices have a fixed number of rows and columns.

- Dataframes are another way of storing data and are mainly used for storing tables. The benefit to using dataframes over matrices is when your data contains numbers and words. Dataframes are able to contain columns of numbers and columns of words while matrices can only contain numbers or words. Dataframes are also useful because it is possible to conduct operations between columns, which will be shown in the Questions section of this lesson.

- As mentioned in the introduction, tibbles are very similar to dataframes but they are more compatible with current uses for R. This is because some older operations in R aren't as useful as they were when R was created, so tibbles had to be created to make some operations run better. Tibbles are created using the `tibble()` function which can be found in the `tidyverse` package, which is different than the other data types discussed above, because they can be created using the base R functions. 


## Vectors

- **`c()`:** The `c()` function takes one main argument and includes optional arguments. The main argument for `c()` are the values that you want to save as a vector. The arguments used can be any set of numbers or words, or both. For example we would use an entry could be: `test <- c("This", "is", "example", 1)`. If you do save numbers in words in the same vector, R will convert the number into a character instead of keeping it as an integer.
  
  - The optional arguments for `c()` are `recursive =` and `use.names =`. The recursive function is useful when the items you are vectoring includes a list. If you set `recursive = TRUE` it breaks down the list and converts it into a vector. If `recursive = FALSE` the vector is saved as a list (by default, `recursive = FALSE`, and it usually stays that way). The argument `use.names =` tells R whether or not to keep the names of the lists present when the vector is saved.
  
### Examples

You can easily create vectors using the `c()` function. Run the code chunk below to see.

```r
vector1 <- c(1, 2, 3, 4)
vector1
#> [1] 1 2 3 4
```

As mentioned in previous sections of this lesson, you can create a vector of both numbers and words, but the numbers will be saved as characters.

```r
vector2 <- c("stats", "is", "number", 1)
vector2
#> [1] "stats"  "is"     "number" "1"

## using class tells us the class of the objects in the vector 
class(vector2)
#> [1] "character"
```

You can also index vectors by using square brackets ([]). To index a value of an R vector, write the vector name and then in the square brackets, the position of that value in the vector.

```r
vector <- c("a", "b", "c", "d", "e") ## save our vector

vector[3] ## if we want to select c, it is the third element so we write vector[3]
#> [1] "c"

vector[-3] ## if we want to return the vector without the letter c, type vector[-3]
#> [1] "a" "b" "d" "e"
```

We can also add, subtract, multiply and divide vectors.

```r
vec1 <- c(2, 4, 6)
vec2 <- c(3, 6, 9)

vec1 + vec2
#> [1]  5 10 15
vec1*vec2
#> [1]  6 24 54
```


## Matrices

- **`matrix()`:** The `matrix()` function takes 5 arguments, 3 of them are the most important. The first one is `data`, which is the data you plan to make a matrix with, this can contain multiple vectors. The next argument is `nrow` which is the number of rows you want to have and `ncol` which is the number of columns you want to include in your matrix.

  - There are two optional arguments, `byrow` and `dimnames`. `byrow` can either be true or false, if false, the entries for the matrix are added by filling out the columns as opposed to filling out the data row by row. `dimnames` allows you to name the rows and the columns of your matrix.
  
### Examples

If we use the matrix function on a set of numbers without specifying the number of rows/columns, you get a matrix with one column.


```r
matrix1 <- matrix(c(1, 2, 3, 4, 5, 6, 7, 8, 9))
matrix1
#>       [,1]
#>  [1,]    1
#>  [2,]    2
#>  [3,]    3
#>  [4,]    4
#>  [5,]    5
#>  [6,]    6
#>  [7,]    7
#>  [8,]    8
#>  [9,]    9
```

Using the `nrow` and `ncol` arguments, we can tell R how we want our matrix to look. 

```r
matrix2 <- matrix(c(1, 2, 3, 4, 5, 6, 7, 8, 9), nrow = 3, ncol = 3)
matrix2
#>      [,1] [,2] [,3]
#> [1,]    1    4    7
#> [2,]    2    5    8
#> [3,]    3    6    9
```

The next chunk will show the use the `byrow` argument to fill out our matrix. You will notice that when comparing the output of this chunk to the one above, other than the diagonals, the entries are all different.

```r
matrix3 <- matrix(c(1, 2, 3, 4, 5, 6, 7, 8, 9), nrow = 3, ncol = 3, byrow = T)
matrix3
#>      [,1] [,2] [,3]
#> [1,]    1    2    3
#> [2,]    4    5    6
#> [3,]    7    8    9
```

We can also add, subtract, multiply and divide matrices

```r
mat1 <- matrix(c(1, 2, 3, 4, 5, 6, 7, 8, 9), nrow = 3, ncol = 3, byrow = T)
mat1
#>      [,1] [,2] [,3]
#> [1,]    1    2    3
#> [2,]    4    5    6
#> [3,]    7    8    9
mat2 <- matrix(c(1, 2, 3, 4, 5, 6, 7, 8, 9), nrow = 3, ncol = 3, byrow = F)
mat2
#>      [,1] [,2] [,3]
#> [1,]    1    4    7
#> [2,]    2    5    8
#> [3,]    3    6    9

mat1 - mat2
#>      [,1] [,2] [,3]
#> [1,]    0   -2   -4
#> [2,]    2    0   -2
#> [3,]    4    2    0

mat1/mat2
#>          [,1]     [,2]      [,3]
#> [1,] 1.000000 0.500000 0.4285714
#> [2,] 2.000000 1.000000 0.7500000
#> [3,] 2.333333 1.333333 1.0000000
```


We can also multiply vectors and matrices

```r
mat1 <- matrix(c(1:9), nrow = 3)
mat1
#>      [,1] [,2] [,3]
#> [1,]    1    4    7
#> [2,]    2    5    8
#> [3,]    3    6    9
vec1 <- c(1:3)
vec1
#> [1] 1 2 3

mat1*vec1
#>      [,1] [,2] [,3]
#> [1,]    1    4    7
#> [2,]    4   10   16
#> [3,]    9   18   27
```

Be sure to notice that multiplication with vectors and matrics is different from typical operations between vectors and matrices. In R these operation will be conducted by elements, which is why for the example above we don't get a 1x3 vector. 

Matrices can be also indexed.

```r
mat2 <- matrix(c(1, 2, 3, 4, 5, 6, 7, 8, 9), nrow = 3, ncol = 3, byrow = F)
mat2
#>      [,1] [,2] [,3]
#> [1,]    1    4    7
#> [2,]    2    5    8
#> [3,]    3    6    9

mat2[3,3] ## third row, third column
#> [1] 9
```
  

  
## Data Frames

- **`data.frame()`:** The main argument that `data.frame()` takes is the data that you want to become a dataframe. To name the columns, you can write `"name" = c()` where c() is the vector of numbers/words. You can name each column by repeating the `"name" = c()` line. The other important argument is `row.names`. For this argument you can write a name for each row in a vector that has the same length as the number of rows as your dataframe. 

  - `data.frame()` contains 4 optional arguments. `check.rows` checks if the rows are consistent in their length and names. `check.names` checks if your column names are unique and there aren't any repeats. `fix.empty.names` automatically names any columns with missing variable names (this is set to true by default). Lastly, `stringsAsFactors` converts character vectors into factors if set to true (set to true by default).
  
### Examples

As mentioned in the Arguments section, there are many ways to create a dataframe. For this one, we'll just insert two vectors into the function, without naming them.

```r
data.frame(c(1,2,3), c(2,4,6))
#>   c.1..2..3. c.2..4..6.
#> 1          1          2
#> 2          2          4
#> 3          3          6
```
We can see that without naming the vectors, `data.frame()` names the rows "c.1..2..3" and "c.2..4..6".


Now we can do the same as above, but save the vectors beforehand and then add them into the function.

```r
vector1 <- c(1:3) ## this is another way writing 1,2,3
data.frame(vector1, vector2 = c(2,4,6))
#>   vector1 vector2
#> 1       1       2
#> 2       2       4
#> 3       3       6
```

We can also take a matrix and convert the matrix into a dataframe. We can also use the `row.names` argument.

```r
mat <- matrix(1:9, nrow = 3)
mat
#>      [,1] [,2] [,3]
#> [1,]    1    4    7
#> [2,]    2    5    8
#> [3,]    3    6    9

df <- data.frame(mat, row.names = c("a", "b", "c"))
df
#>   X1 X2 X3
#> a  1  4  7
#> b  2  5  8
#> c  3  6  9
```


For the last example of making dataframes, we will make use of the `check.names` and `stringsAsFactors` arguments

```r
vector1 <- c(1:3)
df <- data.frame(vector1, vector1 = c("one", "two", "three"), check.names = TRUE, 
                 stringsAsFactors = TRUE)
df
#>   vector1 vector1.1
#> 1       1       one
#> 2       2       two
#> 3       3     three

class(df$vector1.1)
#> [1] "factor"
```
We can see that the dataframe has two columns, vector1 and vector1.1 and if we don't do that, the columns will have the same name and will be a headache to work with. Also note that the class of the `vector1.1` column is now a factor. It was initially written as a vector with characters in it, but the `stringsAsFactors` has now changed it a factor.


We can also index values in dataframes.

```r
df <- data.frame(c(1,2,3), c(2,4,6), c(3, 6, 9))

df[2,2] #to select the number 4 in the center we write df[2,2]
#> [1] 4

df[,2] ## to return the whole 2nd column, write df[,2]
#> [1] 2 4 6

df[2,] ## to select only the 2nd row, write df[2,]
#>   c.1..2..3. c.2..4..6. c.3..6..9.
#> 2          2          4          6

df[-1,] ## you can also return dataframes without rows/columns by including "-"
#>   c.1..2..3. c.2..4..6. c.3..6..9.
#> 2          2          4          6
#> 3          3          6          9
```
  
## Tibbles

- **`tibble()`:** Similar to `data.frame()`, the main argument for `tibble()` is the data you want to turn into a tibble. The data can include vectors, matrices and even dataframes. You can name the columns in a similar way to `data.frame()` by writing the name and then the data you want to be stored in that column.

  - There are two optional arguments for `tibble()`, they are `.rows` and `.name_repair`. `.rows` tells R how many rows you want your tibble to be, you do not have to fill this argument out but it can be useful if you want to confirm that your data has the same amount of rows as you wish. If the number of rows given into the main argument does not match the `.rows` argument, an error will occur. `.name_repair` helps fix issues with column names, it has 5 types of repair. "Minimal" does not change or check column names, "Unique" makes sure names are not empty, "check_unique" makes sure the names are unique, "universal" checks that the names are unique and follow proper syntax. The final option for `.name_repair` is a custom function you can create on your own so the names follow a certain style.

### Questions

Like dataframes, tibbles can be created from vectors

```r
vector1 <- c(1:3)
vector2 <- c(2,4,6)

data <- tibble(vector1, vector2)
data
#> # A tibble: 3 × 2
#>   vector1 vector2
#>     <int>   <dbl>
#> 1       1       2
#> 2       2       4
#> 3       3       6
```

Tibbles can also be created from matrices. This can be done using the `as_tibble()` function.

```r
mat1 <- matrix(1:9, nrow = 3, ncol = 3) ## 3x3 matrix
mat1
#>      [,1] [,2] [,3]
#> [1,]    1    4    7
#> [2,]    2    5    8
#> [3,]    3    6    9

tib <- as_tibble(mat1)
tib
#> # A tibble: 3 × 3
#>      V1    V2    V3
#>   <int> <int> <int>
#> 1     1     4     7
#> 2     2     5     8
#> 3     3     6     9
```

Similarly, dataframes can be converted into tibbles.

```r
df1 <- data.frame("id" = c(1,2,3), "sport" = c("soccer", "baseball", "basketball"),
                  "name" = c("Messi", "Bichette", "James"))
df1
#>   id      sport     name
#> 1  1     soccer    Messi
#> 2  2   baseball Bichette
#> 3  3 basketball    James

tibble(df1, .rows = 3) ## we can use .rows to confirm that there will be 3 rows.
#> # A tibble: 3 × 3
#>      id sport      name    
#>   <dbl> <chr>      <chr>   
#> 1     1 soccer     Messi   
#> 2     2 baseball   Bichette
#> 3     3 basketball James
```

Tibbles can also be indexed.

```r
tib1 <- tibble(data.frame("id" = c(1,2,3), "sport" = c("soccer", "baseball", "basketball"),
                  "name" = c("Messi", "Bichette", "James")))
tib1
#> # A tibble: 3 × 3
#>      id sport      name    
#>   <dbl> <chr>      <chr>   
#> 1     1 soccer     Messi   
#> 2     2 baseball   Bichette
#> 3     3 basketball James

tib1[1,3] ## 1st row, 3rd column
#> # A tibble: 1 × 1
#>   name 
#>   <chr>
#> 1 Messi
```

If we create an identical dataframe and tibble and index the same location, we will get a tibble from the tibble and a specific value from the dataframe

```r
df_index <- data.frame(x = c(1:3), y = c(4:6), z = c(7:9))

tib_index <- tibble(df_index)


df_index[2,2]
#> [1] 5
tib_index[2,2]
#> # A tibble: 1 × 1
#>       y
#>   <int>
#> 1     5
```
The dataframe gives us the integer 5 while the tibble gives us a 1x1 tibble with 5 as the only entry.


Lastly, you can make tibbles where the columns are mathematical operations between columns.

```r
col1 <- c(1:10)
tibble(col1, col2 = col1+10, col3 = (col1+col2)*100)
#> # A tibble: 10 × 3
#>     col1  col2  col3
#>    <int> <dbl> <dbl>
#>  1     1    11  1200
#>  2     2    12  1400
#>  3     3    13  1600
#>  4     4    14  1800
#>  5     5    15  2000
#>  6     6    16  2200
#>  7     7    17  2400
#>  8     8    18  2600
#>  9     9    19  2800
#> 10    10    20  3000
```


## Exercises

<!-- ```{r quiz1-vectors, echo=F} -->
<!-- question_checkbox( "1. Which data types are part of base R? Select all that apply.", -->
<!--   answer("Tibbles"), -->
<!--   answer("Dataframes", correct = T), -->
<!--   answer("Vectors", correct = T), -->
<!--   answer("Matrices", correct = T), -->
<!--   incorrect = paste0("Incorrect."), -->
<!--   allow_retry = T, -->
<!--   random_answer_order = T -->
<!-- ) -->
<!-- ``` -->


<!-- **2.** This question will combine vectors and dataframes. Create two vectors, the first one (call it 'numbers') containing the numbers 10, 20, 30 and 40, and the second one (call it 'cities') containing the words: 'Toronto', 'New York', 'Boston' and 'Vancouver'. Now, take those two vectors and turn them into a dataframe. (Hint: The `c()` and `data.frame()` function will be very helpful.) -->
<!-- ```{r quiz2-vectors, exercise = TRUE} -->
<!-- ## Enter code below -->
<!-- numbers <- c(10) -->
<!-- cities <- c('Toronto') -->
<!-- ``` -->

<!-- ```{r quiz2-vectors-solution} -->

<!-- numbers <- c(10, 20, 30, 40) -->
<!-- cities <- c('Toronto', 'New York', 'Boston', 'Vancouver') -->
<!-- data.frame(numbers, cities) -->
<!-- ``` -->

<!-- **3.** Make a tibble with the first column being the set of numbers from 1 to 10, the second column being the first column times 7 and the third column being the sum of columns 1 and 2. -->

<!-- ```{r quiz3-vectors, exercise = TRUE} -->
<!-- ## enter code below -->
<!-- col1 <- c(1:2) -->
<!-- ``` -->

<!-- ```{r quiz3-vectors-solution} -->

<!-- col1 <- c(1:10) -->
<!-- tibble(col1, col2 = col1*7, col3 = col1 + col2)  -->

<!-- ## OR -->

<!-- col1 <- c(1:10) -->
<!-- col2 <- col1*7 -->
<!-- col3 <- col1 + col2 -->

<!-- tibble(col1, col2, col3) -->
<!-- ``` -->


<!-- **4.** The next question follows the code chunk below. -->

<!-- ```{r quiz4-tibble, results = "hide"} -->
<!-- cities <- c("Toronto", "New York", "Vancouver", "Montreal", "Chicago", "Los Angeles") -->
<!-- rank <- c(1, 2, 3, 4, 5, 6) -->

<!-- tibble(cities, rank, pop = rank*1000,  -->
<!--        rank_plus_pop = rank + pop) -->
<!-- ``` -->

<!-- ```{r quiz4-tibble1, echo=F} -->
<!-- question("How many columns are present in the data?", -->
<!--          answer("4", correct = TRUE), -->
<!--          answer("3"), -->
<!--          answer("2"), -->
<!--          answer("5")) -->
<!-- ``` -->

<!-- ```{r quiz4-tibble2, echo=F} -->
<!-- question("What would be that class of the output of the `tibble` function?", -->
<!--          answer("Vector"), -->
<!--          answer("Matrix"), -->
<!--          answer("Tibble or (tbl)", correct = T), -->
<!--          answer("None of the options.")) -->
<!-- ``` -->

<!-- ```{r quiz4-tibble3, echo=F} -->
<!-- question("How many rows will the data have?", -->
<!--          answer("7"), -->
<!--          answer("3"), -->
<!--          answer("6", correct = T), -->
<!--          answer("5")) -->
<!-- ``` -->


<!-- **5.** For this exercise, create a dataframe containing 3 vectors: one containing a set of 5 numbers, another containing a set of 5 animals and another containing a set of 5 cities. Name the columns of this dataframe 'id', 'animal', 'city'. Save this dataframe under the name 'df' and then convert it into a tibble. -->
<!-- ```{r vec-df-ex1, exercise = TRUE} -->
<!-- ## enter code below -->
<!-- ``` -->

<!-- ```{r vec-df-ex1-solution} -->

<!-- ## Your answers may be different -->
<!-- df <- data.frame(id = c(1:5), animal = c("Dog", "Cat", "Goat", "Bird", "Lion"), -->
<!--                  city = c("Toronto", "San Diego", "New York", "Boston", "Washington") -->
<!--                  ) -->
<!-- tibble(df) -->

<!-- ## OR -->

<!-- id <- c(1:5) -->
<!-- animal <- c("Dog", "Cat", "Goat", "Bird", "Lion") -->
<!-- city <- c("Toronto", "San Diego", "New York", "Boston", "Washington") -->

<!-- df <- data.frame(id, animal, city) -->
<!-- tibble(df) -->
<!-- ``` -->

## Common Mistakes & Errors

- **Vectors**
  - If you try to index a vector and the vector returns 'NA', that likely means that you are trying to index an element that isn't in your vector. To fix this, you need to include a number that is **less than or equal to** the length of your vector.

- **Matrices**
  - Error in matrix[n,m] : subscript out of bounds
    - This error means that you are trying to index a point in the matrix that doesn't exist. Similar to vectors, move the subscript to be inside the lengths of your matrix.
  - In matrix(c(1, 2, 3, 4, 5, 6, 7, 8, 9), nrow = 4, byrow = F) :
  data length [9] is not a sub-multiple or multiple of the number of rows [4]
    - This error means that the number of rows you are trying to use does not fit the amount of numbers you want to use in the matrix. If you want **n** rows, make sure the length of your matrix is divisible by **n**.
  - Error in mat1 + mat2 : non-conformable arrays
    - This error occurs when you try to do mathematical operations on matrices that aren't compatible. This goes back to linear algebra where you need to have similar length between matrices to conduct operations between them.
  
- **Dataframes**
  - Similar to matrices and vectors, you can encounter issues with indexing. Once again, make sure you keep you indexing within the limits of your dataframe.
  - Error in data.frame(c(1, 2, 3), c("a", "b")) : 
  arguments imply differing number of rows: 3, 2
    - This error will occur when the vectors you are trying to make into a dataframe have different lengths. To fix this, make sure your vectors are the same length.

- **Tibbles**
  - Often times, you can use functions like `filter()` or `group_by()` on tibbles and usually when you encounter errors, the error will be with how the function is executed. 
  - Error: Tibble columns must have compatible sizes.
    - This means that when you used the tibble function, the vectors you included were not the same length. To fix this, make sure all vectors are of the same length.

## Next Steps

Now that you understand what vectors, matrices, dataframes and tibbles are. Some next steps include:

- Using dplyr functions with tibbles: https://uomresearchit.github.io/r-tidyverse-intro/04-dplyr/
- Looking at R for Data Science's chapter on tibbles: https://r4ds.had.co.nz/tibbles.html
- The vector chapter in R4DS: https://r4ds.had.co.nz/vectors.html


## Questions

1. True or False, tibbles are part of base R?
  a. True
  b.  False
  
2. Which data type cannot have mathematical operations done on them?
  a. Matrices
  b. Tibbles
  c. Data frames
  d.  All of the data types above can have mathematical operations done on them
  
3. True or False, matrices be multiplied by vectors?
  a.  True
  b. False
  
4. If I have a vector called "names" and want to find the 4th element, what code should I use?
  a. names[3]
  b.  names[4]
  c. [3]names
  d. [4]names
  
5. If I have a data frame called "salaries" and want to find the entry on the 3rd row and in the 4th column, what should I use?
  a.  salaries[3,4]
  b. salaries[4,3]
  c. [3,4]salaries
  d. [4,3]salaries
  
6. True or False, `tidyverse` functions can be used on data frames?
  a.  True
  b. False
  
7. If I have a vector called "sports" with 10 elements, what would be returned if I call sports[20]?
  a. Nothing will happen
  b.  An NA will be returned
  c. An error will occur
  d. The last element of the vector will be returned.
  
8. If I have a tibble called "courses" with 5 rows and 5 columns, what would be returned if I call courses[10,10]?
  a. Nothing will happen
  b. An NA will be returned
  c.  NULL will be returned
  d. The closest entry to the index will be returned.
  
9. True or False, the "$" operator cannot be used on tibbles?
  a. True
  b.  False
  
10. If I have two identical data frames called "data_a" and "data_b", what will happen if I run `data_a - data_b`?
  a. Nothing will happen
  b. A vector filled with zeroes will be returned
  c.  A data frame filled with zeroes will be returned
  d. An error will occur
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
