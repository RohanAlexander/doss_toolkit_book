



# Folder set-up

Written by Isaac Ehrlich.


## Introduction

In this lesson, we will discuss how to set up folders for assignments and projects in R. As the folder structure revolves around an RStudio project, make sure you have gone through the RStudio project lesson as well.

### Folder Set-Up Motivation
Many assignments and analyses you complete will require multiple files, including data files, code, and written reports. To keep these organized, we recommend using a consistent folder structure system. This will make loading data into your R environment simpler, and will help keep your analyses organized.

## Folder Set-Up
After creating a folder with an R Project, you will want to create additional sub-folders to keep your materials organized. Ideally, you will have very few files (if any) in the same folder as your R Project - they should instead be stored in sub-folders as in the image below.

![Example Folder Set-Up](images/folder-setup.png)

We recommend using the following sub-folders:


### Data/Input Folder
One of the folders you will want to create is the `data` folder. Here, you will want to keep the original and cleaned data files you use in your analysis.

### Figure/Plot Folder
Whether you are creating your own plots or using pictures and figures from another source, a dedicated `figure` folder will help you keep any images you may want to use organized.

### Results/Output Folder
If you create any new data sets or have output from your analysis, you will definitely want to keep track of the these. A `results` folder will help keep your output organized.

### Code/Scripts Folder
If you are completing an assignment in R, you will certainly have written code and scripts you want to save. Whether for cleaning data or running complex analysis, be sure to save these files to a folder containing all of your code.

### Other/Miscellaneous Folder (If Necessary)
On occasion you may find that you are using files that don't quite fit into any of the other folders. Rather than have these files float around your R Project, you may want to create an additional `other` folder and put those files in.

## Key Takeaways
* Sub-folders help keep your files and analysis organized.
* You will typically want to include folders for data, figures, results, and code.
* Remember these are just recommendations! Experiment and figure out what works best for you.

## Exercises


<!-- ```{r q1, echo = FALSE} -->
<!-- question("You should keep your root directory clean and instead save files to specific sub-folders", -->
<!-- answer("True", correct = TRUE), -->
<!-- answer("False", message = "Remember you'll want to keep your projects organized!"), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

<!-- ```{r q2, echo = FALSE} -->
<!-- question("You must have the exact folders described in this section for all your projects", -->
<!-- answer("True", message = "We definitely recommend using them, but make sure to figure out what works best for you!"), -->
<!-- answer("False", correct = TRUE, message = "Remember to figure out what works for you!"), -->
<!-- allow_retry = TRUE) -->
<!-- ``` -->

## Next Steps
You're well on your way to keeping an organized project! Next we'll talk about how you can use comments to keep your code readable and organized!














