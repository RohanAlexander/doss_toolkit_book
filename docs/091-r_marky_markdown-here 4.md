


# here and filepaths

*Written by Matthew Wankiewicz and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how about:

- Filepaths and the `here` package

Highlights:

- `here` allows you to reference filepaths in a more replicable way.
- If you have the option to use `file.path` vs `here`, `here` is generally the better option to use. 

## The content

When working on projects using R, filepaths are going to be an important part of calling datasets or saving files. Filepaths are important because when working in R projects, you will likely have multiple folders which contain both R scripts for cleaning or collecting data and also R markdown files or Shiny files to display your data. This section will look at how to properly use filepaths in R and will also introduce the `here` package which makes it easier to find your files. 

### Filepaths

Filepaths for files like .csv's in R will look like `../data/file.csv`. The second part will change depending on what your data folder is named and the file name will change depending on what you have named your file. Filepaths can be typed out but the process can be shortened by using the `file.path()` function. This function takes in strings for arguments and will create a file path using those strings. 

For example, if I have a .csv called '2021data' in a folder called 'data', if I write `file.path("data", "2021data.csv")` the function will create the file path `data/2021data.csv`. This file path can then be used to read in the file to bring the data into the file currently being worked on. This function will also work for other data types like .rds or .txt. 

### Here

The `here` package was created to make the finding of filepaths simpler. The main function in the package is `here()`, and is meant to be used as a replacement for the `file.path()` function we discussed earlier. `here` is good to use because it creates these filepaths relative to the project you are currently working in, helping you avoid any errors. 

Using the `here` function is identical to the use of `file.path`. Simply enter the name of the folder(s) and file you are trying to reach and the function will create a filepath through your current project to get to the desired file. This function can also be used to see what your current directory is. 

Another benefit to the `here` package is that the filepaths it creates are accessible for people using different operating systems. This means that if I use the function on a Mac, someone using a PC will be able to get the same result. `here` is also helpful because when working with R projects, you may run into issues where R cannot find a file in a directory you wrote out, but after using `here`, R will be able to find those files.

## Arguments

- `file.path:` This function just takes strings which it then turns into a file path for you.
- `here:` Like `file.path`, the only argument you need is the path you want to take. 

The `here` library also contains another function called `i_am`. This function tells the `here` function where to start the file path from. For example, if you are working in an R project and want `here` to run from a specific folder, it will tell it to start at that folder.
- When using `i_am` be sure to call it on an existing file or you will end up with an error.

## Examples

If we are working on a project which contains a folder called "Output" and a file called "Data_Analysis", we will find that `file.path` and `here` will return different paths. 

Firstly, with `file.path` we will get:

```r
file.path("Output", "Data_Analysis")
#> [1] "Output/Data_Analysis"
```

Next, when we use `here` we will get:

```r
here("Output", "Data_Analysis")
#> [1] "/Users/rohanalexander/Documents/projects/doss_toolkit_book/Output/Data_Analysis"
```

Both function do the same thing, but `here` just goes a little bit farther in making the path. This is extremely useful when creating projects because it will allow your work to be much more reproducible. 

Looking at `here::i_am`, we can say that we are working in a file called "filepaths.Rmd" and let `here` decide where to start the filepath from.

```r
## here::i_am("filepaths.Rmd")
```
The chunk above will return a string saying "here() starts at /Users/name/folder", depending on the file path your computer takes to get to the file. 

## Exercises

To get used to `file.path`, create the path `Users/DoSS/Toolkit` using `file.path`

<!-- ```{r file-path-exercise, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r file-path-exercise-solution} -->
<!-- file.path("Users", "DoSS", "Toolkit") -->
<!-- ``` -->

<!-- Now, try entering in the same argument with `here`. Don't worry if the filenames get repeated. -->

<!-- ```{r here-example-exercise, exercise = TRUE} -->

<!-- ``` -->

<!-- ```{r here-example-exercise-solution} -->
<!-- here("Users", "DoSS", "Toolkit") -->
<!-- ``` -->


<!-- ```{r here-mult-choice1, echo=FALSE} -->
<!-- question("Which function makes more extending file paths", -->
<!--          answer("makepath"), -->
<!--          answer("here", correct = T), -->
<!--          answer("file.path"), -->
<!--          answer("i_am"), -->
<!--          allow_retry = T) -->
<!-- ``` -->


<!-- ```{r here-mult-choice2, echo=FALSE} -->
<!-- question("When using `i_am`, can you use any file as the argument?", -->
<!--          answer("Yes"), -->
<!--          answer("No", correct = T,  -->
<!--                 message = "The file must be contained an existing file in the project."), -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r here-mult-choice3, echo=FALSE} -->
<!-- question("What are the benefits of using functions like `here` or `file.path` (Select all that apply)?", -->
<!--          answer("Usable over different OS's", correct = T), -->
<!--          answer("There are no benefits"), -->
<!--          answer("Can help avoid errors when calling for files", correct = T), -->
<!--          answer("It allows your work to be more replicable", correct = T), -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r here-mult-choice4, echo=FALSE} -->
<!-- question("True or False, can `here` be used inside functions like `read_csv` to read in files?", -->
<!--          answer("True", correct = T), -->
<!--          answer("False"), -->
<!--          allow_retry = T) -->
<!-- ``` -->


## Common Mistakes & Errors

- One common issue highlighted in this lesson was using `i_am` on files that aren't in your current project. This can happen from typing a file name wrong but if it didn't, make sure the file you're referencing is in your project/directory.
  - An example of this is the error saying: "Could not find associated project in working directory or any parent directory"
  
- One of the only errors which occurs with `here` is "Error in UseMethod". This only happens when you accidentally reference a function inside your `here` call. 

## Next Steps

Some more information on filepaths and `here` include:

- The website for the `here` package: https://here.r-lib.org/
- This blog post by Malcolm Barrett about the `here` package and why it is useful: https://malco.io/2018/11/05/why-should-i-use-the-here-package-when-i-m-already-using-projects/


## Questions

1. What does the `here` package do?
  a.  It makes it easier to find files you are working with
  b. Changes your R project name
  c. Makes it harder to work on a project
  d. None of the above
  
2. What does a file path look like?
  a. `data+file.csv`
  b. `data-file.csv`
  c. `data%>%file.csv` 
  d.  `/data/file.csv`
  
3. What is the output of `file.path("question", "3")`?
  a.  "question/3"
  b. "question,3"
  c. "question3"
  d. The function call will result in an error
  
4. True or False, using the `here` function is identical to the use of `file.path`?
  a.  True
  b. False
  
5. True or False, if I use `here` on a Mac, someone using the same function call on a PC will get a different result?
  a. True
  b.  False
  
6. What is returned when you run the `i_am` function?
  a. The R project name
  b.  The filepath leading to the file
  c. Your file's name
  d. Nothing
  
7. What causes the "Error in UseMethod" error?
  a.  You likely called a function inside `here`
  b. It happens randomly without explanation
  c. The `UseMethod` package is not installed
  d. None of the above
  
8. If I have a folder called "notes" that I am working in, what is the output of `here("folder", "file")`?
  a. "folder/file"
  b. "file"
  c.  ".../notes/folder/file"
  d. "notes"
  
9. If I have a folder called "notes" that I am working in, what is the output of `file.path("folder", "file")`?
  a.  "folder/file"
  b. "file"
  c. ".../notes/folder/file"
  d. "notes"
  
10. True or False, `here` and `file.path` work for any file type?
  a.  True
  b. False
  
  
  
  
  
  
  
  
  
  
  
  
  
  
