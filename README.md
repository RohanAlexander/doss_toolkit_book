## DoSStoolkit <img src="images/stitches_hex_all.png" align="right" height="200" />

The DoSS Toolkit is a collection of self-paced materials to help you learn and use R.

We all know that R is a critical part of applied statistics and data science these days, but it can have a steep learning curve and be intimidating to get started with. 

The [Department of Statistical Sciences](http://www.utstat.utoronto.ca/) (DoSS) toolkit is a free series of open source online modules by undergraduates, that their fellow students and the public can use to learn the essentials of R. 





--



## Style Guide

Based on: https://github.com/UBC-DSCI/introduction-to-datascience

#### General

- Use Canadian spelling
- Expand all contractions
- 80 character line limit.
- Numbers in text should be english words ("four common mistakes" not "4 common mistakes") unless there are units (40km, not forty km)
- Use Oxford commas ("a, b, and c" not "a, b and c")
- Functions in text should have parentheses (`read_csv()` not `read_csv`)
- Remove all references to "course" and "student"; replace with "reader" or "you" where necessary
- Remove all references to "clicking on things" in the HTML version of the book (e.g. "click this link to ...")
- Book titles in the text should be typeset in italics and then the reference (e.g. *R for Data Science* [thebibtexkey])

#### Code blocks

- Always use `|>` pipe, not `%>%`
- Do not end code blocks with `head(dataframe)`; just use `dataframe` to print
- `set.seed` once at the beginning of each chapter
- Use `"double quotes"` for strings, not `'single quotes'`
- Make sure all lines of code are at most 80 characters (for LaTeX PDF output typesetting)
- Pass code blocks through `styler` (although must obey the 80ch limit)

#### Section headings

- All (sub)section headings should be sentence case ("Loading a tabular data set", not "Loading a Tabular Data Set")
- Make sure that subsections occur in 1-step hierarchies (no subsubsection directly below subsection, for example)

#### Learning objectives

- When saying that students will do things in code, always say "in R"
- "you will be able to" (not "students will be able to", "the reader will be able to")

#### Captions

- Captions should be sentence formatted and end with a period

#### Equations

- Make sure all equations get capitalized labels ("Equation \\@ref(blah)", not "equation below" or "equation above")

#### Figures

- Make sure all figures get (capitalized) labels ("Figure \\@ref(blah)", not "figure below" or "figure above")
- Make sure all figures get captions
- Specify image widths of pngs and jpegs in terms of linewidth percent 
(e.g. `out.width="70%"`),
for plots we create in R use `fig.width` and `fig.height`.
- Center align all images via `fig.align = "center"`

#### Tables

- Make sure all tables get capitalized labels ("Table \\@ref(blah)", not "table below" or "table above")
- Make sure all tables get captions
- Make sure the row + column spacing is reasonable
- Do not put links in table captions, it breaks pdf rendering
- Do not put underscores in table captions, it breaks pdf rendering

#### Note boxes

- Note boxes should be typeset as quote boxes using `>` and start with **Note:**

#### Bibliography

- Do not put "et al" or "and others"; always use the full list of authors, BibTeX will choose how to abbreviate
- Read https://trevorcampbell.me/html/bibtex.html and make sure our bib follows this convention

#### Naming conventions

- K-means (not $K$-\*, K means, Kmeans)
- K-nearest neighbors (not $K$-\*, K nearest neighbors, K nearest neighbor, use US spelling neighbor not neighbour). Note that "K-nearest neighbor" is not the singular form; "K-nearest neighbors" is
- K-NN (not $K$-\*, KNN, K NN, $K$NN, K-nn)
- Local repository (not local computer)
- Package (not library, meta package, meta-package)
- data science (not Data Science)
- dataframe (not data frame)
- dataset (not data set)
- scatterplot (not scatter plot)
- bar plot (not bar chart)
- Capitalize all initialisms and acronyms (URL not url, API not api, K-NN not k-nn)
- Response variable (not target, output, label)
- Predictor variable (not explanatory, feature)
- Numerical variable (not quantitative variable)
- Categorical variable (not class variable)

#### Punctuation

- emdashes should have no surrounding spaces. `This kind of typesetting&mdash;which is awesome&mdash;is correct!` and `Typesetting with spaces around em-dashes &mdash; which is bad &mdash; is not correct`
- make sure `\index` commands don't break punctuation spacing. E.g. `This is an item \index{item}; it is good` will typeset with an erroneous space after item, i.e. `This is an item ; it is good`

#### Whitespace

- We need a line of whitespace before and after code fences (code surrounded by three backticks above and below). This is for readability, and it is essential for figure captions.

#### PDF Output

These are absolute last steps when rendering the PDF output:

- Look for and fix bad line breaks (e.g. with only one word on the next line, orphans, and widows)
- Look for and fix bad line wraps in code and text
- Look for and fix bad figure placement (falling off page, going over the side)
- Look for and fix large whitespace sections where LaTeX doesn't want to break the next paragraph (usually `\allowdisplaybreaks` helps)
- Fix incorrect indenting. LaTeX will indent for a new paragraph if there is an extra whitespace line, so these should be deleted if no paragraph break is desired.
- Look for `??` in the PDF (broken refs)
- Look in the index for near-duplicates, and merge if needed
- Look for / fix raw LaTeX code (search for backslash and curly brace in the final PDF)
- Make sure the 3D figures (and the text around them that refers to clicking and dragging) are properly modified for the PDF output
- Make sure all markdown label-replaced URLs (of the form `[blah](url)`) will make 
  sense in the hardcopy book version (i.e. nothing like "click this"). Many links appear in the additional resources: make sure the 
  text-replacement of the URL contains enough information for someone to find the resource (without being able to click the link)

#### HTML Output

- Look for broken references 
- Look for uncentered images


## Repository Organization / Important Files

- The files `index.Rmd` and `##-name.Rmd` are [R-markdown](https://rmarkdown.rstudio.com/) chapter contents to be parsed by [Bookdown](https://bookdown.org/)
- `_bookdown.yml` sets the output directory (`docs/`) and default chapter name
- `img/` contains custom images to be used in the text; note this is not all of the images as some are generated by R code when compiling
- `data/` stores datasets processed during compile
- `docs/.nojekyll` tells github's static site builder not to run [Jekyll](https://jekyllrb.com/). This avoids Jekyll deleting the folder `docs/_main_files` (as it starts with an underscore)


