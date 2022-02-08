


# Reading tables dta and other data types

*Written by Isaac Ehrlich and last updated on 7 October 2021.*

## Introduction

Unfortunately, not all data that you may need to read into R will be stored in nice, easily-readable '.csv' files. To handle alternate data file types, `tidyverse` has a series of read-in functions beyond `read_csv()`. This includes `read_table()`, `read_table2()`, `read_excel()`, `read_fwf())`, and `read_delim()` for tabular data, `read_file()` and `read_lines()` for non-tabular data, and functions in the tidyverse `haven` package for reading data formats from other statistical languages such as `read_sas()`, `read_sav()`, and `read_dta()`.      

In this lesson, you will learn how to:

- Read in a variety of alternate data file types, including tabular, non-tabular, and statistical package data


Prerequisite skills include:

- Installing packages and calling libraries
- Knowledge of `read_csv()` and its arguments

## Tabular Data

The following functions all take similar arguments to `read_csv()`, which are broken down in the previous module. The following sections will instead focus on the different types of files and formats each function is capable of reading.

**`read_table()`: **
`read_table()` reads tabular text data where each column is separated by one (or more) spaces. `read_table()` is frequently used to read in space-delimited `.txt` files but can handle other text file types as well. `read_table()` requires that each line is the same length, and each column is in the same position.

**`read_table2()`: **
`read_table2()` is similar to `read_table()`, but does not require each line to be the same length. 

**`read_fwf()`: **
`read_fwf()` reads in **f**ixed **w**idth **f**ile types. Fixed width files are files where the data is not delimited in any way, but like the proper input to `read_table()`, these files have columns that are in the same place on every line; hence, they are "fixed width." `read_fwf()` takes the additional argument `col_positions`, which specifies the position at which each column begins.

**`read_delim()`: **
`read_delim()` is the general case of `read_csv()`, where the user can specify which single character the file is delimited by, rather than defaulting to the comma, as in `read_csv()`. `read_delim()` takes in the additional argument `delim`, which specifies by which single character columns in the raw file are separated.

**`read_excel()`: **
`read_excel()` reads in `.xls` and `.xlsx` files (Microsoft Excel file types). `read_excel()` takes the additional argument `sheet` that specifies which sheet of an Excel file to read, either using the name of the sheet as a string or the index. If the argument is not specified, `read_excel()` will default to the first sheet.

## Non-Tabular Data

**`read_file()`: **
`read_file()` reads an entire file as a single string into a single vector.

**`read_lines()`: **
`read_lines()` reads each line of a file as a separate string, and creates a list of strings.

## Statistical Package Data (Using the Tidyverse `haven` Package)

**`read_sas()`: **
`read_sas()` reads `.sas7bdat` and `.sas7bcat` files generated in SAS.

**`read_sav()`: **
`read_sav()` reads `.sav` files generated in SPSS.

**`read_dta()`: **
`read_dta()` reads `.dta` files generated in Stata. One particularly common way to use it is in combination with `labelled::to_factor()`. This then adds the labels into the dataset. Otherwise they are stored separately. For instance, a typical usage is something like:


```r
my_dta_dataset <- 
  read_dta("my_dta_dataset.dta"))

# The Stata format separates labels so reunite those
my_dta_dataset <- 
  labelled::to_factor(my_dta_dataset)
```

## Overview and next steps

There are many different file types you may come across, but fortunately tidyverse has a fairly extensive set of functions to read in from as well. Happy reading!


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
