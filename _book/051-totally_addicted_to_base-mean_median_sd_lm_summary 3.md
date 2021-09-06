


# mean, median, sd, lm, and summary

*Written by Mariam Walaa.*


## Introduction

In this lesson, you will learn how to:

- Use `mean()`, `median()`, and `sd()` to compute summary statistics 
- Use `summary()` to compute summary statistics for numeric variables in a data frame
- Use `lm()` to build linear regression models

Prerequisite skills include:

- Installing packages
- Loading packages
- Importing data

Highlights:

- 1-dimensional data can be summarized with `mean()`, `median()`, `sd()`
- n-dimensional data can be summarized with `summary()`
- `lm()` can be used to build linear regression models

## Arguments

### `mean()`

The `mean()` function takes the following as arguments:

| Argument | Parameter | Details                                                 |
|----------|-----------|---------------------------------------------------------|
| x        | column    | this is the set of values to compute the average of     |
| na.rm    | Boolean   | this is to indicate whether NA values should be ignored |

You can read more about the arguments in the `mean()` function's documentation
[here](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/mean).

### `median()`

The `median()` function takes the following as arguments:

| Argument | Parameter | Details                                                 |
|----------|-----------|---------------------------------------------------------|
| x        | column    | this is the set of values to compute the median of      |
| na.rm    | Boolean   | this is to indicate whether NA values should be ignored |

You can read more about the arguments in the `median()` function's documentation
[here](https://www.rdocumentation.org/packages/stats/versions/3.6.2/topics/median).

### `sd()`

The `sd()` function takes the following as arguments:

| Argument | Parameter | Details                                                           |
|----------|-----------|-------------------------------------------------------------------|
| x        | column    | this is the set of values to compute the standard deviation of    |
| na.rm    | Boolean   | this is to indicate whether NA values should be ignored           |

You can read more about the arguments in the `sd()` function's documentation
[here](https://www.rdocumentation.org/packages/stats/versions/3.6.2/topics/sd).

### `summary()`

The `summary()` function takes the following as arguments:

| Argument | Parameter | Details                                                |
|----------|-----------|--------------------------------------------------------|
| object   | data      | this is the data to summarize (typically a data frame) |

You can read more about the arguments in the `summary()` function's documentation
[here](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/summary).

### `lm()`

The `lm()` function takes the following as arguments:

| Argument | Parameter       | Details                                                       |
|----------|-----------------|---------------------------------------------------------------|
| formula  | Y ~ X1 + … + Xn | equation of linear regression model                           |
| data     | data frame      | data frame containing variables for the model                 |
| subset   | condition       | condition to filter data frame by prior to building the model |

You can read more about the arguments in the `lm()` function's documentation
[here](https://www.rdocumentation.org/packages/stats/versions/3.6.2/topics/lm).

## Overview

This section will demonstrate how to use the `lm()` function to build simple and multiple
linear regression models. We will be looking at a subset of the Broadway Grosses data set
provided by Alex Cookson in [the dataset
repository](https://github.com/tacookson/data/tree/master/broadway-grosses)provided on
GitHub. The Broadway Grosses data set comprises data on revenue and attendance figures for
theaters that are part of The Broadway League.


```r
glimpse(broadway)
#> Rows: 47,524
#> Columns: 14
#> $ week_ending          <date> 1985-06-09, 1985-06-09, 1985…
#> $ week_number          <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
#> $ weekly_gross_overall <dbl> 3915937, 3915937, 3915937, 39…
#> $ show                 <chr> "42nd Street", "A Chorus Line…
#> $ theatre              <chr> "St. James Theatre", "Sam S. …
#> $ weekly_gross         <dbl> 282368, 222584, 249272, 95688…
#> $ potential_gross      <dbl> NA, NA, NA, NA, NA, NA, NA, N…
#> $ avg_ticket_price     <dbl> 30.42, 27.25, 33.75, 20.87, 2…
#> $ top_ticket_price     <dbl> NA, NA, NA, NA, NA, NA, NA, N…
#> $ seats_sold           <dbl> 9281, 8167, 7386, 4586, 2938,…
#> $ seats_in_theatre     <dbl> 1655, 1472, 1088, 682, 684, 1…
#> $ pct_capacity         <dbl> 0.7010, 0.6935, 0.8486, 0.840…
#> $ performances         <dbl> 8, 8, 8, 8, 8, 8, 8, 8, 8, 8,…
#> $ previews             <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
```

### summary()

We can print a summary of the variables in this data using the `summary()` function as
follows.


```r
summary(broadway)
#>   week_ending          week_number    weekly_gross_overall
#>  Min.   :1985-06-09   Min.   : 1.00   Min.   : 2474396    
#>  1st Qu.:1996-10-20   1st Qu.:14.00   1st Qu.: 9093031    
#>  Median :2005-01-02   Median :28.00   Median :15060671    
#>  Mean   :2004-05-22   Mean   :27.37   Mean   :16693026    
#>  3rd Qu.:2012-09-30   3rd Qu.:41.00   3rd Qu.:22897588    
#>  Max.   :2020-03-01   Max.   :53.00   Max.   :57807272    
#>                                                           
#>      show             theatre           weekly_gross    
#>  Length:47524       Length:47524       Min.   :      0  
#>  Class :character   Class :character   1st Qu.: 262229  
#>  Mode  :character   Mode  :character   Median : 470064  
#>                                        Mean   : 574487  
#>                                        3rd Qu.: 758438  
#>                                        Max.   :4041493  
#>                                                         
#>  potential_gross   avg_ticket_price top_ticket_price
#>  Min.   :   7754   Min.   :  0.00   Min.   :  4.0   
#>  1st Qu.: 629523   1st Qu.: 43.37   1st Qu.: 85.0   
#>  Median : 903150   Median : 60.23   Median :200.0   
#>  Mean   : 939598   Mean   : 67.91   Mean   :189.7   
#>  3rd Qu.:1190502   3rd Qu.: 84.65   3rd Qu.:250.0   
#>  Max.   :3559306   Max.   :511.58   Max.   :998.0   
#>  NA's   :12613                      NA's   :11357   
#>    seats_sold    seats_in_theatre  pct_capacity   
#>  Min.   :    0   Min.   :   0     Min.   :0.0000  
#>  1st Qu.: 5442   1st Qu.:1021     1st Qu.:0.6914  
#>  Median : 7736   Median :1181     Median :0.8330  
#>  Mean   : 7893   Mean   :1238     Mean   :0.8028  
#>  3rd Qu.:10187   3rd Qu.:1509     3rd Qu.:0.9538  
#>  Max.   :24305   Max.   :1969     Max.   :1.5536  
#>                                                   
#>   performances       previews      
#>  Min.   : 0.000   Min.   : 0.0000  
#>  1st Qu.: 8.000   1st Qu.: 0.0000  
#>  Median : 8.000   Median : 0.0000  
#>  Mean   : 7.238   Mean   : 0.5837  
#>  3rd Qu.: 8.000   3rd Qu.: 0.0000  
#>  Max.   :17.000   Max.   :16.0000  
#> 
```

You'll notice the following about the output provided by `summary()`:

* The only column of type `character` does not have a numeric summary. Instead, the length
and class of the column is provided.
* The remaining columns are of type `integer` and `double`, and all have a numeric
summary. The numeric summary provides:
  * Minimum, 1st Quantile, Median, Mean, 3rd Quantile, Maximum

### mean(), median(), and sd()

We can also compute the mean, median, and standard deviation for 1-dimensional data, such
as any numeric variable in the data set.


```r
mean(broadway$avg_ticket_price)
#> [1] 67.91474
```


```r
median(broadway$avg_ticket_price)
#> [1] 60.235
```


```r
sd(broadway$avg_ticket_price)
#> [1] 38.58942
```

Be careful with the type of values an object contains when you pass it to these functions.
If the values include NAs, you will need to add `na.rm = TRUE`. If the values aren't
numeric, you will need to convert them to numeric. You can take a look at the Data Types
tutorial for more information on how to do this.

### lm()

If we want to predict the number of seats sold in a week, there are several variables
in the data set that may be helpful for making this prediction, such as the average ticket
price, the number of performances taking place that week, and the theater's seat capacity.
We can build a _multiple_ linear regression to make this prediction with this data.

Before we build the regression model, let's take note of the components that this model
will need to consist of:

  1. The dependent variable that we want to predict (Highlighted in blue)
  2. The independent variables that we want to make predictions with (Highlighted in pink)
  3. The data frame that contains all of these variables (Highlighted in orange)



<pre><code class='language-r'><code>multiple_regression <- lm(formula = <span style='color:cornflowerblue'>seats_sold</span> ~<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style='color:deeppink'>avg_ticket_price + performances + seats_in_theatre</span>,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;data = <span style='color:orange'>broadway</span>)</code></code></pre>

To view the results from this model, we can use the `summary()` function as follows:


```r
summary(multiple_regression)
#> 
#> Call:
#> lm(formula = seats_sold ~ avg_ticket_price + performances + seats_in_theatre, 
#>     data = broadway)
#> 
#> Residuals:
#>      Min       1Q   Median       3Q      Max 
#> -11449.0   -962.5    214.0   1162.6  13054.3 
#> 
#> Coefficients:
#>                    Estimate Std. Error t value Pr(>|t|)    
#> (Intercept)      -2.849e+03  3.597e+01  -79.20   <2e-16 ***
#> avg_ticket_price  1.655e+01  2.040e-01   81.11   <2e-16 ***
#> performances      1.637e+02  3.556e+00   46.05   <2e-16 ***
#> seats_in_theatre  6.813e+00  2.222e-02  306.66   <2e-16 ***
#> ---
#> Signif. codes:  
#> 0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
#> 
#> Residual standard error: 1697 on 47520 degrees of freedom
#> Multiple R-squared:  0.7164,	Adjusted R-squared:  0.7164 
#> F-statistic: 4.002e+04 on 3 and 47520 DF,  p-value: < 2.2e-16
```

We can also do a _simple_ linear regression with only one independent variable as follows:



<pre><code class='language-r'><code>simple_regression <- lm(formula = <span style='color:cornflowerblue'>seats_sold</span> ~<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style='color:deeppink'>pct_capacity</span>,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;data = <span style='color:orange'>broadway</span>)</code></code></pre>

We can view the results from the model again using `summary()`.


```r
summary(simple_regression)
#> 
#> Call:
#> lm(formula = seats_sold ~ pct_capacity, data = broadway)
#> 
#> Residuals:
#>     Min      1Q  Median      3Q     Max 
#> -9555.8 -1611.3  -178.6  1829.4 15925.8 
#> 
#> Coefficients:
#>              Estimate Std. Error t value Pr(>|t|)    
#> (Intercept)  -1228.73      52.92  -23.22   <2e-16 ***
#> pct_capacity 11363.63      64.39  176.49   <2e-16 ***
#> ---
#> Signif. codes:  
#> 0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
#> 
#> Residual standard error: 2476 on 47522 degrees of freedom
#> Multiple R-squared:  0.3959,	Adjusted R-squared:  0.3959 
#> F-statistic: 3.115e+04 on 1 and 47522 DF,  p-value: < 2.2e-16
```

### Example: Combining `mean()`, `median()`, and `lm()`

We can even use `mean()` and `median()` together with `lm()`. For example, we can make
predictions for the mean and median value of an independent variable.




<pre><code class='language-r'><code>predict(simple_regression,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;data.frame(pct_capacity = <span style='background-color:#ffff7f'>mean</span>(broadway$pct_capacity),<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;na.rm = TRUE))<br>#> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1 <br>#> 7893.45</code></code></pre>



<pre><code class='language-r'><code>predict(simple_regression,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;data.frame(pct_capacity = <span style='background-color:#ffff7f'>median</span>(broadway$pct_capacity),<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;na.rm = TRUE))<br>#> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1 <br>#> 8237.17</code></code></pre>

Notice that this code uses the `predict()` function which is not covered in this tutorial,
but you can learn more about it in the documentation provided
[here](https://www.rdocumentation.org/packages/raster/versions/3.4-5/topics/predict).

## Exercises

This section will ask you to complete exercises based on what you've learned from the
previous section.

### Exercise 1

We want to predict the number of seats sold `seats_sold` based on the number of
performances `performances`. Fill in the blanks for the code below to create a simple
linear regression model.



<pre><code class='language-r'><code><span style='background-color:#ffff7f'> &nbsp;</span>(formula = <span style='background-color:#ffff7f'> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span> <span style='background-color:#ffff7f'> </span> <span style='background-color:#ffff7f'> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>,<br>&nbsp;&nbsp;&nbsp;data = <span style='background-color:#ffff7f'> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>)</code></code></pre>

You'll notice that there are 5 blanks in total that you'll need to fill.

<!-- ```{r summary-fill-in-blanks, echo = FALSE} -->
<!-- quiz(question("What should the first blank be?", -->
<!--               answer("summary"), -->
<!--               answer("predict"), -->
<!--               answer("lm", correct = TRUE), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("What should the second blank be?", -->
<!--               answer("pct_capacity"), -->
<!--               answer("seats_sold", correct = TRUE), -->
<!--               answer("formula"), -->
<!--               answer("performances"),  -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("What should the third blank be?", -->
<!--               answer("~", correct = TRUE), -->
<!--               answer(" = "), -->
<!--               answer("\\-"), -->
<!--               answer("+"), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("What should the fourth blank be?", -->
<!--               answer("pct_capacity"), -->
<!--               answer("seats_sold"), -->
<!--               answer("formula"), -->
<!--               answer("performances", correct = TRUE), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE), -->
<!--      question("What should the fifth blank be?", -->
<!--               answer("df"), -->
<!--               answer("data"), -->
<!--               answer("broadway", correct = TRUE), -->
<!--               random_answer_order = TRUE, -->
<!--               allow_retry = TRUE)) -->
<!-- ``` -->


### Exercise 2

If we want to create a simple linear regression model for a _subset_ of the
data, we will need to add another argument to `lm()` to let it know which subset we want.
For example, we may want to create a regression for observations that have less than 12
performances.

Use the code from above in addition to the `subset` parameter to do this.


<!-- ```{r summary-statistics-exercise-2, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r summary-statistics-exercise-2-solution, exercise = FALSE} -->
<!-- lm(formula = seats_sold ~ performances, -->
<!--    data = broadway, -->
<!--    subset = performances < 12) -->
<!-- ``` -->


<!-- ```{r summary-statistics-exercise-2-code-check} -->
<!-- ??grade_code() -->
<!-- ``` -->


### Exercise 3



<!-- ```{r summary-statistics-true-statements, echo = FALSE} -->
<!-- question("Which of these are true? Check all true statements.", -->
<!--          answer(paste("It is possible to create a model for only a subset of the ", -->
<!--          "observations using lm()."), correct = TRUE), -->
<!--          answer(paste("It is possible to include multiple independent variables ", -->
<!--           "in the formula within lm()."), correct = TRUE), -->
<!--          answer("mean(), median(), and sd() exclude NAs from the calculation by default.", -->
<!--                 message = paste("mean(), median(), and sd() do not exclude NAs from ", -->
<!--                                 "the calculation by default. You need to let R know ", -->
<!--                                 "that you may have NA values in your data.")), -->
<!--          answer("summary() does not provide any summary for non-numeric variables.", -->
<!--                 message = paste("summary() provides a non-numeric summary for non-numeric ", -->
<!--                                 "variables, which includes the variable class and length.")), -->
<!--          allow_retry = TRUE, -->
<!--          random_answer_order = TRUE) -->
<!-- ``` -->

## Common mistakes & errors

Here are some common mistakes and errors you may come across:

- You try to create a formula within the `lm()` function without using the appropriate
operators (i.e., `~` to separate the dependent variable from the independent variable(s),
or `+` to separate the independent variables)
- You might be specifying the dependent variable in place of the independent variables, and vice versa. Be sure to follow the `Y ~ X1 + X2 + ... + Xn` formatting.

## Next steps

If you would like to read more about these functions, here are some additional resources
you may find helpful:

- [R for Data Science - Chapter 24: Model
building](https://r4ds.had.co.nz/model-building.html).

