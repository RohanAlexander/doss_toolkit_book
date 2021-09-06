



# Introduction to R Markdown

*Written by Shirley Deng.*

## Introduction

Have you ever found yourself typing up a report in Microsoft Word and tried to insert code, code output, images or math? It can be pretty cumbersome! 

But it's *not a problem anymore*...

R Markdown documents allow you to not only type up reports, as you would in a Word document, but allow you to embed R, Python and SQL code with (hopefully) a little less fuss.

### Why use R Markdown?

R Markdown allows for our files to be reproducible - if you or someone else finds an error in your code, or there's a figure you want to fix, or there's just a typo with a symbol - there's no need to remake a new document from scratch. 

Instead, you can edit the .Rmd file and "knit" (or compile) it to make your new html, .pdf or Word document. You can think of R Markdown as writing reports with code.

## Creating a R Markdown file

To start a .Rmd file in RStudio, click *File*, then *New File*, and select *R Markdown...*

From there, we can select if we want our report to be in the form of an **HTML page**, **pdf**, or **Word document**, and give our report a title and author name.

RStudio will then generate a .Rmd file with a little template for us

### YAML Header Chunk

We notice that the template starts off with something like the following chunk:

```
---
title: "A Good, Creative Title"
author: "Shirley Deng"
date: "01/01/2021"
output: pdf_document
---
```

As you might guess, this creates a header for your report with the title, author and date specified.

We can also change the output option if we have a change of heart and would prefer an HTML page or Word document:

* `output: pdf_document`
* `output: word_document`

## Markdown

Following the header chunk, we see a little section on R Markdown.

Markdown is a way for us to format our report text, and the sections below will outline how to use it.

### Sections

The two pound signs, `#`, in front of *R Markdown* indicate that that line of text will be a header.

Whenever we use the pound sign to denote a header, this also creates a section in our final report document. We can view these sections by toggling the document outline with the following keyboard shortcuts:

* `Cmd+Shift+O` on Mac
* `Ctrl+Shift+O` on Windows and Linux

For each `#`, the smaller the header. We can use smaller headers to denote subsections.

### Paragraphs

To indicate a new paragraph, place two spaces at the end of the line.

For example, this line ends with two spaces...`  `  
And this text follows it.
    
#### Note

Pressing the tabulator key, `Tab` on your keyboard, will *not* indent a paragraph!

### Bold Text

We can bold text by putting a pair of asterisks, `**`, around it.

For example, we can write **bold** with `**bold**`.

### Italicized Text

We can make text italicized by either using a single asterisk, `*`, around it.

Alternatively, we can also use an underscore, `_`, instead of the asterisk.

For example, we can write *italics* with `*italics*` or `_italics_`.

### Superscript

We can make superscript by using a caret, `^`, around it. 

For example, we can write this s^uperscript^ with `s^uperscript^`.

### Subscript

We can make subscript the same way we make superscript, except with a tilde, `~`, instead of a caret.

For example, we can write this s~ubscript~ with `s~ubscript~`.

### Lists

We can make lists by either using thr asterisk, `*`, dash, `-`, or plus sign, `+`, as bullets.

For example...

```
* this
* would
* make
```

the following list:

* this
* would
* make

And, 

```
- this  
- also   
- makes
```

this list:

- this
- also
- makes

And,

```
+ so  
+ does  
+ this
```

this list:

+ so  
+ does  
+ this

### Sublists

We can also use an indent to create a sublist.

For example,

```
- this
  - makes a sublist
```

like so:

- this
  - makes a sublist
  
### Ordered lists

We can also makew numbered lists, simply by numbering each item.

For example,

```
1. this
2. is
3. numbered
```

Like this:

1. this
2. is
3. numbered

### Hyperlinks

We can make a hyperlink by using the syntax `[text here](link url here)`

For example, 

```
[this makes a link to the RStudio website](https://www.rstudio.com/)
```

like this:

[this makes a link to the RStudio website](https://www.rstudio.com/)

### Images

We can embed images (with caption!) similar to how we make hyperlinks.

We just add an exclaimation point, `!`, in front of the hyperlink syntax.

For example, 

```
![this embeds a picture of the RStudio icon like so](https://d33wubrfki0l68.cloudfront.net/521a038ed009b97bf73eb0a653b1cb7e66645231/8e3fd/assets/img/rstudio-icon.png)
```

like this:

![this embeds a picture of the RStudio icon like so](https://d33wubrfki0l68.cloudfront.net/521a038ed009b97bf73eb0a653b1cb7e66645231/8e3fd/assets/img/rstudio-icon.png)

### Hyperlinked images

If you want to get *real* fancy, we can hyperlink images using a combination of the syntax we introduced above.

For example,

```
[![this embeds a clickable picture of the RStudio icon](https://d33wubrfki0l68.cloudfront.net/521a038ed009b97bf73eb0a653b1cb7e66645231/8e3fd/assets/img/rstudio-icon.png)](https://d33wubrfki0l68.cloudfront.net/521a038ed009b97bf73eb0a653b1cb7e66645231/8e3fd/assets/img/rstudio-icon.png)
```

[![this embeds a clickable picture of the RStudio icon](https://d33wubrfki0l68.cloudfront.net/521a038ed009b97bf73eb0a653b1cb7e66645231/8e3fd/assets/img/rstudio-icon.png)](https://d33wubrfki0l68.cloudfront.net/521a038ed009b97bf73eb0a653b1cb7e66645231/8e3fd/assets/img/rstudio-icon.png)
  
### Escapes

There are some special characters, called **metacharacters**, that need an **escape** (a backslash, `\`), in order to display properly. For example,

In order to write this... | we'd have to write this
------------------------- | -------------------------
\$                        | `\$`
\&                        | `\&`
\%                        | `\%`
\##                        | `\#`
\_                        | `\_`
\{                        | `\{`

## Math environments

Writing math in R Markdown is probably one of its best features. To do so, we use another format - LaTeX.

Like how R Markdown can be likened to writing reports with code, we can liken LaTeX to writing mathematical equations with code.

### Delimiters

Say we wanted to write the Pythagorean theorem, \(x^2 + y^2 = z^2 \).

We need to work in a math environment, or **math mode**, in order to write math using LaTeX.

#### Inline

Sometimes we want to write a little bit of math in the middle of some text. In this case, we'd want our math *in line* with the rest of our text.

If we want our Pythagorean theorem inline, like above, we can write it as this:  `\(x^2 + y^2 = z^2 \)`

to get this: \( x^2 + y^2 = z^2 \)

#### Centred Display

But sometimes we want to showcase our math. Say, in the case we're introducing an important equation.

If we have some math we'd like on its own line and centred, we can write this: ` \[ x^2 + y^2 = z^2 \] `

to get this: \[ x^2 + y^2 = z^2 \]

Alternatively, we can also write this: ` $$ x^2 + y^2 = z^2 $$ `

to get this too: $$ x^2 + y^2 = z^2 $$

#### Aligned

What if we have multiple lines of math that we want to showcase? Like this:

\begin{aligned}
a = 1 \\  
b = 2
\end{aligned}

It would be pretty inconvenient to type \$\$ around every line:

```
$$ a = 1 $$  
$$ b = 2 $$
```

Instead, we can use the `aligned` delimiters around our math, using `\\` to end each line.

```
\begin{aligned}
a = 1 \\  
b = 2
\end{aligned}
```

However, it's not neccessary to end the last line with `\\`. 

This:

```
\begin{aligned}
a = 1 \\  
b = 2 \\
\end{aligned}  
```

Can yield this:  
\begin{aligned}
a = 1 \\  
b = 2 \\
\end{aligned}  
Too. 

### Superscript

Recall from our Markdown section that we use carets, `^`, for superscript. 

For example, we can write this s^uperscript^ with `s^uperscript^`.

We also use carets when we want superscript **in math environments**, albeit *slightly* differently.

Instead of wrapping the superscripted text with the carets, we use a single caret, followed with the text wrapped in curly brackets, `{}`.

For example, let's try using the inline delimiters `\(\)` to write \(s^{uperscript}\):

`\(s^{uperscript}\)` yields \( s^{uperscript} \)

#### Note: Remember to use the curly brackets! 

Notice that `\( s^uperscript \)` yields \( s^uperscript \).

Without curly brackets, only the **first character** that follows the caret is superscripted.

### Subscript

The same way superscripts and subscripts are paralled in Markdown applies to math environments.

For example, `\(s_{uperscript}\)` yields \( s_{uperscript} \),

And without curly brackets, `\( s_uperscript \)` yields \( s_uperscript \)

### Math escapes: brackets and dolla dolla bill \$ignz

What happens when we want to use brackets *in* math environments?

In order to write this... | we'd have to write this
------------------------- | -------------------------
\( \$ \)                  | ` \$ `
\( \& \)                  | ` \& `
\( \% \)                  | ` \% `
\( \## \)                  | ` \## `
\( \_ \)                  | ` \_ `
\( \{ \)                  | ` \{ `

For example, we can write a spicy \( \$pi\_c \) by using `\( \$pi\_c \)`.

#### Exceptions? 

What are some circumstances we *shouldn't* use an escape?

In order to write this... | we can just write this
------------------------- | -------------------------
\( [ \)                   | ` [ `
\( ( \)                   | ` ( `

### Other syntax

There's specific syntax for a lot of the more complex mathematical symbols we might find ourselves using!

#### Note: For the rest of the *Math environments* section, we will be making use of the inline delimiters `\( \)` **unless** otherwise specified.

#### Fractions:

We can use ` \frac{numerator}{denominator} ` to get \( \frac{numerator}{denominator} \).

#### Binomials:

We often see \( {n \choose k} \) when working in combinatorics or probability.

Similar to the fraction syntax, we can use ` \binom{top}{bottom} ` to get \( \binom{top}{bottom} \).

Alternatively, we can use ` {top \choose bottom} ` to get \( {top \choose bottom} \) as well.

#### Integrals

##### Indefinite

To get a plain Jane, indefinite integral, we can simply use ` \int ` to get \( \int \).

If we have multiple integrals, we just add an `i` for each additional one, as so:

In order to write this... | we can write this        
------------------------- | -------------------------
\( \int \)                | ` \int `                 
\( \iint \)               | ` \iint `                
\( \iiint \)              | ` \iiint `
\( \iiiint \)             | ` \iiiint `

What if we wanted more space between our integrals? Then simply use `\int` multiple times.

For example, `\int\int` would give us \(\int\int\).

##### Definite

We can make use of the superscript and subscript syntax in order to make our indefinite integrals into definite integrals.

For example, `\int_a^b` would give us \( \int_a^b \).

What if we had something more complex, like \( \int_{a+b}^{c-d} \)? We could use curly brackets, like so: `\int_{a+b}^{c-d}`

#### Sums 

Like with integrals, we can get *just* the sigma for summation, \(\sum \), with `\sum`.

To get the indices, once again we make use of the syntax we've learned already.

For example, `\sum_{i=1}^{n}` would give us \( \sum_{i=1}^{n}\).

#### Limits

This is getting repetitive!

To get \( \lim_{n \rightarrow \infty} \), we can use `\lim_{n \rightarrow \infty}`

#### Note: More resources on LaTeX math syntax can be found in the *Resources and references* section :\^)

### Spaces

Spaces created by pressing the space bar don't really work in math mode!

Instead, we have several options for writing spaces in math environments.

We see that this...       | will give us this
------------------------- | -------------------------
` poo poo `               | \( poo poo \)
` poo \; poo `            | \( poo \; poo \)
` poo \: poo `            | \( poo \: poo \)
` poo \, poo `            | \( poo \, poo \)
` poo \! poo `            | \( poo \! poo \)

## Code

Another handy feature of R Markdown is that we can **display and run** code in its own *code-y* font.

### Displaying

#### Inline

Say we just want to indicate that something is code, without actually providing the full section it came from, let alone run it. 

To display a bit of code inline with the rest of our text, we can wrap the code with a pair of backticks, ` `` `.

For example, we can write `this` with \`this\`

#### Blocks

But what if we have a whole block of code we want to show?

We can wrap the code using **three or more** backticks instead.

For example:

```
this is a whole lot of code
```

created with,

    ```
    this is a whole lot of code
    ``` 

##### Readability

While we could write this all in a single line, like this:

    ``` this is a whole lot of code ```

It's much easier on the eyes to keep the backticks on their own lines.

![MY EYES](https://www.youtube.com/watch?v=Qn977W9HjWM)

### Running

To *run* R code in our R Markdown file, we need to insert a code chunk.

We can do so with the following keyboard shortcuts:

* `Cmd+Option+I` on Mac
* `Ctrl+Alt+I` on Windows and Linux

From there, we can fill the code chunk with our code.

For example,

This:

\`\`\`\{r\}  
x <- 1  
\`\`\`

Yields this:


```r
x <- 1
```


### Chunk options

There are some commong chunk options we make use of to adjust what we want to happen when we compile, or *knit*, our R Markdown documents.

By default, any output from our code chunks will be shown in the document once knit. What if we *don't* want the code itself to show, only the output? Then we can use the `echo` option.

For example, this:

\`\`\`\{r\, echo=F}  
x <- 1  
x  
\`\`\`

Yields this:


```
#> [1] 1
```

We can also have *only* the code show, but no output, using the `eval` option.

For example, this:

\`\`\`\{r\, eval=F}  
x <- 1  
x  
\`\`\`

Yields this:


```r
x <- 1
x
```

More code chunk options can be found [here](https://rmarkdown.rstudio.com/lesson-3.html).

## Resources and references

### Introductory

#### From RStudio

* [Introductory R Markdown guide](https://rmarkdown.rstudio.com/lesson-1.html)
* [R Markdown quick reference guide PDF](https://rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf)
* [R Markdown **cheatsheet**](https://rstudio.com/wp-content/uploads/2015/02/rmarkdown-cheatsheet.pdf)
* [R Markdown **keyboard shortcuts**](https://support.rstudio.com/hc/en-us/articles/200711853-Keyboard-Shortcuts)
* [**R Markdown: The Definitive Guide**](https://bookdown.org/yihui/rmarkdown/)

#### From other sources

* [Karl Broman's "Reproducible reports with R Markdown" guide](https://kbroman.org/datacarpentry_R_2018-06-04/04-rmarkdown.html)
* [Our Coding Club's "Getting Started with R Markdown" guide](https://ourcodingclub.github.io/tutorials/rmarkdown/)
* [University of Kansas' "R Markdown Basics" guide](https://cran.r-project.org/web/packages/stationery/vignettes/Rmarkdown.pdf)

### LaTeX 

* [Overleaf guides](https://www.overleaf.com/learn)
* ["Introduction to LaTeX: 2. Typing Math" guide from the University of Illinois at Urbana-Champaign](https://faculty.math.illinois.edu/~hildebr/tex/course/intro2.html)
* [More on integrals](https://math.meta.stackexchange.com/questions/4497/how-to-show-the-integral-symbol-on-this-site/)
* [Spacing](http://www.emerson.emory.edu/services/latex/latex_119.html)
* [Escape character](https://tex.stackexchange.com/questions/34580/escape-character-in-latex)















