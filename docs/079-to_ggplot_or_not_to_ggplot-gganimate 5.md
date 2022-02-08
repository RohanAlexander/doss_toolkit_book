


# gganimate

*Written by Matthew Wankiewicz and last updated on 7 October 2021.*





## The content

In this lesson you will learn how to:

- Create animated plots with the `gganimate` package

Some pre-requisites include:

- Having `ggplot2` and `gganimate` installed and loaded
- Previous use of the `ggplot2` package
- You may also need to install the `gifski` package to load animations.

Highlights:

- Using `gganimate` is another way to display your data.
- The package's functions can only be used on HTML documents or can be saved and posted, perfect for websites or social media.
- A cheat sheet for the package can be found [here.](https://ugoproto.github.io/ugo_r_doc/pdf/gganimate.pdf)


The `gganimate` package is an extension of the `ggplot2` package which allows you to make your ggplots animated. The animations contained in this package allow you to show trends in data over a period of time or depending on certain states. This can be a useful way to keep readers engaged with your data or can be used if you want to share the trends you find on places like twitter.

Before using `gganimate`, you'll have to have a graph set up using `ggplot2`, once you have the graph you can move on to animating it. 

The package can be installed from CRAN using `install.packages("gganimate")`.

## Functions

### `transition_*()`:

The transition functions are the most important functions in the package. The functions are what make the plots animated. There are 8 total `transition_*` functions, 4 will be shown below.

- **`transition_states`:** This function animates graphs based on a certain column in your data. The plot will move based on the different levels in the column. For example, if you have a column with different species of animals, the plot will move/change for each type of animal present in the column. 
  - **states:** States is the column you want to move the plot by.
  - **transition_length:** This argument changes the length of the transition between the states.
  - **state_length:** This argument changes how long each state is present for.
  - **wrap:** This determines if the animation loops or not. It is set to TRUE by default.

Below is an example of the `transition_states` function:

```r
broadway <- read_csv("https://raw.githubusercontent.com/tacookson/data/master/broadway-grosses/grosses.csv")

broadway_plot <- broadway %>% 
  ggplot(aes(weekly_gross)) + 
  geom_histogram(bins = 15)

broadway_plot + transition_states(transition_length = 1,
                                  states = theatre, 
                                  state_length = 1)
```

<img src="079-to_ggplot_or_not_to_ggplot-gganimate_files/figure-html/gganimate-transition-states-example-1.gif" width="75%" />

The plot above shows the distribution of weekly gross ticket sales for theatres on broadway. Each state on the plot is a different theatre.


- **`transition_time`:** This function is the same as `transition_states` but uses time to animate instead of variables. This function is very useful for showing trends over time.
  - **time**: Time is the only required argument for this function. It represents the time separating each observation in the plot, this can include Days, Weeks or Years.
  - **range**: Range is an optional argument, this represents the range of time you would like to show on the animation. For example, you could look at a certain span of years.

- **`transition_reveal`:** A variant of `transition_time`. This function is different from `transition_time` because of the way it interprets data for plotting. Instead of strictly going by time values, the function aims for smoother transitions compared to `transition_time`. Overall, the function will reveal each frame over time. This can be useful for plotting `geom_path` objects as it will be able to make the line grow over time, like someone is drawing it. 
  - **along**: The most important argument for this function. It represents the variable you want R to display state by state. For example, if you set `along = Year`, the function will display a new state on the graph for each year in the data.
  - **range**: This argument is optional, it allows you to set a range of time for your animation.
  - **keep_last**: Determines if the last row will show up for future frames. It is set to TRUE by default and doesn't really need to be changed.
  
- **`transition_filter`:** Instead of having new stages based on different levels of a variable or by periods of time, `transition_filter` shows different states based off of the `filter` function. 
  - **transition_length:** This argument changes the length of the transition between the states.
  - **filter_length:** This argument changes how long each filter state is present for.
  - You will also need to add filter expressions. You can place as many expressions as you want, these will become the states of your animation. Write them in the form `x < y`, `var == "dog"`, you don't need to include the filter function.
  - **wrap:** This determines if the animation loops or not. Set to TRUE by default.
  - **keep:** Tells R if you want to keep rows that don't match the filter in your data. The main use of this argument is with "exit functions" and how they operate. Exit functions will be discussed later.
  
Some other transition functions include `transition_null`, `transition_manual`, `transition_components` and `transition_layers`. These functions aren't used as much as the other 4 shown, more information about the functions can be found in the [`gganimate` documentation.](https://cran.r-project.org/web/packages/gganimate/gganimate.pdf)

### More Aesthetic Functions

Along with the transition functions, there are other `gganimate` functions which can help your animations look better. There are two types of functions which can help your animations: Enter/Exit functions and the ease function. 

The Enter/Exit Function determine how the data for each state will enter the graph. Instead of having the points on a graph appear/disappear, these functions will add more interesting transitions, like shrinking/growing or fading in/out. The `gganimate` website gives some helpful information about these functions and can be found [here.](https://gganimate.com/reference/enter_exit.html)

The `ease_aes` function changes how the animation moves between its states on the plot. There are many different types of easing that can be applied onto animations, each having a different effect. A list of easing types and a visual demonstration of how they affect the animation can be found on the [R bloggers site.](https://www.r-bloggers.com/2021/01/ease_aes-demo/)

Another function that can be used with `gganimate` is `ggtitle`. Using this function allows us to have a title which changes with each state of the graph. For example, if we have a histogram showing the distribution of ages by country, we can use `ggtitle` to change the title depending on which country it is showing. 

- To have the title change by state for `transition_states` write your title followed by "{closest_state}".
- To have the title change for `transition_reveal` use "{frame_along}" after your title.
- To have the title change for `transition_filter` use "{closest_filter}" after the title.
- To have the title change for `transition_time` use "{frame_time}" after the title.

### `animate`

The `animate` function is used to render the animations created. In these renderings you can change the image quality, number of frames, frames per second and many other options. The most important arguments of `animate` will be discussed below:

- **plot:** The plot argument is simply your plot. This can be the entire plot expression, or you can save the expression as an object use that. 
- **nframes:** This is the number of frames in your animation. It is set to 100 by default but you can change it to match the number of states there are in your plot.
- **fps:** This is the frames per second. If you want your animation to be really slow, lower the frames per second. This argument defaults to 10. 
- **duration:** This is how long you want your animation to be.
- **device:** This argument changes how the images are stored for the animation. By default they are saved as .png.

## Common Errors

- Error: Provided file does not exist. 
  - This means that you are using a keyword that does not match the transition function. To fix this, you need to change to a different keyword. 
  - `transition_states` matches with "{closest_state}", `transtion_reveal` matches with "{frame_along}", `transition_filter` matches with "{closest_filter}" and `transition_time` uses "{frame_time}".
  
- Error: transition_filter requires at least 2 filtering conditions
  - Make sure you have 2 filtering conditions defined.
  - If you have 2 filtering conditions already, you will need to add the `transition_length` and `filter_length` arguments to your function.
  
- Error in transform_path(all_frames, next_state, ease, params$transition_length[i],  : 
  transformr is required to tween paths and lines
  - To fix this, install the `transformr` package.


## Test your Understanding

The next three questions will use the code chunk below:

```r
caribou_timeplot <- caribou %>% 
  filter(animal_id == "GR_C01") %>% 
  filter(event_id < 2259197491) %>% 
  ggplot(aes(longitude, latitude)) +
  geom_path() +
  ggtitle("Timestamp: {****}")

caribou_timeplot + transition_*(timestamp)
```


<!-- ```{r multiple-choice-gganimate-q1, echo=FALSE} -->
<!-- question("What type of animation will we have if `transition_time` is used?", -->
<!--          answer("A line showing the coordinates of the caribou over time."), -->
<!--          answer("Single lines drawn for each moment in time (not continuous)", correct = T), -->
<!--          answer("No plot will occur"), -->
<!--          answer("A scatter plot showing the coordinates, changing over time"),  -->
<!--          random_answer_order = T,  -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r gganimate-question-2, echo=FALSE} -->
<!-- question("If we want to have a continuous line be drawn, which transition function should we use?", -->
<!--          answer("`transition_states`"), -->
<!--          answer("`transition_time`",  -->
<!--                 message = "`transition_time` would not have a continous line for this plot."), -->
<!--          answer("`transition_reveal`", correct = T), -->
<!--          answer("Another transition function"),  -->
<!--          random_answer_order = T,  -->
<!--          allow_retry = T) -->
<!-- ``` -->

<!-- ```{r gganimate-question-3, echo=FALSE} -->
<!-- question("Which `ggtitle` keyword should we use if we want a continuous 'drawn' line for our plot?", -->
<!--          answer("{closest_state}"), -->
<!--          answer("{frame_along}", correct = TRUE), -->
<!--          answer("{closest_filter}"), -->
<!--          answer("{frame_time}"), -->
<!--          allow_retry = TRUE,  -->
<!--          random_answer_order = TRUE) -->
<!-- ``` -->



<!-- ```{r gganimate-q4-sorting, echo=FALSE} -->
<!-- order <- c("Find a dataset", "Create a ggplot plot",  -->
<!--            "Use one of the transition functions to animate the plot",  -->
<!--            "Use an Enter/Exit/easing function to make your plot fancier (optional)",  -->
<!--            "Render and save the plot using `animate`") -->
<!-- question_rank("What is the proper order for using `gganimate`?", -->
<!--               answer(order, correct = T), -->
<!--               answer(rev(order)),  -->
<!--               answer(c("Find a dataset", "Create a ggplot plot", -->
<!--                        "Render and save the plot using `animate`", -->
<!--                        "Use one of the transition functions to animate the plot",  -->
<!--                        "Use an Enter/Exit/easing function to make your plot fancier (optional)")), -->
<!--               answer(c("Find a dataset", "Create a ggplot plot", -->
<!--                        "Use an Enter/Exit/easing function to make your plot fancier (optional)", -->
<!--                        "Use one of the transition functions to animate the plot",  -->
<!--                        "Render and save the plot using `animate`")), -->
<!--               random_answer_order = T, allow_retry = T) -->
<!-- ``` -->

<!-- ```{r gganimate-question-5, echo=FALSE} -->
<!-- question("When you get an error saying 'transformr is required to tween paths and lines', what should you do?", -->
<!--          answer("install the `transformr` package", correct = T),  -->
<!--          answer("use a different function"),  -->
<!--          answer("re-install `gganimate`"),  -->
<!--          answer("restart your R session"),  -->
<!--          allow_retry = T,  -->
<!--          random_answer_order = T) -->
<!-- ``` -->

<!-- ```{r gganimate-question-6, echo=FALSE} -->
<!-- question("If you get an 'Object Not Found' error, what is likely the issue and how do you fix it?", -->
<!--          answer("You are referencing a plot that doesn't exist, make sure you don't have any typos", -->
<!--                 correct = T), -->
<!--          answer("`gganimate` is not loaded. Use `library('gganimate')` to fix the issue"), -->
<!--          answer("`gganimate` is not installed. Use `install.packages('gganimate')` to fix the issue"),  -->
<!--          answer("You are referencing a function that doesn't exist, make sure you are using the right function"), -->
<!--          allow_retry = T,  -->
<!--          random_answer_order = T) -->
<!-- ``` -->

<!-- ```{r gganimate-question-7, echo=FALSE} -->
<!-- question("How do you fix the 'Provided file does not exist' error?", -->
<!--          answer("Re-run the function"), -->
<!--          answer("Use `labs` instead of `ggtitle`"), -->
<!--          answer("Change the keyword used in `ggtitle`", correct = TRUE), -->
<!--          answer("Re-install `gganimate` and `tidyverse`"), -->
<!--          allow_retry = TRUE,  -->
<!--          random_answer_order = TRUE) -->
<!-- ``` -->

<!-- Modify the code below to add a title that changes depending on the `Cyl`. (Hint: Check which transition function is being used.) -->
<!-- ```{r gganimate-question-8, exercise = TRUE} -->
<!-- cars_plot <- mtcars %>%  -->
<!--   ggplot(aes(mpg)) + -->
<!--   geom_histogram(bins = 5) -->

<!-- cars_plot + transition_states(cyl) -->
<!-- ``` -->

<!-- ```{r gganimate-question-8-solution} -->
<!-- cars_plot <- mtcars %>%  -->
<!--   ggplot(aes(mpg)) + -->
<!--   geom_histogram(bins = 5) + -->
<!--   ggtitle("Cyl: {closest_state}") -->

<!-- cars_plot + transition_states(cyl) -->
<!-- ``` -->

<!-- Modify the code below to display different states based on a filter. Filter for `mpg > 20`, `gear == 3` and `carb <= 5`. Also, set the transition length to 2 and the filter length to 3. -->
<!-- ```{r gganimate-question-9, exercise = TRUE} -->
<!-- cars_plot <- mtcars %>%  -->
<!--   ggplot(aes(disp, qsec)) + -->
<!--   geom_point() + -->
<!--   ggtitle("Filter: {closest_filter}") -->

<!-- cars_plot +  -->
<!-- ``` -->

<!-- ```{r gganimate-question-9-solution} -->
<!-- cars_plot <- mtcars %>%  -->
<!--   ggplot(aes(disp, qsec)) + -->
<!--   geom_point() + -->
<!--   ggtitle("Filter: {closest_filter}") -->

<!-- cars_plot + transition_filter(transition_length = 2, -->
<!--                               filter_length = 3,  -->
<!--                               mpg > 20, gear == 3, carb <= 5) -->
<!-- ``` -->


The final question will use the plot below:

<img src="079-to_ggplot_or_not_to_ggplot-gganimate_files/figure-html/gganimate-example-plot-q10-1.gif" width="75%" />


<!-- ```{r gganimate-question-10, echo=FALSE} -->
<!-- question("Which code chunk was used to create the plot above?",  -->
<!--          answer("ex_plot <- expeditions %>%  -->
<!--   ggplot(aes(highpoint_metres, members)) + -->
<!--   geom_point() + -->
<!--   ggtitle('Season: {closest_state}') -->

<!-- ex_plot + transition_states(season)", correct = TRUE),  -->
<!--       answer("ex_plot <- expeditions %>%  -->
<!--   ggplot(aes(highpoint_metres, members)) + -->
<!--   geom_point() + -->
<!--   labs(title = 'Season') -->

<!-- ex_plot + transition_states(season)", message = "Hint: look at the title."), -->
<!--       answer("ex_plot <- expeditions %>%  -->
<!--   ggplot(aes(highpoint_metres, members)) + -->
<!--   geom_point() + -->
<!--   ggtitle('Season: {closest_state}') -->

<!-- ex_plot + transition_time(season)"),  -->
<!-- answer("ex_plot <- expeditions %>%  -->
<!--   ggplot(aes(highpoint_metres, members)) + -->
<!--   geom_point() + -->
<!--   ggtitle('Season: {closest_state}') -->

<!-- ex_plot + transition_filter(season)"), -->
<!-- allow_retry = T, random_answer_order = T) -->
<!-- ``` -->



## Helpful Links

Some helpful links include:

- The `gganimate` website: https://gganimate.com/

- Katherine Goode's presentation on `gganimate`: https://goodekat.github.io/presentations/2019-isugg-gganimate-spooky/slides.html#1

- The rOpenSci Labs github page for learning `gganimate`: https://github.com/ropensci-archive/learngganimate


## Questions

1. True or False, `gganimate` plots will work if the output file is a PDF?
  a. True
  b.  False
  
2. True or False, `gganimate` is part of the `ggplot2` package?
  a. True
  b.  False
  
3. If I want my `gganimate` plot to loop, which argument should I use?
  a. `loop = TRUE`
  b. `repeat = TRUE`
  c.  `wrap = TRUE`
  d. That argument does not exist
  
4. Which function is best suited to animate an line that changes over time (like yearly population totals)?
  a. `transition_states()`
  b.  `transition_time()`
  c. `geom_point()`
  d. `transition_line()`
  
5. What is the `render` function used for?
  a.  Render animations that were created
  b. Change the scales of the plot
  c. Make the plot static
  d. None of the above
  
6. If I want to make a moving plot that changes depending on a categorical variable, which function should be used?
  a.  `transition_states()`
  b. `transition_time()`
  c. `transition_reveal()`
  d. `transition_cat()`
  
7. What does the `ggtitle` function do?
  a. Creates a title that does not change
  b. Creates a new plot
  c.  Creates a title that changes depending on the state
  d. None of the above
  
8. If I am using `transition_filter`, which `ggtitle` call should I use?
  a.  "{closest_filter}"
  b. "{frame_time}"
  c. "{closest_state}"
  d. "{frame_along}"
  
9. What is the default file type for the `animate` function?
  a. gif
  b. jpg
  c. html
  d.  png
  
10. What do enter/exit functions do?
  a. Make the animation static
  b.  Change how the animation begins/ends
  c. Add more plots
  d. Add a title to the plots
  
  
  
  
  
  
  
