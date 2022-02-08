


# Writing R Packages

*Written by Matthew Wankiewicz and last updated on 7 October 2021.*

## Introduction

While working on projects, you may get to the point where you want to create your own package in R. This package could be as simple as containing a temperature converter between Fahrenheit to Celsius or could contain a web-scraper which helps you get data you would like to analyze. This lesson will help go over the basics of creating a package in R.

Before we begin, be sure to have the `devtools` and `roxygen2` packages installed as they are very useful when creating packages. 

While there are a few different ways to create package in R, the method we will look at in this lesson is great for getting started.

## Steps for Making a Package in R

1. After you have installed `devtools` and `roxygen2`, create a new R project, then click new directory and then R package. Here you will name your R package and include any files to the creation of the package. Once you have selected any files, click "Create Package" to make the package. 

2. Now that the package has been created, there will be files located in the lower right-hand corner. The files include: "DESCRIPTION", "man" and "R". "DESCRIPTION" is where you can tell users about your package, including the name, description, and author. Next, the "man" folder is where you describe the functions in your package. These files are saved as ".Rd" files which stands for R documentation. The descriptions include the name, usage, description and a few examples of the functions. Lastly, the "R" folder will contain R scripts where you will write your functions. 
    - You can create as many functions as you want, just make sure that there is a ".Rd" file for each of the functions you have created.
    - You don't need to edit the .Rd files on your own. The `roxygen` package can create this documentation based off of your functions. This is shown in the video later on. 
  
3. Once you have written your functions, you can install your package to your R by using Cmd + Shift + B for Mac or Ctrl + Shift + B for Windows. Once the package has been installed, you can test out your functions to make sure they are working properly. If your functions work fine, you have successfully created a package in R! Now you can either upload the code to GitHub for others to look at or you can continue building onto your package.
    - If you plan to add functions from other packages into your package, make a new heading in "DESCRIPTION" called "Imports" and list the functions you are adding in. 

4. There are other ways to create packages which are more advanced than the steps I have detailed, more information about these steps will be included in the "Further Reading" Section.

## Each Section of Packages in depth

**Description**: The description file will look similar to the one below:
![Image from Analytics Vidhya](https://cdn.analyticsvidhya.com/wp-content/uploads/2017/03/20070011/R7.png)

Filling it out is fairly simple and when you first enter this file, it will tell you what you should enter for each heading. For the license you can pick whichever one you want (located [here](https://choosealicense.com/licenses/)), the most common ones are MIT and Apache.

**Man folder:** The "man" folder will look similar to the one below:
![Photo from Piping Hot Data](https://www.pipinghotdata.com/posts/2020-10-25-your-first-r-package-in-1-hour/img/document2.PNG){width=70%}

For each `\topic{}` you should fill out the corresponding topic of your package in the {}. In `\usage` you should enter in how to use the function you're describing. In `\arguments` enter in the arguments and a brief description of the argument, each argument should be separated by `\itemn` where n is the number of the argument. `\examples` includes examples of your function in action. While you can fill this out on your own, `roxygen` can do this automatically. 

**R folder:** The R folder is where you place your functions. Each function will be contained in separate R files. You can keep all of your functions in one R file, it just helps to keep things organized if you have a file for each function. 

The inside of the files will look like the image below:

![Photo from Analytics Vidhya](https://cdn.analyticsvidhya.com/wp-content/uploads/2017/03/20070032/R9.png)

For `@title` you should write the title of the function, `@description` is where the description goes, `@param` is where your parameters go, `@return` is what your function returns and `@examples` are examples of how to use the function. Below that part is where you write out your entire function. This should be repeated for every function you plan to include in your package. 

**NAMESPACE:** The NAMESPACE file is a more advanced file for making R packages. From the R Packages book from Hadley Wickham, it says that this file is "not that important if you’re only developing packages for yourself. However, understanding namespaces is vital if you plan to submit your package to CRAN". NAMESPACE files can also be created automatically from `roxygen`. 


### After you have filled out each file

Once you have filled out each file with your functions you are now ready to build your package. To do this, go to your menu bar and select "Build" and then "Configure Build tools...". Once you have selected this there will be a new window that opens which includes options for the package. Check off the box that says "Create documentation with Roxygen" then select all checkboxes and click "OK" if another window appears. You can also type in "-–as-cran" into "Check Package", this will let R conduct tests to simulate your package being checked/tested in CRAN. 

  - Creating documentation with Roxygen takes information from your functions and creates documentation from it. It is also able to create a NAMESPACE file. In order to do this, make sure you have your NAMESPACE file deleted so Roxygen can make a new one and don't make any R documentation for your functions, Roxygen can do it for you. 

Now you can go back to "Build" and then click "Clean and Rebuild". This will restart your R session and load in your package to R. Now you can test out your functions to make sure they are working properly. If your functions work without error, you have successfully created your package!

### Sharing Your Package

If you would like other people to use your function and want to share it, there are two main options. The first option (and easiest) would be to upload your package to GitHub. To do this, create a GitHub repository and upload your files to the repository. Once the files are on GitHub, it can be installed using `remotes::install_github`.

You can also select Git when creating your package. After you have created and edited your functions & files, you can use the `usethis::use_github` to create a repository for your package. If you haven't done this before, the function will give you steps in creating a key to connect to your GitHub and will also tell you how to store it. Once you have done this, you can re-run the function and it should upload your files to GitHub. 

As you get more advanced with creating packages in R, you can send it to CRAN to try to get it verified there. Having your package verified by CRAN means that the package can be installed using `install.packages`. To get the package CRAN verified, you would need to submit your source package to https://cran.r-project.org/submit.html. To create a source package, go to "Build" then "Build Source Package". R will then create a ".tar.gz" file which can be uploaded to the CRAN website. 

## Live Coding

Video displaying live coding of an R package:

<iframe width="560" height="315" src="https://www.youtube.com/embed/wLGRLCXIAYA" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

To get your access token from GitHub use `usethis::browse_github_token`, it will open up a new page and you can access a token from GitHub there. It will also tell you how to store your token after running the function. (This is also covered in the GitHub lessons.)

## Exercises

<!-- ```{r making-packages-q1, echo=F} -->
<!-- question("Which packages are very important to the creation of R packages? (Select all that apply)", -->
<!--          answer("`devtools`", correct = T), -->
<!--          answer("`roxygen2`", correct = T), -->
<!--          answer("`dplyr`"), -->
<!--          answer("`rvest`"), -->
<!--          random_answer_order = T, -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r making-packages-q2, echo=F} -->
<!-- question("What is the importance of the 'man' folder when making a package?", -->
<!--          answer("This folder contains the R scripts for the functions in the package"), -->
<!--          answer("This folder contains documentation for the functions in the package", -->
<!--                 correct = T), -->
<!--          answer("This folder contains code for GitHub"), -->
<!--          answer("This folder is not important"), -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r making-packages-q3, echo=F} -->
<!-- question("Where do the R scripts for your functions go?", -->
<!--          answer("The R folder", correct = T), -->
<!--          answer("The 'man' folder"), -->
<!--          answer("The NAMESPACE file"), -->
<!--          answer("The DESCRIPTION file"), -->
<!--          random_answer_order = T, -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r making-packages-q4, echo=F} -->
<!-- question("What is in the DESCRIPTION file?", -->
<!--          answer("Information about the package, including your contact information.",  -->
<!--                 correct = T), -->
<!--          answer("Descriptions of each function."), -->
<!--          answer("The code behind each of the functions"), -->
<!--          answer("The combination of all code and text in your package"), -->
<!--          random_answer_order = T, -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r making-packages-q5, echo=F} -->
<!-- question("What are the best ways to let anyone access your package? (Select all that apply)", -->
<!--          answer("Upload your package files to GitHub", correct = T), -->
<!--          answer("Submission and approval by CRAN for your package", correct = T), -->
<!--          answer("Packages you create cannot be shared"), -->
<!--          answer("Once you make a package anyone can use it, even if it's not on CRAN or GitHub"), -->
<!--          random_answer_order = T, -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r package-questions-6, echo=F} -->
<!-- question("True or False: You can only have one function in an entire package?", -->
<!--          answer("True"), -->
<!--          answer("False", correct = T), -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r package-questions-7, echo=F} -->
<!-- question("What does the 'Install and Restart' button do?", -->
<!--          answer("Installs your package into R and lets you use it", correct = T), -->
<!--          answer("Refreshes your package to the last save"), -->
<!--          answer("Installs your package into R but does **not** let you use it"), -->
<!--          answer("Restarts your R session to let you work on a new package"), -->
<!--          random_answer_order = T, -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r creating-packages-steps, echo=F} -->
<!-- order <- c("Select 'New Project' in RStudio", "Select 'New Directory'", -->
<!--            "Select 'R Package' and Name your package", "Edit the files", -->
<!--            "Configure Build Tools... create documentation with `roxygen`", -->
<!--            "Clean and Rebuild", "Share the Package with others!") -->

<!-- question_rank("What is the correct order in making a new R package in RStudio?", -->
<!--               answer(order, correct = T), -->
<!--               answer(rev(order), message = "Wrong direction"), -->
<!--          allow_retry = T) -->
<!-- ``` -->


## Next Steps

Some next steps for making packages include:

- The R packages book by Hadley Wickham and Jenny Bryan: https://r-pkgs.org/
- The CRAN documents on writing packages: https://cran.r-project.org/doc/manuals/r-release/R-exts.html


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

