


# apply, sapply, and lapply

*Written by Ananya Jha and last updated on 7 October 2021.*

## Introduction

The apply family of functions is one of the most commonly used classes and is used to manipulate data (in the form of matrices, arrays, dataframes, lists, etc.) repetitively. They are generally used to run a function on multiple chunks of data of an object.

If you have programmed before, the functionality of apply functions can be thought of as a 'for loop' but they are considered more efficient. \
In this lesson we will be covering apply, lapply and sapply. There is a huge variety of apply functions available, and while they work for different kinds of data, all of these have at least two common arguments- an object and a function (which can be either user-defined or built in) and we can "apply" the latter to the former. We will get into the details of the arguments and how to use them later. 


In this lesson, you will learn how to:

- Use apply, lapply and sapply (functions from the apply family)

- Use appropriate versions of the apply family of functions for the correct use cases


Prerequisites:

- Basic understanding of lists, vectors, arrays, matrices, and data frames
prerequisites


### Arguments

Let's first take a look at what the R documentation has as the arguments for these functions:

 - apply(X, MARGIN, FUN, ..., simplify = TRUE)

 - lapply(X, FUN, ...)
 
 - sapply(X, FUN, ..., simplify = TRUE, USE.NAMES = TRUE)

Where:



| Argument      | Details                                                                                         |
|---------------|-------------------------------------------------------------------------------------------------|
| X             | The object to which we want to apply the function (can be array/matrix/list/vector/data frame)  |
| MARGIN        | A vector to specify how the function is applied (1 for along row/2 for column)                   |
| FUN           | The function (in-built or user defined) to be applied repeatedly to the elements of X            |
| ...           | Optional arguments to FUN                                                                       |
| simplify      | Logical to pick simplified results (a matrix or vector when possible)                           |
| USE.NAMES     | Logical; set to TRUE X is character and want X as names for the result                          |





At first look these functions might all seem the same.




<img src="images/049-apply_sapply_lapply1.jpeg" width="50%" style="display: block; margin: auto;" />



Now let's dive deeper into their differences to understand better.

## Apply
Let's start with apply which is the most basic from the apply family of functions. It operates primarily on arrays and matrices, and can occasionally work with data frames but with restrictions (the data frame object type must be compatible as function arguments).  

This is the only function (out of the ones covered in this lesson) that requires margins to be specified in the arguments. For example in the case of a matrix, 1 would mean the function would be applied along the rows, 2 would be columns, and c(1,2) would be both rows and columns. 

## Lapply
This is another member of the apply family of functions that operates on list, data frames, vectors. It has two main differences compared to apply-  

1) It always returns a list the same length as the input list

2) It does not require margin specification as it only applies the function to columns


## Sapply
The final apply function covered in this lesson is sapply. 

Just like lapply, sapply also operates on lists, data frames and vectors and does not need margin specification and just like in apply, we can use simplify = TRUE to simplify the results. 

Sapply is commonly known as "a user-friendly version of lapply". In layman's terms, sapply is a wrapper of lapply and the only difference is that it simplifies the output (when possible) and returns a vector instead of a list. 

**Note-** sapply(x, f, simplify = FALSE, USE.NAMES = FALSE) would be the same as lapply(x, f)

## Summary of differences table
To summarize the differences between these functions, we can use this table:
\


| Function | Operates on                 | Returns                             | Margins to specify(yes/no) |
|----------|-----------------------------|-------------------------------------|----------------------------|
| Apply    | arrays and matrices         | a vector or array or list of values | Yes                        |
| Lapply   | lists, data frames, vectors | a list                              | No                         |
| Sapply   | lists, data frames, vectors | a vector                            | No                         |


### Examples

#### Example 1
We will first work with the popular mtcars data set to understand how these functions work. Let's take a quick look at it 

```r
data <- mtcars
head(mtcars)
#>                    mpg cyl disp  hp drat    wt  qsec vs am
#> Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1
#> Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1
#> Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1
#> Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0
#> Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0
#> Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0
#>                   gear carb
#> Mazda RX4            4    4
#> Mazda RX4 Wag        4    4
#> Datsun 710           4    1
#> Hornet 4 Drive       3    1
#> Hornet Sportabout    3    2
#> Valiant              3    1
```
Let's subset this dataset to fit our needs better and call it cars. 

We can now find the means of all columns:

```r
apply(cars, 2, mean)
#>        hp        wt 
#> 146.68750   3.21725
```

We can also find the column quantiles using the quantile function


```r
apply(cars, 2, quantile, probs = c(0.10, 0.25, 0.50, 0.75, 0.90))
#>        hp      wt
#> 10%  66.0 1.95550
#> 25%  96.5 2.58125
#> 50% 123.0 3.32500
#> 75% 180.0 3.61000
#> 90% 243.5 4.04750
```

While it is not too relevant in this context, we can also compute the sum of rows like this:

```r
apply(cars, 1, sum)
#>           Mazda RX4       Mazda RX4 Wag          Datsun 710 
#>             112.620             112.875              95.320 
#>      Hornet 4 Drive   Hornet Sportabout             Valiant 
#>             113.215             178.440             108.460 
#>          Duster 360           Merc 240D            Merc 230 
#>             248.570              65.190              98.150 
#>            Merc 280           Merc 280C          Merc 450SE 
#>             126.440             126.440             184.070 
#>          Merc 450SL         Merc 450SLC  Cadillac Fleetwood 
#>             183.730             183.780             210.250 
#> Lincoln Continental   Chrysler Imperial            Fiat 128 
#>             220.424             235.345              68.200 
#>         Honda Civic      Toyota Corolla       Toyota Corona 
#>              53.615              66.835              99.465 
#>    Dodge Challenger         AMC Javelin          Camaro Z28 
#>             153.520             153.435             248.840 
#>    Pontiac Firebird           Fiat X1-9       Porsche 914-2 
#>             178.845              67.935              93.140 
#>        Lotus Europa      Ford Pantera L        Ferrari Dino 
#>             114.513             267.170             177.770 
#>       Maserati Bora          Volvo 142E 
#>             338.570             111.780
```

#### Example 2

As mentioned before, we can also use a user-defined function with apply. Let's first generate a random matrix.

```r
mat <- matrix(rep(seq(5), 4), ncol = 5)
```

We can use either a user defined function inside the apply function. Here, we sum along the rows and add 5 to each element:

```r
apply(mat, 1, function(x) sum(x) + 5)
#> [1] 20 20 20 20
```
Or we can use the user-defined function as an argument:

```r
func <- function(x){
  return (sum(x)+5)
}
apply(mat, 1, func)
#> [1] 20 20 20 20
```



#### Example 3
We can create a random list to test out the lapply and sapply functions.

```r

list_i <- list(i1 = 1:10, 
             i2 = rnorm(20), 
             i3 = rnorm(20, 1), 
             i4 = rnorm(100, 5))
list_i
#> $i1
#>  [1]  1  2  3  4  5  6  7  8  9 10
#> 
#> $i2
#>  [1]  0.15381364 -0.69693999  0.72041208  0.37261014
#>  [5]  0.05606283  0.96654386  0.13606536 -0.45568911
#>  [9]  1.20564088 -0.27711595 -0.64800165  0.66083435
#> [13] -1.71617753  0.57116836 -1.06550130  0.08860368
#> [17] -0.39218502 -0.64355218 -0.28212755 -1.23736399
#> 
#> $i3
#>  [1] -0.97638196  1.79164724  0.55506796  1.18614855
#>  [5]  1.73633491  0.05457173 -0.82041090  2.75868949
#>  [9]  1.40936118  0.20280778  0.91560770  0.04698224
#> [13]  0.46942992 -0.20874767  2.05155483  0.15118871
#> [17]  0.60344266  3.13423697  1.12784392  1.09831603
#> 
#> $i4
#>   [1] 4.828035 4.948769 5.417792 5.224515 3.379236 5.737661
#>   [7] 4.332593 5.924854 4.997431 5.323091 4.932802 3.938601
#>  [13] 5.544445 5.054802 4.440426 2.815160 5.329697 3.601186
#>  [19] 5.593037 5.198026 4.530852 6.513729 5.104839 5.032969
#>  [25] 6.416401 3.768042 3.974242 4.868119 4.274661 4.222627
#>  [31] 3.426240 4.813757 4.281125 5.450987 6.429025 3.118096
#>  [37] 3.878951 5.359202 4.292966 7.292357 4.113761 4.695622
#>  [43] 4.448941 5.096859 5.554649 4.014806 4.453720 5.401951
#>  [49] 4.554049 5.997388 4.473217 3.179252 5.294293 5.939532
#>  [55] 3.353501 5.157278 4.421409 4.231790 5.569080 5.790731
#>  [61] 3.937831 6.147968 4.456011 5.598575 4.321729 4.038193
#>  [67] 3.278764 4.197260 5.036000 2.807386 6.049809 4.557337
#>  [73] 6.049850 5.341004 5.514933 6.093618 5.288561 5.787614
#>  [79] 4.325788 5.184406 4.245662 3.581264 5.419015 5.017495
#>  [85] 3.174199 4.577404 5.666197 3.769284 5.979460 4.656197
#>  [91] 4.444289 6.328714 6.289508 4.835657 4.906574 4.699113
#>  [97] 7.003265 4.801568 8.345750 3.995385

lapply(list_i, mean)
#> $i1
#> [1] 5.5
#> 
#> $i2
#> [1] -0.124145
#> 
#> $i3
#> [1] 0.8643846
#> 
#> $i4
#> [1] 4.891018
sapply(list_i, mean)
#>         i1         i2         i3         i4 
#>  5.5000000 -0.1241450  0.8643846  4.8910181
```
As you can see, lapply returns a more complicated vector output and sapply returns the same output in a list.


## Exercises 

### Question 1

<!-- ```{r letter-a, echo=FALSE}  -->
question("What is the output of the lapply function?",
  answer("a list", correct = TRUE),
  answer("an array"),
  answer("a vector")
)


### Question 2

**2a)** Use the numerical columns(columns 1-4) of the `iris` dataset to compute the minimum value of each column using apply, lapply and sapply and store the outputs.


```r
head(iris)
#>   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
#> 1          5.1         3.5          1.4         0.2  setosa
#> 2          4.9         3.0          1.4         0.2  setosa
#> 3          4.7         3.2          1.3         0.2  setosa
#> 4          4.6         3.1          1.5         0.2  setosa
#> 5          5.0         3.6          1.4         0.2  setosa
#> 6          5.4         3.9          1.7         0.4  setosa
```


```r
ap <- apply(iris[,-5], MARGIN = 2,  FUN = min) 
l_ap <- lapply(iris[,-5], FUN = min) 
s_ap <- sapply(iris[,-5], FUN = min)
```

**2b)** Add the three outputs from above to a list called "list_output".



```r
list_output <- list(ap, l_ap, s_ap )
```
 
**2c)** Use an appropriate apply function to find the type of each element of list_output (using the type of function) 



```r
sapply(FUN = typeof, X = list_output) 
#> [1] "double" "list"   "double"
```


## Some extra notes

1) If you are deciding between using for loops or apply functions, always pick apply functions as they are slightly faster and require fewer lines of code. Using apply also makes the code easier to read and understand.


<img src="images/049-apply_sapply_lapply2.jpeg" width="50%" style="display: block; margin: auto;" />

2) Apply functions are capable of a lot of cool things. We can also use the apply function to generate plots for the objects like this:
<img src="049-totally_addicted_to_base-apply_sapply_lapply_files/figure-html/figures-side-1.png" width="50%" /><img src="049-totally_addicted_to_base-apply_sapply_lapply_files/figure-html/figures-side-2.png" width="50%" /><img src="049-totally_addicted_to_base-apply_sapply_lapply_files/figure-html/figures-side-3.png" width="50%" /><img src="049-totally_addicted_to_base-apply_sapply_lapply_files/figure-html/figures-side-4.png" width="50%" />
Here, we are generating a box plot for all numerical columns of the iris data set.  
<img src="images/049-apply_sapply_lapply3.jpeg" width="50%" style="display: block; margin: auto;" />

3) Using these functions can often be tricky. If you are ever struggling to decide between these functions and want the results simplified, the easiest option would be sapply. On the off-chance that you don't want simplified results, use lapply. Generally, either of these two would be ideal.
<img src="images/049-apply_sapply_lapply4.jpeg" width="50%" style="display: block; margin: auto;" />

## Common mistakes and errors
- In the case of one dimensional data (like vectors), lapply or sapply should be used as the apply function will never work. It expects the data to have at least two dimensions and will give errors. 
- If your data happens to have NA values and you use apply function, the result would be NA regardless of the function choice. You can choose to ignore the NA values (if there are any) by using na.rm inside the apply function. 

## Next steps
- To know more about these functions, a useful resource is- https://www.analyticsvidhya.com/blog/2021/02/the-ultimate-swiss-army-knife-of-apply-family-in-r/
- You can explore other functions of the apply family like tapply, vapply, mapply
- You can also explore "apply-like" functions such as colSums, rowSums, colMeans, rowMeans, etc.

## References
- [r documentation] (https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/apply).

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
