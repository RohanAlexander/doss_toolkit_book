



# usethis

*Written by Leuven Wang and last updated on 5/2/2022.*

## Introduction

`usethis` is an R package that automates repetitive tasks during project setup, something very useful for starting data analysis projects or if you are creating your own package.

In this lesson, you will learn how to use `usethis` to:

- Create new R projects or packages.
- Setup common supplementary files and configurations for R projects and packages.
- Connect and perform simple actions with Github.

Prerequisites:

- Basic understanding of project structure.
- Basic understanding of writing R functions.
- Basic understanding of Git and Github.
- Previous knowledge from the `devtools` lesson would be useful.

The first step is to install the package onto your computer and load it within your console.


```r
install.packages("usethis")
library(usethis)
```





Since `usethis` does not handle data analyses or programming work directly, we will not be working with scripts but rather mostly in the R console.

## Creating New Packages/Projects

Firstly, lets distinguish between a package and a project. A project would be similar to the kind of assignments you're used to completing in school work - data analysis work that features code contextually applied in that one particular instance. This is not to say that such projects wouldn't benefit from the quick implementation of functions or otherwise repetitive setup tasks.
  
  
A package, on the other hand, is a bundled collection of R functions that you can repeatedly call on when completing other projects. In short, it provides reusable R code, such that you don't have to copy and paste the same functions over and over again when starting new but similar assignments. However, a package is also more than just a quick shortcut to some source code. Packages provide your bundled functions with accompanying features such as version control, documentation, dependencies, tests and examples, data, and much more. In essence, packages are a comprehensive toolkit that you can conveniently call on to aid you in your work or to distribute to others.
  
Now, lets make our own package!
  
  
First, open up RStudio and create a new package by going to File > New Project > New Directory > R Package. You should end up with a window like this:

![](newpackagewizard.JPG)

Give your package a fun name, choose a location for your directory to be situated in and click "Create Project". You will notice RStudio will now take you to a whole new project environment. Notice that the project icon in the top right will have changed from saying "Project: (None)" to the name of your project (in our example, "exppackage"). This means that you are working within the project environment.  In the "Files" tab on your right, you will see that R has already set up the basic building blocks of your new project.

![](filestab.JPG)

Doing this is synonymous as if you had typed in the R **console** (although now you would have to specify your desired folder path):

```r
usethis::create_package("exppackage")
```




Alternatively, if you are not creating a package but would rather use `usethis` to setup an ordinary data analysis project you can work from the RStudio GUI or use the command `create_project()` inside the console:


```r
usethis::create_project("expproject")
```

Notice that the structure and contents of the resulting directory are different to those of a package.



## Common Files and Configurations Setup

### Adding Package Functions
If you're working with a package, in the "R" folder you will probably find an example function that has already been built for you, "hello.R". Feel free to delete it or leave it be. We will now create our own function within the package. First, within the project environment, type into the R **console**:


```r
usethis::use_r("function_name") #use whatever you'd like to name your function in place of function_name
```

This creates a new R file titled "function_name" and opens it in RStudio.

![](newfunction.JPG)

Now, within the `function_name.R` file, you can write the contents of your function. We're going to keep it simple:


```r
linear_transform <- function(x){
  x+1
}
```

This function simply adds 1 to the numerical input `x`. Press "Ctrl+Shift+S" to save the function and load it into the source and you can now run your function. Alternatively, you can check the "Source on Save" box at the top of your code editor.
  
  
To add some meta information to your function, make sure your text selector is within the curly brackets of your bracket and press "Ctrl + Shift + Alt + R" to add a `roxygen` comment (or go to Code > Insert Roxygen Skeleton). Modify the comment with the appropriate information including a title, the parameters, and the function expected return value and possible examples. You can read more about `roxygen` [here](https://roxygen2.r-lib.org/articles/roxygen2.html).

![](roxygencomment.JPG)

To alert the system that we've updated our documentation and see what we've done, type in the **console**:

```r
devtools:: document()
devtools:: install()
?linear_transform
```

And you'll see our written description of our function in the "Help" tab on the right, just like all those other R packages that you've used before. Pretty neat, huh?

![](helptab.JPG)


### Package Licenses

If you plan on sharing your package, you probably want to include some sort of license in it as well. You can find a list of such licenses on the `usethis` website [here](https://usethis.r-lib.org/reference/licenses.html). Implementation is extremely simple. Identify the license you want, find the corresponding `usethis` code, and place it into the console. For example, with the MIT License:


```r
use_mit_license(copyright_holder = "Your Name Here")
```

You will notice immediately the appearance of licensing files in your packages' root directory. You can open them to read it.

![](licensingfiles.JPG)


You can read more about licensing at these links:
  
https://choosealicense.com/
  
https://r-pkgs.org/license.html
  
https://thinkr-open.github.io/licensing-r/rlicense.html


### Package-Level Documentation

Similar to how we created documentation on a specific function, we can also do so for the entire package using:


```r
use_package_doc()
```

This generates a dummy `R` file with `roxygen` comments for us to add documentation on our entire package. This way, we don't have to repeat essential documentation information for our package in each function documentation file. We can call this file similar to what we did with function documentation through:


```r
?exppackage #remember to call devtools:document() first after updating your documentation!
```


### Unit Testing

Testing is useful not only when initially developing your code to see if it works but also later on when your using it and you may have forgotten its capabilities or limitations. Instead of testing individual parts of your process over and over again in the console, you can rely on the tests you have previously designed to assure yourself that your code works as you intended. To begin setting up such a series of tests, type in your console:


```r
usethis::use_testthat()
```

Now go the `R` file containing the function you want to write test for and call in the console:

```r
usethis::use_test()
```

Alternatively you can also skip calling `use_testthat()` and skip right to your function file and call `use_test()`.

You will notice that R has created a new `tests` folder within the package/project directory. Within that folder you will find a sub-folder `testthat` and a new R file, `test-the_name_of_your_function_file.R`. Opening it up gives an example test written for you.


![](testexample.JPG)


You can run this test by clicking on the "Run Tests" button on the top right of your code editor and witness the test results in the "Build" pane on your right side. If you want to run individual test, you can copy and paste them into your console after running `devtools::load_all()`.

Now, lets write our own test for `linear_transform()`. The basic structure of a test is quite simple as you can tell:


```r
test_that("linear_transform() works", {
  expect_equal(linear_transform(2),3)
})
```

You can also test for errors such as here where we place a non-numerical input into our function:


```r
test_that("linear_transform() works", {
  expect_equal(linear_transform(2),3)
  expect_error(linear_transform("boogaloo"))
})

```

There are many different versions of `expect_` that allow you to test for not just successes and errors, but also failures or warning messages.

You're going to want to think about how you organize your tests. The entire `R` file can be dedicated to all the tests surrounding the functions in your code file. Each individual `test_that()` can contain all the tests for a specific function within the code file or for a specific functionality of a function within the code file (e.g. you can have one `test_that()` for testing extreme values and another `test_that()` for testing invalid inputs).

A useful function for running all the tests related to your package (i.e. every single test file in the folder) is


```r
devtools::test()
```


### Adding Dependencies

Sometimes, your package or project is going to depend on other packages or projects to work. A simple way to ensure that anyone who uses your package will automatically download all its accompanying dependencies is to call into the console:


```r
usethis::use_package("quanteda") #replace quanteda with your dependency.
```

Once we've done this, we can update our documentation with `devtools::document()`. If you then open up the `DESCRIPTION` file in your main directory, you will see that your dependencies have been listed under the "Imports" section.


### Adding Data

Sometimes, your package or project will be reliant on specific data. `use_data` allows you to easily save package data in the directory correctly. For example, we create a fake dataset "data" and save it like so:


```r
data <- data.frame(seq(1:100), rnorm(100))
use_data(data)
```

This creates a new folder within your directory titled "data" and creates an `rda` file named after your variable (in this case also named "data") and places it within the folder. You can also save other forms of data besides datasets such as integers or strings. The important thing is assigning them a variable name.


### Read Me and News

Creates `README.md` and `NEWS.md` files within the project directory.


```r
usethis::use_readme_md()

usethis::use_news_md()
```



## Working with Github.

`usethis` supports various functions for users working with GitHub. This may be useful in the event that you want to apply version control, particularly if you are planning on sharing your package with others.


To begin, log on to your Github account. Then type into your R console:


```r
usethis::create_github_token()
```

This will open up a new tab on your browser for you to create a Personal Access Token to GitHub. Give your token an appropriate name and generate it.

![](githubcreatetoken.JPG)

Then, copy it and type into your console:


```r
gitcreds::gitcreds_set()
```

You will be prompted to enter your token which you can now paste into your console and press enter.

![](tokenset.JPG)

You can verify the validity of your token and what account is associated with it using:


```r
usethis::git_sitrep()
```

![](gitsitrep.JPG)

You may notice that your Git config name and email are unset. To correct this, simply do:


```r
use_git_config(user.name = "Your Name", user.email = "theemailattachedtoyourgithubaccount@example.com")
```

Whilst your name does not have to be your GitHub username, your email MUST be the email associated with your GitHub account. Now, within the environment of your project or package, type:

```r
usethis::use_git()
```
You may be prompted for confirmation. If given, this will initialize your project/package as a local repository and make your first commit. To create a remote repository on GitHub.com and push your local branch directly on there, use

```r
usethis::use_github()
```
and Voila! Your browser should open up at a brand new repository under your GitHub account, with all the files of your project directory already uploaded on it.   



## Exercises

### Question 1

<!-- Create a new R package titled "TotallyAwesomePackage" -->
<!-- ```{r question1, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r question1-solution} -->
<!-- usethis::create_package("TotallyAwesomePackage") -->
<!-- ``` -->



<!-- ### Question 2 -->

<!-- Add a GPL v3 licensing file to your new package. -->

<!-- ```{r question2, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r question2-solution} -->
<!-- usethis::use_gpl_license(version = 3) -->
<!-- ``` -->


<!-- ### Question 3 -->

<!-- We want to add some functions to our new package. Create a new R file titled "FunFunctions". -->

<!-- ```{r question3, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r question3-solution} -->
<!-- usethis::use_r("FunFunctions") -->
<!-- ``` -->


<!-- ### Question 4 -->



<!-- ```{r question4} -->

<!-- question("You can't see the package directory here but you should have some basic idea of how it's structured. Under which sub-folder is the `FunFunctions.R` file located?",  -->
<!--          answer("data"),  -->
<!--          answer("R", correct= TRUE), -->
<!--          answer("tests"), -->
<!--          answer("man") -->
<!-- ) -->

<!-- ``` -->


<!-- ### Question 5 -->

<!-- ```{r question5} -->

<!-- question("When saving supplementary data files to accompany your package and projects, what's the most important thing?",  -->
<!--          answer("They should be in the form of data frames."),  -->
<!--          answer("They cannot contain character values."), -->
<!--          answer("They can only be saved with a variable name.", correct = TRUE), -->
<!--          answer("All data is saved in the same rda file.") -->
<!-- ) -->

<!-- ``` -->

<!-- ### Question 6 -->

<!-- Create a data frame named "records", with one column titled "tau" containing all the integers from 1 to 50 (inclusive), and another column titled "theta" containing 50 samples taken from the Uniform(1,10) distribution. Then, save it into the package. -->
<!-- ```{r question6, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r question6-solution} -->
<!-- tau <- c(1:50) -->
<!-- theta <- runif(50,1,10) -->
<!-- records <- data.frame(tau,theta) -->
<!-- use_data(records) -->
<!-- ``` -->



<!-- ### Question 7 -->

<!-- We're now going to deploy your package onto GitHub. Pretend that you have already created and are logged into an account on GitHub. Now, enter the function which will take you to the Personal Access Token creation page. -->


<!-- ```{r question7, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r question7-solution} -->
<!-- usethis::create_github_token() -->
<!-- ``` -->

<!-- ### Question 8 -->

<!-- Now that you have your (imaginary) PAT, let's set it within your R console. Type the function which will prompt you for your PAT and underneath that, type the function which will allow you to verify your connection. -->

<!-- ```{r question8, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r question8-solution} -->
<!-- gitcreds::gitcreds_set() -->
<!-- usethis::git_sitrep() -->
<!-- ``` -->

<!-- ### Question 9 -->

<!-- Create your new GitHub repository with your current project directory and make you initial commit. -->

<!-- ```{r question9, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r question9-solution} -->
<!-- usethis::use_github() -->
<!-- ``` -->

<!-- ### Question 10 -->

<!-- ```{r question10} -->

<!-- question("What should you remember when setting up your unit test for functions?",  -->
<!--          answer("We have to be in the R file we want to set tests for when we call use_test()."),  -->
<!--          answer("There are many different versions of expect_ which can test for different results."), -->
<!--          answer("It's best to coherently organize all of our tests so that we are clear on their aims."), -->
<!--          answer("All of the above", correct = TRUE) -->
<!-- ) -->

<!-- ``` -->

