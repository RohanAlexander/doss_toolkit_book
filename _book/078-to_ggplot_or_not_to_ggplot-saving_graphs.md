


# Saving graphs

*Written by Yena Joo.*


## Introduction
There are some situations where you may need pictures of the plots when writing on blogs or sending emails about the data you're analyzing. In that case, you would wonder how to save and upload the plots created in R.  

In this lesson, you will learn how to:  

- save graphs  
- change graph sizes  

Prerequisite skills include:  

- You should know how to create graphs using `plot()` or `ggplot()`  
- You should know the formats of the image (such as png, jpeg, pdf)  

Highlights:  

- jpeg, png, pdf  
- `ggsave()`  
- `unlink()`  


## Saving Graphs 

### Save as Jpeg image
Set the file name for the plot you are going to save using the function `jpeg(file = filename.jpeg)`, if you want to save as jpeg image. 
We need to call the function `dev.off()` after plotting, which will return control to the screen.  

```r
jpeg(file="plot1.jpeg")
ggplot(data = mtcars, aes(x=wt, y=mpg, color= wt)) + geom_point()
dev.off()
```


### Save as png image
We can set the resolution we want using the `width` and `height` arguments.
We can also set the full local path of the file we want to save if we don’t want to save it in the current directory.  

You can save the file as png image by using the function `png(file = "filepath/filename.png")`. 

```r
png(file = "plot2.png", width = 500, height = 300)
ggplot(data = mtcars, aes(mpg, wt)) + geom_point()
dev.off()
```

### Save as pdf file

To save a plot as pdf format, we do the following using `pdf(file = 'filename.pdf')`. 

```r
pdf(file = "plot3.pdf", eval = FALSE)
ggplot(data = mtcars, aes(mpg, wt)) + geom_point()
dev.off()
```


### Delete the saved image/file
What if we want to delete the file from the directory? We can delete the file using the function `base::unlink('FILE NAME')`. 

```r
unlink("plot3.pdf")
```

### `ggsave()`

Instead of using dev.off(), there is another function we can use to save the created plots. We use `ggsave()` to the ggplots.  

`ggsave()` includes the following arguments:  
```
ggsave(filename, plot = last_plot(), device = NULL, path = NULL, scale = 1, width = NA, height = NA, units = c("in", "cm", "mm"), dpi = 300, limitsize = TRUE, ...)
```   
And these are some core arguments:  

- `filename`: file name of the graph you are going to save.  
- `plot`: By default, the plot to save is the last plot displayed on your R file.  
- path: path of the directory to save the plot. By default, it is directed to the working directory.  
- `width`, `height`, `units`: You can set the width and height, as well as the units of those measurements.  

Here are some examples. Make sure put the correct format of the file after the file name as follows: 

```r
ggplot(data = mtcars, aes(mpg, wt)) + geom_point()
ggsave("plot4.pdf")
ggsave("plot4.png")
ggsave("plot4.jpeg")
ggsave("mtcars.pdf", width = 20, height = 20, units = "cm")
```

If you would like to delete the file, you can use the same `unlink()` function.  

## Exercises

### Question 1
Modify this code so you can save the following scatter plot into 10 x 10 cm graph in jpeg format, using `ggsave`. The file name should be `answer1`. 

```r
ggplot(data = mtcars, aes(mpg, wt)) + geom_point()
```

<img src="078-to_ggplot_or_not_to_ggplot-saving_graphs_files/figure-html/q1_save-1.png" width="672" />


```r
ggplot(data = mtcars, aes(mpg, wt)) + geom_point()
```

<img src="078-to_ggplot_or_not_to_ggplot-saving_graphs_files/figure-html/q1_save-solution-1.png" width="672" />

```r
ggsave("answer1.jpeg", width = 10, height = 10, units = "cm")
```

### Question 2
Now, delete the file using `unlink`. 



```r
unlink("answer1.jpeg")
```


### Question 3
Now, using `dev.off()`, save the following plot as pdf. The name of the file should be ```iloveplot.pdf```. 

```r
ggplot(data = mtcars, aes(x=wt, y=mpg, color= wt)) + geom_point()
```

<img src="078-to_ggplot_or_not_to_ggplot-saving_graphs_files/figure-html/q3_save-1.png" width="672" />


```r
jpeg(file="iloveplot.pdf")
ggplot(data = mtcars, aes(x=wt, y=mpg, color= wt)) + geom_point()
dev.off()
#> quartz_off_screen 
#>                 2
```


## Next Steps

### Common Mistakes & Errors
- Be careful when you set the local file path. 


### Next Steps
- You can use the saved graph in your documents such as word, pptx, or even post the pictures online.  

## References  

- [How to save a ggplot](https://ggplot2.tidyverse.org/reference/ggsave.html)
- [more information on ggsave()](https://ggplot2.tidyverse.org/reference/ggsave.html)



















