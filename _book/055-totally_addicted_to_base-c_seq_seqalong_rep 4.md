



# c, seq, seq along, and rep

*Written by Matthew Wankiewicz.*


## Introduction

In this lesson, you will learn how to:

- Learn how to make vectors/lists using `c()`.
- Create sequences using the `seq()` and `seq_along()` functions.
- Replicate values in a vector using `rep()`.

Prerequisite skills include:

- General knowledge of using vectors in R.

Highlights:

- `c()` is useful for making vectors quickly.
- `seq()` can help create sequences of numbers.
- `seq_along()` can give you the position of a value in a vector.
- `rep()` can create a vector with a repeated value.

## The content

As you continue using to use R, you will find that making vectors will be something you use a lot. The `c()` function is amazing tool to help us create vectors. The `c()` function can make vectors from sets of numbers, letters, or both!

Sometimes, you may find that you want to create different sequences of numbers, either for categorizing variables or just getting a list of random numbers. The `seq()` function is one of the best ways to achieve this. The `seq()` function gives us a list of numbers usually from 1 to the number you choose. You can also decide if the function skips numbers.

The `seq_along()` function is useful for finding the index position of parts of a vector. Sometimes, you will have a vector will different values, and `seq_along()` is useful for finding which position the value is in.

Another thing you may attempt to do in R is repeat values. Often times, you will repeat values when you want to make an "empty" vector which will store the results of simulations. The `rep()` function allows us to repeat strings or numbers a certain amount of times, which we can then save as a vector.

## Arguments

- **`c()`:** The `c()` function takes one main argument and includes optional arguments. The main argument for `c()` are the values that you want to save as a vector. The arguments used can be any set of numbers or words, or both. For example we would use an entry could be: `test <- c("This", "is", "example", 1)`.

- **`seq()`:** The `seq()` function can take 1 to 3 entries, depending on how specific you want your set of numbers to be. If you want a list of numbers from 1 to any number, you can simply use `seq(n)` where n is the number you want to stop at (if you do `seq(2)`, it will return the numbers 1 and 2.). If you want to specify where to start or stop, you can use the arguments `from =` and `to =`, which tells R where it should start and end. Lastly, if you want to change the increment of your sequence, you can use the `by =` argument.

- **`seq_along():`** The `seq_along()` function takes one argument. The argument it takes is a vector for which it will give the index position of a data point. For example, if we use the `test` vector from the `c()` example above, the output of `seq_along(test)` would be 1 2 3 4.

- **`rep()`:** The `rep()` function takes two main arguments. The first argument is `x =`, or the vector/value you plan to repeat. The second argument is `times =`, the number of times you want to repeat the vector (if you don't enter a value it defaults to 1). If we use our `test` variable with the `rep()` function, we can repeat the values of the vector as many times as we want.

## Other Optional Arguments

- **`c()`:** The optional arguments for `c()` are `recursive =` and `use.names =`. The recursive function is useful when the items you are vectoring includes a list. If you set `recursive = TRUE` it breaks down the list and converts it into a vector. If `recursive = FALSE` the vector is saved as a list (by default, `recursive = FALSE`, and it usually stays that way). The argument `use.names =` tells R whether or not to keep the names of the lists present when the vector is saved.

- **`seq()`:** The optional arguments for `seq()` are `length.out` and `along.with`. `length.out` tells R how many numbers you want to be present in the sequence of numbers. For example, if you set `length.out = 3` R will return 3 numbers, split up in even increments. `along.with =` is similar to length out, it takes a vector and returns the same amount of numbers as the length of that vector. If `along.with = 1:3`, it will return 3 numbers, split up in equal increments.

- **`rep()`:** The optional argument for `rep()` are `length.out` and `each`. `length.out` tells R how long it wants the output vector to be, similar to the main argument `times`. `each` only applies when you plan to repeat a vector. `each()` tells R how many times the first element of the vector should be repeated before it moves on to repeating the second element.

## Questions and Exercises

### `c()`

**1.**

<!-- ```{r q1cFunction, echo=F} -->
<!-- question_checkbox( -->
<!--   "What does the c() function do? (Select all that apply)", -->
<!--   answer("Creates a vector", correct = TRUE), -->
<!--   answer("Plots a graph", message = "Incorrect"), -->
<!--   answer("Repeats a certain value", message = "Incorrect."), -->
<!--   answer("Returns a sequence of numbers", message = "Incorrect."), -->
<!--   allow_retry = T, -->
<!--   random_answer_order = T -->
<!-- ) -->
<!-- ``` -->

**2. Using the `c()` function, save a vector with the numbers 21, 31, and 42 in it. (Add the c() function beside the arrow.)**

<!-- ```{r q2cFunction, exercise = TRUE} -->
<!-- ## Enter code below -->

<!-- vector <-  -->
<!-- vector -->
<!-- ``` -->

<!-- ```{r q2cFunction-solution} -->

<!-- vector <- c(21, 31, 42) -->
<!-- vector -->
<!-- ``` -->

The `c()` function can save numbers but can also save words with numbers, try it out in the next exercise.

**3. Save a vector with the numbers 21 and 31 along with the words "Statistics" and "Data"**

<!-- ```{r q3cFunction, exercise = TRUE} -->
<!-- ## Enter code below -->

<!-- vector <-  -->
<!-- vector -->
<!-- ``` -->

<!-- ```{r q3cFunction-solution} -->

<!-- vector <- c(21, 31, "Statistics", "Data") -->
<!-- ``` -->

### `seq()`

**1. Using the seq() function, return the sequence of numbers starting at 2 and ending at 20, increasing by 2's**

<!-- ```{r q1seqFunc, exercise = TRUE} -->
<!-- ## Enter code below -->


<!-- ``` -->

<!-- ```{r q1seqFunc-solution} -->

<!-- seq(from = 2, to = 20, by = 2) -->
<!-- ``` -->

**2.**

<!-- ```{r q2seqFunc, echo=F} -->
<!-- question_checkbox( -->
<!--   "Which functions only returns a sequence of numbers? (Select all that apply.)", -->
<!--   answer("seq()", correct = TRUE), -->
<!--   answer("seq_along()", correct = TRUE), -->
<!--   answer("c()", message = "Incorrect."), -->
<!--   answer("rep()", message = "Although rep() does repeat values, it can repeat values that are not numbers."), -->
<!--   allow_retry = T, -->
<!--   random_answer_order = T -->
<!-- ) -->
<!-- ``` -->

**3. Using the `length.out` argument in the `seq()` function, return the sequence of FOUR numbers starting at 25 and ending at 100.**


<!-- ```{r q3seqFunc, exercise = TRUE} -->
<!-- ## Enter code below -->

<!-- ``` -->

<!-- ```{r q3seqFunc-solution} -->
<!-- seq(from = 25, to = 100, length.out = 4) -->
<!-- ``` -->


### `seq_along()`

**You can use the `seq_along()` function to find the index position of elements in a vector, run the code chunk below to see how it works**

<!-- ```{r seq-alongExample1, exercise = TRUE} -->
<!-- vector <- c("dog", "cat", "fish", "cow") -->
<!-- vector -->
<!-- seq_along(vector) -->
<!-- ``` -->


**1. Now, create a vector containing the words "stats", "science", "math", "R" and use the `seq_along()` function to find the index positions of each word.**

<!-- ```{r seq-alongExercise1, exercise = TRUE} -->
<!-- vector <- c("stats") -->
<!-- seq_along(vector) -->
<!-- ``` -->

<!-- ```{r seq-alongExercise1-solution} -->
<!-- vector <- c("stats", "science", "math", "R") -->
<!-- seq_along(vector) -->
<!-- ``` -->

### `rep()`

**1. Using the `rep()` function, repeat the word "dog" 7 times.**

<!-- ```{r q1repFunc, exercise = TRUE} -->
<!-- ## Enter code below -->


<!-- ``` -->

<!-- ```{r q1repFunc-solution} -->

<!-- rep(x = "dog", times = 7)  -->

<!-- ## OR -->

<!-- rep("dog", 7) -->
<!-- ``` -->

**2. Save a vector with the words: "University", "of", and "Toronto". Once that vector is saved, use the `each` argument in the `rep()` function and repeat each word 3 times.**


<!-- ```{r q2repFunc, exercise = TRUE} -->
<!-- ## Enter code below -->
<!-- vector <- c("College", "and", "school") -->

<!-- ``` -->

<!-- ```{r q2repFunc-solution} -->

<!-- vector <- c("University", "of", "Toronto") -->
<!-- rep(x = vector, each = 3) -->
<!-- ``` -->

## Common mistakes & errors

Here are some common errors that can occur for each of the functions discussed in this section:


**`c()`:**

- Error: object 'string' not found
This means that R thinks you're trying to save an existing vector under the name 'string' (will likely be different). To fix this, add quotations marks around the word that R is having an issue with. If that doesn't work, there may be a typo.

**`seq()`:**

- Some functions in R can work without specifically defining arguments (`ggplot(aes(x, y))` is the same as `ggplot(aes(x = x, y = y))`). The `seq()` function needs each argument to be written out if you plan to use more arguments than `from` and `to`.

**`seq_along()`**

- Error: object 'string' not found
In this case, it means that the vector that R is trying to find does not exist. This likely means that there was a typo.

**`rep()`**

- Error: object 'string' not found
As mentioned above, R does not recognize an object entered into the function. You likely have a typo or you should put quotation marks around the string you want to repeat.

## Next steps

Some next steps include:

- Looking at more examples of `rep()` and `seq()` in action: https://bookdown.org/ndphillips/YaRrr/vectors.html

- R4DS's explanation of using iteration (include the `seq_along()` function): https://r4ds.had.co.nz/iteration.html


