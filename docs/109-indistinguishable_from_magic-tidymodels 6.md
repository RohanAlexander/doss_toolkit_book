


# tidymodels


*Written by Yena Joo and last updated on January 2022.*

## Introduction
Tidyverse has become an essential package for analyzing data when using a consistent interface. 
`tidymodels` is a package created to provide a consistent interface when creating a data model that inherits the principles of `tidyverse`.  

After all the chapters learning the tidyverse framework and if you feel like you are familiar with the basics, we can start building various statistical models to incorporate to your analyses.

You'll learn key concepts such as defining model objects and creating modeling workflows.
 
In this lesson, you will learn about:  
- create robust models   
- perform statistical analysis  
- compare models   
- custom modeling  
- create statistical models   



Install Tidymodels with: 
```
install.packages("tidymodels")
```

Note that the package loads some core `tidyverse` packages, including `dplyr`, `tidyr`, and `ggplot2`.   


```r
library(tidymodels)
#> Registered S3 method overwritten by 'tune':
#>   method                   from   
#>   required_pkgs.model_spec parsnip
#> ── Attaching packages ────────────────── tidymodels 0.1.4 ──
#> ✓ broom        0.7.10     ✓ recipes      0.1.17
#> ✓ dials        0.0.10     ✓ rsample      0.1.1 
#> ✓ dplyr        1.0.7      ✓ tibble       3.1.6 
#> ✓ ggplot2      3.3.5      ✓ tidyr        1.2.0 
#> ✓ infer        1.0.0      ✓ tune         0.1.6 
#> ✓ modeldata    0.1.1      ✓ workflows    0.2.4 
#> ✓ parsnip      0.1.7      ✓ workflowsets 0.1.0 
#> ✓ purrr        0.3.4      ✓ yardstick    0.0.9
#> ── Conflicts ───────────────────── tidymodels_conflicts() ──
#> x purrr::discard() masks scales::discard()
#> x dplyr::filter()  masks stats::filter()
#> x dplyr::lag()     masks stats::lag()
#> x recipes::step()  masks stats::step()
#> • Use suppressPackageStartupMessages() to eliminate package startup messages
```
You can see the list of the packages included in the tidymodels package above.  

In this lesson, we will focus on the core packages in `tidymodels`, including:   
- `rsample`  
- `recipes`  
- `parsnip`  
- `yardstick`  


### Prerequisite skills include   
-  `tidyverse`  
-  Basic modeling  
-  Machine Learning knowledge 

### Data preparation (Data resampling): `rsample`
Every statistical analysis and modeling start with data. 
`rsample` is a General Resampling Infrastructure for R. The package comes in handy when you want to separate a data set into training dataset and testing dataset. 

#### Resampling Methods  

**Simple Training**
"The initial_split() function is specially built to separate the data set into a training and testing set"  
By using the `prop` argument, you can set the proportion of the data that is for testing and training.  

```r
mtcars_split <- initial_split(mtcars, prop = 0.7)
mtcars_split
#> <Analysis/Assess/Total>
#> <22/10/32>
training_df <- training(mtcars_split)
testing_df <- testing(mtcars_split)
```
The function executes the row count for analysis, assess, and total.  
You can use the function `training()` to access the training data, and `testing()` to access the testing data.   


```r
mtcars_split %>% 
training() %>% 
  glimpse()
#> Rows: 22
#> Columns: 11
#> $ mpg  <dbl> 30.4, 22.8, 17.3, 18.1, 16.4, 15.2, 17.8, 15.…
#> $ cyl  <dbl> 4, 4, 8, 6, 8, 8, 6, 8, 8, 8, 6, 6, 8, 6, 4, …
#> $ disp <dbl> 75.7, 108.0, 275.8, 225.0, 275.8, 275.8, 167.…
#> $ hp   <dbl> 52, 93, 180, 105, 180, 180, 123, 150, 150, 17…
#> $ drat <dbl> 4.93, 3.85, 3.07, 2.76, 3.07, 3.07, 3.92, 2.7…
#> $ wt   <dbl> 1.615, 2.320, 3.730, 3.460, 4.070, 3.780, 3.4…
#> $ qsec <dbl> 18.52, 18.61, 17.60, 20.22, 17.40, 18.00, 18.…
#> $ vs   <dbl> 1, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 1, …
#> $ am   <dbl> 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, …
#> $ gear <dbl> 4, 4, 3, 3, 3, 3, 4, 3, 3, 3, 4, 5, 5, 4, 4, …
#> $ carb <dbl> 2, 1, 3, 1, 3, 3, 4, 2, 2, 2, 4, 6, 4, 4, 1, …
```


**Bootstrap Sampling**
Bootstrap sampling can be easily conducted by using the function `bootstraps()`. Bootstrap is sampling with replacement to estimate the variability in a statistic of interest to assess the accuracy of an estimate from resampling from a larger population. 

```r
bootstraps(
  mtcars,
  times = 25
)
#> # Bootstrap sampling 
#> # A tibble: 25 × 2
#>    splits          id         
#>    <list>          <chr>      
#>  1 <split [32/12]> Bootstrap01
#>  2 <split [32/13]> Bootstrap02
#>  3 <split [32/11]> Bootstrap03
#>  4 <split [32/9]>  Bootstrap04
#>  5 <split [32/13]> Bootstrap05
#>  6 <split [32/13]> Bootstrap06
#>  7 <split [32/10]> Bootstrap07
#>  8 <split [32/13]> Bootstrap08
#>  9 <split [32/14]> Bootstrap09
#> 10 <split [32/11]> Bootstrap10
#> # … with 15 more rows
```

The package also provides different types of cross-validation functions as well as various resampling methods you can use. All the functions can be easily found [here](https://rsample.tidymodels.org/reference/index.html)

https://cloud.r-project.org/web/packages/rsample/rsample.pdf
https://rsample.tidymodels.org

### Preprocessing (Feature engineering): `recipes` 
The `recipes` package contains a data preprocessor, which means it is designed to help you preprocess your data before training your model.  
It is divided into a series of steps, such as:   
- creating dummy variables   
- model transformation   
- extract key information from raw data, and etc.     

This is the order of how the package is organized:  

As the name of the package is 'recipes', it creates and provides you a recipe to process the data sets, so you can 'prep' the set and 'bake' it according to the recipe. 
  
"
In recipe(), the function defines the formula of the preprocessing of transformation. This process is similar to the `ggplot()` function.  
In prep(), the function calculates statistics from the training data.    
In bake(), the function applies the preprocessing to data sets. 
"

Here is an example: 

Using the same mtcars training dataset, you can create a recipe and prep it.  
```
mtcars_recipe <- training_df %>% 
  recipe(Of your choice) %>%
  Transformation of your choice %>% 
  prep()
```

Then,using the function `bake()`, you can execute the preprocessing using the testing data, as we did for the training data as the following.  

```
mtcars_recipe %>% bake(testing(mtcars_split))
```

Once you applied the trained data recipe, you can use the function `juice()` to extract the finalized training set.  
```
mtcars_training <- juice(mtcars_recipe)
```

For more information on `recipes`, here is an [additional resource on recipes package](https://recipes.tidymodels.org) you may find helpful.   



### Model Fitting, Model training: `parsnip`  
The `parsnip` package provides functions and methods that you can train models and solve problem related to model fitting.
 
Parsnip allows you to:  
- provides functions and methods for modeling (fitting the model, predictions, etc)
- framework for model parameter tuning  
- Evaluating model  

The package provides different model types such as random forests `rand_forest`, logistic regression `logistic_reg`, linear regression `linear_reg`, etc. You can also customize on how you're going to use the model using the parameters of the functions.   

There are two big modes of the model, classification and regression. To briefly explain, classification predicts discrete class labels, whereas regression predicts a continuous quantity output.  

For example, if you want to use the function `rand_forest`, 

```
mtcars_fit <- rand_forest(trees = int, mode = "classification" or "regression") %>% 
set_engine("randomForest") %>% 
fit(variable of your choice ~., data = mtcars_training)
```
Note that you can use `rand_forest` and `decision_tree` if you choose "classification" mode.  

The `set_engine()` function allows you to use packages such as `ranger`, `randomForest`, etc.  

You can then apply the model to the testing dataset by using the the `predict()` function:  
```
mtcars_prediction <- predict(mtcars_fit, mtcars_testing)
```

and there are interfaces that allow you to fit a model: 
- fit() for formula interface
- fit_xy() for non-formula interface  


For more information on `parsnip`, here is an [additional resource on parsnips package](https://parsnip.tidymodels.org) you may find helpful.   

https://www.tidymodels.org
https://www.tidyverse.org/blog/2018/11/parsnip-0-0-1/


### Model Evaluation: `yardstick` 
The `yardstick` package allows you to estimate how well models are performing using tidy data principles. For regression models, we can use R-squared or MSE to evaluate the model performnce, however classifier evaluation requires a little more than that.  

Using the package, you can create custom metrics to evaluate your model.  

```
mtcars_prediction %>% 
bind_cols(mtcars_testing) %>% 
metrics(truth = Variable name, estimate = .pred_class)
```
https://yardstick.tidymodels.org
https://cran.r-project.org/web/packages/yardstick/readme/README.html
## Exercises

### Question 1
What core packages are included in the `tidymodels` package?   
  a. parsnip  
  b. recipes  
  c. yardstick  
  d. all of the above  
  
### Question 2  
Which of the statements is tidymodels package appropriately used?   
  a. When I want to import excel file to R and edit the table.   
  b. When I want to create a histogram using the data and label it.   
  c. When I want to do statistical analysis with great flexibility and with multiple stages.   
  d. When I want to create a pdf file and write correct references.   
  
### Question 3
(True or False) The `tidymodels` package includes some core packages from the `tidyverse`.  
  a. True  
  b. False  

### Question 4
What argument in initial_split() should you use to set the proportionfor testing and training?   
  a. num  
  b. prop  
  c. base   
  d. rat  

### Question 5

What functions are in the `recipe` package (Select all that apply)?  
  a. bake()   
  b. milk()   
  c. recipe()  
  d. juice()  

### Question 6
What are the two common modes of the `parsnip` models?  
  a. vectors  
  b. classification  
  c. aversion  
  d. regression  


### Question 7
(True or False) For the models with classification mode, you can evaluate the model performance using R-squared.   
  a. True  
  b. False  

### Question 8
Select one example of the most appropriate usage of the `tidymodels` package.  
  a. Import data with readr, use tidyr to clean data, and plot the graph using ggplot2.  
  b. connect R with SQL, import data and use kable() function to create a neat table.   
  c. resample imported data using rsample, preprocess data with recipes, fit the model using parsnip, and evaluate the model with yardstick.   
  d. None of the above.   
  
  
### Question 9
What does the following function do?  
```
set_engine(object, engine, ...)
```
  a. It is used to specify which package will be used to fit the model.   
  b. It is used to preprocess a dataset.   
  c. It is used to bootstrap sampling.   
  d. None of the above.    
  
### Question 10
Which statement is correct about tidymodels (select all that apply)?   
  a. You can build a model.  
  b. You can preprocess your data.  
  c. You can tune model parameters.  
  d. You can evaluate your model. 

## Common Mistakes & Errors 
https://rviews.rstudio.com/2019/06/19/a-gentle-intro-to-tidymodels/
