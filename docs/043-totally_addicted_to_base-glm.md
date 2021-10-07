


# Generalized linear models with glm

*Written by Ruijia Yang and last updated on 7 October 2021.*

## Introduction

In R, we can use the `glm()` function to create Generalized Linear Models (GLM) on many data types, such as count data, probability data, proportion data, etc. The usage of `glm()` is like the function `lm()` which we used before, but also have a family input.

In this section, you will learn：

- how to use `glm()` to fit a generalized linear model with the different data types.
- how to predict the probability using the fitted model.

Prerequisite skills include: 

- Installing packages
- Loading packages
- Importing data

Highlight:

- fit a logistic regression model
- fit a Poisson regression model


## Arguments

The `glm()` function takes the following as arguments:

| Argument | Parameter       | Details                                                       |
|----------|-----------------|---------------------------------------------------------------|
| formula  | Y ~ X1 + … + Xn | equation of regression model                                  |
| data     | data frame      | data frame containing variables for the model                 |
| family   | family function | link function (error distribution) to be used in the model    |

The family arguments have Gaussian family as default - `family = "gaussian"`, which is how R refers to normal distribution. If the family is Gaussian, then a GLM is the same as a Linear Model (LM).

GLM also have non-normal errors or distribution, such as Poisson family for count data, or binomial family for binomial data.

The form of the glm function is:
`glm(formula, family = familytype(link = linkfunction), data = )`

You can read more about the arguments in the `glm()` function's documentation
[here](https://www.rdocumentation.org/packages/stats/versions/3.6.2/topics/glm).


## Example

### Generalized Linear Model on binary data

For this example, we’ll use the built-in R dataset called mtcars:


```r
#view first six rows of mtcars data frame
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

In the mtcars data set, the variable vs indicates if a car has a V-shaped engine or a straight engine.

We want to create a model that helps us predict the probability of a vehicle having a V engine or a straight engine given a weight (wt) of 2000 lbs and engine displacement (disp) of 160 cubic inches.



```r
#fit logistic regression model
model <- glm(formula = vs ~ disp + wt, data=mtcars, family=binomial)
```

We fit the above logistic regression model in which we use the variables disp and wt to predict the response variable vs (the engine type of the car: 0 = V-shaped, 1 = straight). We can now predict using `predict()` function to calculate the probability in the following code.


```r
newdata = data.frame(wt = 2, disp = 160)
#include the argument type=”response” in order to get the prediction
predict(model, newdata, type="response")
#>         1 
#> 0.3434185
```

The model predicts the probability of the vehicle having a straight engine (vs = 1) to be 0.34.

We can also make several predictions at once if we have a data frame with multiple new cars.


```r
#define new data frame of three cars
morecar = data.frame(disp=c(220,200,180),
                     wt=c(2.4,2.2,2.1))

#view data frame
morecar
#>   disp  wt
#> 1  220 2.4
#> 2  200 2.2
#> 3  180 2.1

#use model to predict value of am for all three cars
predict(model, morecar, type="response")
#>         1         2         3 
#> 0.1126874 0.1544423 0.2361081
```

From the output, we know that:

- The probability of car 1 having a straight engine (vs = 1) is 0.11.
- The probability of car 1 having a straight engine (vs = 1) is 0.15.
- The probability of car 1 having a straight engine (vs = 1) is 0.24.

Now let's see an example with an interaction term.


### Generalized Linear Model on count data

We can use generalized linear models to model count data as well. The errors in such data may be distributed non-normally and the variance usually increases with the mean values. 

As the same with binary data, we still use `glm()` to build the model, while we specify a Poisson error distribution and the log as the link function - the natural log is the default link function for the Poisson error distribution. 


```r
#loading the data
cases <-  
    structure(list(Days = c(1L, 2L, 3L, 3L, 4L, 4L, 4L, 6L, 7L, 8L, 
                            8L, 8L, 8L, 12L, 14L, 15L, 17L, 17L, 17L, 18L, 19L, 19L, 20L, 
                            23L, 23L, 23L, 24L, 24L, 25L, 26L, 27L, 28L, 29L, 34L, 36L, 36L, 
                            42L, 42L, 43L, 43L, 44L, 44L, 44L, 44L, 45L, 46L, 48L, 48L, 49L, 
                            49L, 53L, 53L, 53L, 54L, 55L, 56L, 56L, 58L, 60L, 63L, 65L, 67L, 
                            67L, 68L, 71L, 71L, 72L, 72L, 72L, 73L, 74L, 74L, 74L, 75L, 75L, 
                            80L, 81L, 81L, 81L, 81L, 88L, 88L, 90L, 93L, 93L, 94L, 95L, 95L, 
                            95L, 96L, 96L, 97L, 98L, 100L, 101L, 102L, 103L, 104L, 105L, 
                            106L, 107L, 108L, 109L, 110L, 111L, 112L, 113L, 114L, 115L), 
                   Students = c(6L, 8L, 12L, 9L, 3L, 3L, 11L, 5L, 7L, 3L, 8L, 
                                4L, 6L, 8L, 3L, 6L, 3L, 2L, 2L, 6L, 3L, 7L, 7L, 2L, 2L, 8L, 
                                3L, 6L, 5L, 7L, 6L, 4L, 4L, 3L, 3L, 5L, 3L, 3L, 3L, 5L, 3L, 
                                5L, 6L, 3L, 3L, 3L, 3L, 2L, 3L, 1L, 3L, 3L, 5L, 4L, 4L, 3L, 
                                5L, 4L, 3L, 5L, 3L, 4L, 2L, 3L, 3L, 1L, 3L, 2L, 5L, 4L, 3L, 
                                0L, 3L, 3L, 4L, 0L, 3L, 3L, 4L, 0L, 2L, 2L, 1L, 1L, 2L, 0L, 
                                2L, 1L, 1L, 0L, 0L, 1L, 1L, 2L, 2L, 1L, 1L, 1L, 1L, 0L, 0L, 
                                0L, 1L, 1L, 0L, 0L, 0L, 0L, 0L)), 
              .Names = c("Days", "Students"), 
              class = "data.frame", 
              row.names = c(NA, -109L)
              )
attach(cases)
```

Fit the model by specifying the Poisson distribution and including it in the argument. Display model results by using `summary()`.


```r
Poisson_model <- glm(formula = Students ~ Days, cases, family = poisson)

summary(Poisson_model)
#> 
#> Call:
#> glm(formula = Students ~ Days, family = poisson, data = cases)
#> 
#> Deviance Residuals: 
#>      Min        1Q    Median        3Q       Max  
#> -2.00482  -0.85719  -0.09331   0.63969   1.73696  
#> 
#> Coefficients:
#>              Estimate Std. Error z value Pr(>|z|)    
#> (Intercept)  1.990235   0.083935   23.71   <2e-16 ***
#> Days        -0.017463   0.001727  -10.11   <2e-16 ***
#> ---
#> Signif. codes:  
#> 0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
#> 
#> (Dispersion parameter for poisson family taken to be 1)
#> 
#>     Null deviance: 215.36  on 108  degrees of freedom
#> Residual deviance: 101.17  on 107  degrees of freedom
#> AIC: 393.11
#> 
#> Number of Fisher Scoring iterations: 5
```

This `summary` of a glm fit lists the following items:

- the covariates used in the model, the corresponding estimates for the regression parameters ($\hat{\beta}$), their standard errors, $z$ statistics and corresponding P values;
- the dispersion parameter used - for the standard Poisson regression model this dispersion parameter is equal to 1, as indicated in the R output;
- the null deviance; 
- the AIC calculated for this regression model.

In this model result, the negative coefficient for Days indicates that as days increase, the mean number of students with the disease is smaller - And this coefficient is highly significant (p < 2e-16).

We also see that the residual deviance is greater than the degrees of freedom, so that we have over-dispersion. This means that there is extra variance not accounted for by the model or by the error structure. So we may need to adjust our model. 

## Exercise

### Exercise 1

Let‘s use the built-in R dataset mtcars again. Now we want to predict the transmission type of the car, by using the variables `disp` and `hp`. (Note: the transmission type of the car: 0 = automatic, 1 = manual).

Please fit the model below and view the model summary:

<!--```{r ex1, exercise=TRUE, exercise.lines = 4} -->

<!-- ``` -->

<!-- ```{r ex1-solution} -->
<!-- model <- glm(am ~ disp + hp, data=mtcars, family=binomial) -->
<!-- summary(model) -->
<!-- ``` -->

### Exercise 2

Assume that there is a car A with disp = 180 and hp = 90. 

Now please predict the probability that car A has an automatic transmission (am=0) or a manual transmission (am=1) below:

<!--```{r ex2, exercise=TRUE, exercise.lines = 4} -->

<!-- ``` -->


<!-- ```{r ex2-solution} -->
<!-- #define new observation -->
<!-- newdata = data.frame(disp=180, hp= 90) -->

<!-- #use model to predict value of am -->
<!-- predict(model, newdata, type="response") -->
<!-- ``` -->


## Common mistakes and errors

1. When using `predict()` function, the names of the columns in the new data frame should exactly match the names of the columns in the data frame used to build the model.

2. Response variables can't be factor/categorical variables. If you need to do logistic regression, you should change factor/categorical variable to 0 and 1, or FALSE and TRUE, or add `family=binomial`.

3. If you have any NA values, you can either drop or impute NA values if there is numeric variable.


## Next steps

In the next step, you can learn and try Generalized Linear Mixed Model (GLMM) when you couldn't use GLM because of grouping in the data.


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
