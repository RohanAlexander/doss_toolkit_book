


# Bar charts

*Written by Matthew Wankiewicz and last updated on 7 October 2021.*

## Introduction

In this lesson, you will learn how to:

- Plot bar charts using the `ggplot` package
- Customize bar charts with `ggplot`

Prerequisite skills include:

- Having `ggplot` installed and loaded
- Basic familiarity with `ggplot`

Highlights:

- Bar charts are the best way to display categorical data.
- The `ggplot` function allows you to customize your bar graphs.

## The content

When you encounter a dataset that does not include numerical data, the best way to visualize what you are working with is a bar chart. Generally, bar charts will have the categorical variable on the x-axis, and the count/percentage on the y-axis.

Bar charts are different from graphs like histograms because histograms display numerical variables while bar charts work best for categorical.

Bar charts are useful for getting a view of how your data looks and seeing which groups appear the most. 

## Arguments

The main arguments for making bar charts is part of the `ggplot` function:

- **data:** This represents the dataset you plan to use. You can either write `data = dataframe` or you can pipe the dataset into `ggplot`.
- **`aes():`** This is where you place the argument that decides which variable you are focusing on.
  - `x = variable:` This is the variable you want to display.
  - `fill = variable:` This can change the fill of your bar depending on the different options in your variable. 
- **`geom_bar():`** This is where you put any arguments to change the looks of your graph, whether it's colour or size of the bars.
  - **`fill:`** This argument decides the colour of the inside of the bars.
  - **`colour:`** This argument decides the colour of the outline of the bars.
- The `labs` function is useful for adding titles and subtitles to your graph.
  

## Other Optional Arguments

Some optional arguments for the `geom_bar()` function include:

  - **`width:`** This argument changes the width of the bars, it defaults at 0.9.
  - **`alpha:`** Changes the transparency of the bars.


## Questions

For this module, we will be using lemur data from Alex Cookson, https://github.com/tacookson/data/tree/master/duke-lemur-center.







































