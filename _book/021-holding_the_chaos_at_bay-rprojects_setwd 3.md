




# R Projects and working directory

Written by Isaac Ehrlich.


## Introduction

Whether you want to save a script, load data, or output graphs, R needs to know which folder to look for on your computer. The folder path you use for any given analysis or project is called the **working directory**.   

In this section, you will learn how to set a working directory using the function `setwd()` as well as how to use **RStudio projects**, and why RStudio projects are better for organization and reproducibility.

Some key concepts and functions to keep in mind throughout the section: **working directory**, **R Projects**, `getwd()`, `setwd()`.


## The working directory

The working directory is the folder path from which you can load or save files.
If you are working on a project in R/RStudio, then your working directory could be the folder containing all files and any additional sub-folders related to your project. Once you've let R know what this directory is, you could refer to (or call) various files contained in your working directory by providing the file name in your R script. This is true since the reference to each file is interpreted relative to the working directory. This, on the other hand, implies that files "living" outside this directory would need to be referenced using their full file path, otherwise you get an error. 

You can use the function `getwd()` to find your current working directory.

To change your working directory, you can use the function `setwd()` with the folder path of your new directory as the argument. For example, if I wanted to change my working directory to the folder `C:/Users/Documents/Scripts` I would use the command `setwd("C:/Users/Documents/Scripts")`. Alternatively, you can set the working directory through R's Toolbar, and then browse on your computer as shown in the image below (If you choose to do this, note what happens on the R console once you select your folder from the folder menu; you should see the `setwd()` function executed with your chosen folder path).

<img src="images/setwd.png" width="75%" />

### Drawbacks of `setwd()`

If you set your working directory manually in an R session (using either `setwd()` or through the toolbar), it is  likely that the folder path will be unique to your computer. In this case, if you or someone else was attempting to run your code on another device, they would first need to edit the folder path to which the working directory is set. While this is not necessarily critical, it decreases the usability of your code and the reproducibility of your analysis. To avoid this issue, RStudio has a feature called R Projects, discussed next.

## R Projects

R Projects are a type of file, labelled `.Rproj`, which designate a working directory. When an RStudio project is open, the working directory is automatically set to the folder path of the RStudio project. Now, the paths that you use to save and load files are all relative to the location of your RStudio project, rather than specific folder names on your computer. Therefore, instead of using `setwd()`, we encourage you to create an RStudio project at the beginning of any new project or assignment. This will improve your organization and reproducibility. The image below shows an example RStudio project setup. We will discuss recommended folder setups in the following section.

<img src="images/r-project-example.png" width="75%" />


### Creating and Opening R Projects

To create an R Project, go to 'File', and then select 'New Project'. RStudio will then ask if you wish to create the project in a new or existing directory. If you have already created a folder on your computer, select existing directory. Otherwise, select 'New Directory/New Project', and then name the project, and choose the location to store it on your computer.

To open an R project, you can go to 'File' and select 'Open Project' in RStudio. Alternatively, you can double click on the `.Rproj` file in your file explorer. Note, RStudio is capable of running multiple projects at the same time, but not within the same session. If you want to run multiple R Projects, you will need to open a new session.

## Common Mistakes & Errors

If you are using `setwd()`, make sure you are using proper syntax to define the folder path, and that the folder exists. Otherwise, you are likely to get the following error:


```r
setwd("C:This/Folder/Doesnt/Exist")
#> Error in setwd("C:This/Folder/Doesnt/Exist"): cannot change working directory
```

The syntax may vary depending on the operating system of your device.

## Exercises

<!-- ```{r repojq1, echo = FALSE} -->
<!-- question("R will automatically know where you want to save a file", -->
<!-- answer("True", message = "R might have a default, but it can't read your mind!"), -->
<!-- answer("False", correct = TRUE, message = "Correct! Don't forget about your working directory!"), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

<!-- ```{r repojq2, echo = FALSE} -->
<!-- question("If you are using an R Project, the working directory is set to", -->
<!-- answer("your desktop"), -->
<!-- answer("a random folder"), -->
<!-- answer("the folder containing the R Project", correct = TRUE), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

<!-- ```{r repojq3, echo = FALSE} -->
<!-- question("To specify the working directory, we recommend you use", -->
<!-- answer("setwd()"), -->
<!-- answer("an R Project", correct = TRUE), -->
<!-- answer("neither setwd() nor an R Project"), -->
<!-- answer("both setwd() and an R Project"), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

## Key Takeaways & Next Steps

* In order to successfully read and save files, you need to specify a working directory
* Setting a working directory through `setwd()` makes it hard to share and reproduce your analysis
* R Projects are a helpful tool to define your working directory and easily organize your assignments 

In the following section, we will discuss how to set up and organize your folders for a project in R.
















