


# PDF outputs

*Written by Yena Joo and last updated on 7 October 2021.*

## Introduction
So far, we learned almost everything to write a proper paper, and the content should be exported into pdf document. In this lecture, we are going to learn how to produce a PDF in R Markdown.   

*Note that PDF output requires an installation of LaTeX.*


Prerequisite skills include:  

- You should know how to use RMarkdown. 

Highlights:  

- Use of YAML metadata

## PDF outputs
You have to use R Notebook or R Markdown to produce a PDF. When you open the Notebook, you specify the pdf_document output format in the YAML metadata. To have a PDF format, the Rmd file should look something like this:  

This is the original format of the R Markdown metadata, when you first create a new markdown document. 
```
---
title: "Title"
author: "Author"
date: "Feb 7, 2021"
output: html_document
---
```

Since we want the pdf output, change the `html_document` to `pdf_document`. 

```
---
title: "Title"
author: "Author"
date: "Feb 7, 2021"
output: pdf_document
---
```

Under `output`:  
- You can add a table of contents by writing `toc: true`.   
- You can also specify the depth of headers that it applies to using `toc_depth`.   
- You can add section numbering to headers using `number_sections`.   

``` 
---
title: "Title"
author: "Author"
date: "Feb 7, 2021"
output:
  pdf_document:
    toc: true
    number_sections: true
---
```


You can enhance the default display of data frames using `df_print`. 

```
---
title: "Title"
author: "Author"
date: "Feb 7, 2021"
output:
  pdf_document:
    df_print: kable
--- 
```

Also, there are various LaTex packages that may not be built in the template, but you can still include them to the YAML. 
Here is another example of including a package using `header-includes:`.  

```
---
title: "Title"
author: "Me"
header-includes:
   - \usepackage{LaTex pacakge of your choice }
output:
    pdf_document
---
```

You can find LaTeX packages on [CTAN(The Comprehensive TeX Archive Network) subpage](https://www.ctan.org/pkg/).  

  
## Exercises

### Question 1

<!-- ```{r q1_pdf, echo=F} -->
<!-- question_checkbox( -->
<!--   "What is the correct command to create table of contents? ", -->
<!--   answer("toc: false", correct = F), -->
<!--   answer("toc: 1", correct = F), -->
<!--   answer("toc_depth: true ", correct = F), -->
<!--   answer("toc: true", correct = T), -->
<!--   answer("toc_depth: 2", correct = F), -->
<!--   allow_retry = T, -->
<!--   random_answer_order = T, -->
<!--   incorrect = "Try again. You got this!" -->
<!-- ) -->
<!-- ``` -->


### Question 2

Modify the metadata so it changes into the pdf document with table of contents with depth of the header being 3, and add numbering to the header section. 

<!-- ```{r q2_pdf, exercise.eval = F, exercise=TRUE, eval = F} -->
<!-- --- -->
<!-- title: "Title" -->
<!-- author: "Author" -->
<!-- date: "Feb 7, 2021" -->
<!-- output: html_document -->
<!-- --- -->
<!-- ``` -->
<!-- ```{r q2_pdf-solution, eval= F} -->
<!-- --- -->
<!-- title: "Title" -->
<!-- author: "Author" -->
<!-- date: "Feb 7, 2021" -->
<!-- output: -->
<!--   pdf_document: -->
<!--     toc: true -->
<!--     toc_depth: 3 -->
<!--     number_sections: true -->
<!-- --- -->
<!-- ``` -->


## Next Steps
Using all the functions we learned so far, try to write a paper of your interest, cite the sources, and knit to PDF to create a perfect professional paper. 


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
