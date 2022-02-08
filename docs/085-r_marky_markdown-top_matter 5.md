


# Top Matter: Title, Date, Author, Abstract

*Written by Yena Joo and last updated on 7 October 2021.*

## Introduction

When writing a formal paper or an essay using R, you are going to be writing in RMarkdown, and the first page of the paper should include a good title, date, author, and a neat abstract. Using latex in Markdown, it would be simple and easy to create a good first page of your essay. 

Prerequisite skills include:   

- nothing much, just the topic of your own choice and functions we have learned so far which could be a good asset to your essay!

Highlights:   

- Format of a paper  
- YAML metadata  
- Abstract  

## Title, Date, Author

When you create a new R Markdown file, this is going to be a default latex template the Markdown creates as follows: 
![Default latex template chunk](images/69_markdown.png){width=80%}


The template creates the default title, author, date, and output type for you. All you need to do is to change the green coloured texts into whatever you would like. Also, most of the formal research papers are created in pdf documents. If you need to write in pdf, you could change the output type to `output: pdf_document`, instead of `hmtl_document`.    

For example:    

```
---
title: "How to create a perfect essay"
author: "Your Name"
date: "April 28, 2021"
output: pdf_document
---
```
  
If you are starting from a blank R Notebook file, you can just copy and paste this chunk of code above and get started. 

## Abstract

The abstract of a research paper is a part that implies/summarizes only the most important points of the paper. You should include: 

1. The purpose/goal of the study and the research problem
2. Design of the study and how it was conducted/analyzed
3. Major findings and results of the study/analysis that you conclude with

You should write the abstract after you have finished writing the entire paper. The abstract is usually in one paragraph that readers could know the broad content of the paper just by reading it.  

Also, try not to use every detail of your paper, or numeric references to the bibliography or sections of your paper, since readers would not have access to the full paper, and they would not have enough time to go over the entire paper to look for the references. Make sure to focus on the core contents.  

To create an abstract, you would first need a header:  

```
## Abstract 
```
Then, get started on the abstract once you finished writing your entire paper.  

## Exercises

### Question 1 

<!-- ```{r q1_topmatter, echo=F} -->
<!-- question_checkbox( -->
<!--   "To create a pdf document from your R Markdown document, what do you have to put in the YAML metadata of your document?", -->
<!--   answer("output: html_document", correct = F), -->
<!--   answer("output_style: pdf_document", correct = F), -->
<!--   answer("output: pdf_document", correct = T), -->
<!--   answer("pdf_document", correct = F), -->
<!--   allow_retry = T, -->
<!--   random_answer_order = T, -->
<!--   incorrect = "Try again. You got this!" -->
<!-- ) -->
<!-- ``` -->

### Question 2
<!-- ```{r q2_topmatter, echo=F} -->
<!-- question_checkbox( -->
<!--   "What do you have to include in your abstract? Select all that apply.", -->
<!--   answer("The purpose/goal of the study", correct = T), -->
<!--   answer("Major findings and results", correct = T), -->
<!--   answer("Design of the study and how it was conducted", correct = T), -->
<!--   answer("numeric references to bibliography or sections", correct = F), -->
<!--   answer("complex mathematical notations", correct = F), -->
<!--   allow_retry = T, -->
<!--   random_answer_order = T, -->
<!--   incorrect = "Try again. You got this!" -->
<!-- ) -->
<!-- ``` -->

### Question 3
Read the following chunk: 
```
---
title: "This is a title"
author: "Kelly"
date: "January 2022"
output: html_document
---
```
What do you need to change if you want to create a PDF document? 
a. title  
b. author  
c. date  
d. output  

### Question 4
What do you have to include in an abstract?  
a. Design of the study   
b. goal of the study   
c. major findings of the study   
d. all of the above  

### Question 5


### Question 6

### Question 7

### Question 8

### Question 9

### Question 10


## Common Mistakes & Errors

There is not much space to make a mistake here, but take your time to write your abstract. Do not include too much information in your abstract. Think of your abstract as an appetizer of the meal, it is to show the readers a big picture of your paper.  

## Next Steps

You can now create a well-formatted first page of your paper. Try adding Introduction, Method, Analysis, Visualization, Discussion, and Conclusion parts to your paper, and have fun! In the next lecture, you will learn how to create a nice table that could be presented in papers. 



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
