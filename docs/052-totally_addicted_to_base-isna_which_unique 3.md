


# Investigating and playing with data

*Written by Uzair Mirza and last updated on February 6 2021.*

## Introduction

When working with real world datasets we will find them often times if not always as being messy. Hence before and while cleaning our datasets we would like to know if there are some **empty entries** or **occurrences of specific values** in our data, get to know all the **unique categories** in our data set and sometimes **compare two objects**. All this effort is done with the goal of reducing the bias and sources of error in our study to get accurate results.

Think about conducting an observational study and working with data from a survey. We will have cases where we would like to know if there were participants who chose not to answer our main question of interest, or to observe respondents from a specific age-group or gender and study their other replies. Perhaps we want to find people above or below a certain limit which might be considered outliers, or we might be interested in knowing all the unique income levels to which people belong in our study. We might also want to test if there are multiple entries by the same person which might be a cause of over representation in our data.

For the sake of this lesson, let us simulate a data frame that might look similar to that extracted from a survey. Usually, information extracted using Google Forms or other sources might be in form of CSV files or present at a specific URL.

Here, however, we will be skipping the step of conducting the survey, extracting, and reading the related file, and instead we will be replacing all these steps with generation of our own data using different simulation techniques.

Lastly, don't get intimidated or overwhelmed by the length of the lecture. All the topics have a bunch of examples, the intention is to make it easy for you to grasp the understanding of the material. Going over all the examples is not necessary **BUT** highly recommended.

## Let the lecture begin!!

### Required setup

For this lecture you are required to load in the package `tidyverse`. You can think of a package as a specific toolkit in your garage that contains all the tools that might be required for to perform the task.

**NOTE** if this is your first time and you don't have the package installed then you can uncomment the code(remove the hashtags) in the lines starting with `install.packages()` and run the code to install and then load the package.


```r
# loading necessary package
#install.packages("tidyverse")
library(tidyverse)

#install.packages("mice")
library(mice)
```

### Setting up our topic of study

Suppose we are conducting a study where we are trying to investigate how bone density varies in different groups and by different factors.

For this study we collected bone density and weight of 20 participants and asked them to identify and self-declare their age and gender.

So let us first simulate some data. Below is the code chunk to simulate the data.

You can go ahead and copy and paste the code below to follow along. Just like before, if you don't have the package then go ahead and uncomment the code line and first ` install.packages("mice")`. To play around and simulate another yet similar dataset you can change the number of the seed (ex:)for example, `set.seed(423)`). Furthermore, please note that for this lecture you are not required or expected to understand this code chunk.


```r
# setting seed
library(mice)
set.seed(1234)

# simulating data for 20 participants
n <- 20

# assigning ID to the participants
ID <- c(1:n)
## simulating data and creating the initial data frame
age <- rnorm(n, mean = 40, sd = 2) %>%
  round(digits = 0)

bone_density_cat <- c("normal", "low", "alarming")
bone_density <-
  as.factor(sample(
    bone_density_cat,
    size = n,
    replace = T,
    prob = c(.5, .3, .2)
  ))

weight <- rnorm(n, mean = 152.34, sd = 24.47) %>%
  round(digits = 2)

gender_cat <- c("male", "female", "non-binary")
gender <- as.factor(sample(gender_cat, size = n, replace = T))

data <- tibble(ID, age, bone_density, weight, gender)

# Simulating NAs in the data frame and extracting it
data_1 <- ampute(
  data,
  patterns = matrix(
    c(1, 0, 1, 1, 1,
      1, 1, 1, 1, 0,
      1, 0, 1, 1, 0),
    nrow = 3,
    byrow = TRUE
  ),
  freq = c(1 / 3, 1 / 3, 1 / 3),
  prop = 0.2,
  mech = "MAR"
)

## Data with NA introduced and categories restored
data_2 <- data_1$amp
data_2$bone_density[data_2$bone_density == 1] <- "alarming"
data_2$bone_density[data_2$bone_density == 2] <- "low"
data_2$bone_density[data_2$bone_density == 3] <- "normal"

data_2$gender[data_2$gender == 1] <- "female"
data_2$gender[data_2$gender == 2] <- "male"
data_2$gender[data_2$gender == 3] <- "non-binary"
data <- data_2
```

Let us now have a peek at the data frame.


```r
head(data)
#>   ID age bone_density weight     gender
#> 1  1  38          low 179.31       male
#> 2  2  41          low 140.70 non-binary
#> 3  3  NA       normal 134.98       <NA>
#> 4  4  35          low 140.07       male
#> 5  5  41       normal 112.48 non-binary
#> 6  6  41          low 123.77     female
```

Here is the description of all the variables in our data set;

1. ID (numeric variable)
    - ranging 1-20
2. Age (numeric variable)
    - ranging 35-45
3. Bone density (categorical variable)
    - normal
    - low
    - alarming
4. Weight (numeric variable)
    - ranging 98.99-187.81
5. Gender (categorical variable)
    - male
    - female
    - non-binary

Now, before diving in and starting the study we need to clean our data. This is done with the aim to minimize possible biases and errors in our data. Let us now look at some of the questions which may arise while cleaning and how we can solve them.

*As mentioned before, for each case we will be working with couple of examples (a mix of intuitive and course related) in hopes of better understanding and remembering the topic.*

### Dealing with empty entries: `is.na()`

When collecting data or when conducting study, we need to know if our data has some empty entries. In a survey these empty entries can arise when someone chooses not to respond to a certain question, in a study this can be because there was an error in the recording tool. So instead of discarding the entire observation we might choose to keep the observation with the empty entry. This is because in real studies collecting data is quite expensive and also the missed entry might not be significantly relevant to the study (i.e. name, residency-status, etc.).

When reading datasets, empty entries in R are treated and declared as `NA` which stands for **N**ot **A**vailable. To check against every entry OR a particular entry in the data frame is `NA` we use ` is.na()`.

#### Is this NA?

When we want to inquire about the above question, we use the `is.na()` function. In R this function ***takes in*** a value, vector, or data frame and ***returns*** for every value in the data frame ` TRUE` if it is ` NA` and ` FALSE` otherwise. So here note the return type can be either a vector or a matrix depending on the size and dimension of the input.

#### Examples

##### Example 1

Think of the case where you are receptionist of a hotel with five rooms, where hotel rooms are treated as a vector. Empty rooms are declared with NA and booked rooms are declared with the unique ID of the person who booked them.

Now imagine you get a call from a potential guest asking if there are any free rooms.

This is how you answer this question using `is.na()`.


```r
# Setting up our hotel rooms
rooms <- c(23, 12, 3, NA, 4)
# checking if we have empty rooms
is.na(rooms)
#> [1] FALSE FALSE FALSE  TRUE FALSE
```

This is what the result translates to; room 1,2,3,5 are booked and room 4 is empty. This is because as expected ` NA` in the fourth position results in `TRUE` in the fourth position, meaning room 4 is empty.

Furthermore, note as mentioned the size of the output is the same as the size of the input.

##### Example 2

Let us now get back to the bone density study and see what possible questions can be answered using the `is.na()` function.

Suppose we would like to know if bone density varies in different genders. First thing we would like to know is if there are any empty (`NA`) entries in the gender we recorded. This is how it is done:


```r
# getting all the recorded genders in the study
gender <- data$gender

# checking for gender
is.na(gender)
#>  [1] FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE
#> [10] FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE
#> [19] FALSE FALSE
```

As it might seem hard to read the result, let us now check for the count for the individual results for `TRUE` versus ` FALSE` in the result.


```r
# shows the unique count of occurrences
table(is.na(gender))
#> 
#> FALSE  TRUE 
#>    17     3
```

Based on the above results we can see that of all the participants there were three for which the response for gender was **N**ot **A**valible.

Now depending on our study's protocol we can either choose to remove those entries or assign a new category for the unreported category.

Before proceeding with the study and going to the next step we would want to know the position of these `NA` values. How to get the position and filter them out will be the next skill to study.


### Finding position of specific elements: `which()`

Often we would want to find the position of entries in our data based on certain conditions. Let's say you would like to know the effect of treatment for people of a certain age or a certain gender. Another possible case while data cleaning is (as discussed previously) further building up and refining data upon discovery of `NA`.

Cases like these require us to use ` which()` to locate the position of these entries.

#### Which ones are it?

Inquiring about questions related to identification and finding positions in the data frame, requires the use of the ` which()` function.

This function ***takes in*** a logical argument or a combination of logical arguments and ***returns*** the position of the entries which satisfy the passed logical argument.

#### Examples

##### Example 1

Getting back to our hotel example, let us look at two cases.

Let us say that one of the guests who had previously booked at our hotel has now arrived and would like to know their room number. Suppose they mention their ID is 23 (recall that rooms were booked against ID) this is how we would go about searching for their room number.


```r
# our hotel rooms
rooms <- c(23, 12, 3, NA, 4)

# checking the room number
## STEP1: declaring the required logical argument
argument <- rooms == 23

## STEP2: passing the argument
which(argument)
#> [1] 1
```

Based of this result we can let our guest know that room 1 is the room booked for them.

**Note in the previous code chunk we can combine step 1 and 2 and directly pass in the argument in the function; i.e. ` which(rooms == 23)`. The `argument` variable was used for the ease of understanding.**

Let us look at another related example which deals with a combination of the previously learned function ` is.na()`.

Imagine that we are faced with the question of which rooms are free (`NA`). This is how we will be answering this question.


```r
# checking empty rooms
which(is.na(rooms))
#> [1] 4
```

Based on this result we can see that the fourth room is free.

Let us dissect this case. Recall that ` is.na()` returns `TRUE` against all the entries which are `NA`s and ` which()` returns the position of the elements which pass the argument (i.e. elements in the argument that are `TRUE`, hence in this case we know that room 4 is empty).

##### Example 2

Getting back to our bone density study, let us look at what questions we can answer using this function.

Let's say we are interested and would like to know the participants who have normal levels of bone density. This is how we do this.


```r
# STEP1: declaring the logical argument
## looking for normal bone density
argument <- data$bone_density == "normal"

# STEP2: passing the argument getting the results
which(argument)
#> [1]  3  5  8  9 11 12 15 17 19
```

Based on the results we can see that participants 3, 5, 8, 9, 11, 12, 15, 17 and 19 had normal bone density, but for the sake of clarification let us also verify this in a form of a clean table.


```
#>   ID bone_density
#> 1  3       normal
#> 2  5       normal
#> 3  8       normal
#> 4  9       normal
#> 5 11       normal
#> 6 12       normal
#> 7 15       normal
#> 8 17       normal
#> 9 19       normal
```

Let us close this example with looking at a case combining `which()` with ` is.na()`.

Suppose, while cleaning the data and removing the ` NA` values we would like to know the other characteristics of the observations with any missing values. This is how we would go about solving this problem.


```r
# STEP1: Declare logical argument
## Checks are done against age and gender
argument <- is.na(data$gender) | is.na(data$age)

# STEP2: Get to positions of the cases which pass the argument
positions <- which(argument)

# STEP3: Filter the data based on the specified condition and get the results
data %>%
  filter(ID %in% positions)
#>   ID age bone_density weight     gender
#> 1  3  NA       normal 134.98       <NA>
#> 2  9  NA       normal 145.14       <NA>
#> 3 11  NA       normal 187.81 non-binary
#> 4 12  NA       normal 126.19       <NA>
#> 5 13  NA          low 131.41       male
```

Here, we only checked for `NA` in the categories of age and gender due to the study's assumption that we asked participants to self-report age and gender.

Overall, based on the results, we can see that we had five participants who choose not to report or had an error recording their age and of these five participants, three of them had similar issues with recording their gender.

#### Special cases and dealing with common errors

So far we have been dealing with cases where we were able to find the elements in the data frame satisfying the logical argument. Let us now look at the case for which entries satisfying the logical argument do not exist in the data frame and see what is returned.


```r
# STEP1: Declare logical arguments
## Check for an invalid ID
argument_1 <- data$ID == 34
## Check for an NA ID
argument_2 <- is.na(data$ID)
## Check for an invalid data type in weight
argument_3 <- data$weight == "Twinny One"
## Check for an invalid ID in age
argument_4 <- data$age == "Twinny 2"


# STEP2: Get to positions of the cases which passes the declared arguments
position_1 <- which(argument_1)
position_2 <- which(argument_2)
position_3 <- which(argument_3)
position_4 <- which(argument_4)

# STEP3: Get the result
position_1
#> integer(0)
position_2
#> integer(0)
position_3
#> integer(0)
position_4
#> integer(0)
```

Here in each case we can see that when elements satisfying the logical argument are not found and then the result is always ` integer(0)`.

Let us look at what this output means. Recall when we mentioned that the output of ` which()` is a vector of integers containing the positions of the occurrences satisfying the logical argument. So here ` integer(0)` is an **integer vector of length 0**; that is, it is an empty integer vector, which translates to mean that there are no values in our data set matching the specified logical argument.

Let us now close this topic with introduction of some common errors that we might encounter.

One common case occurs when we fail to input a logical argument, which means our current function fails to work and returns an error. Let us see what the output looks like.


```r
# STEP1: Declare logical arguments
argument_F <- 21
# STEP2: Test and find our argument
which(argument_F)
#> Error in which(argument_F): argument to 'which' is not logical
```

Here as expected we can see that our "logical" argument has an error and is not logical, hence the error message. Upon encountering this message, check the input of logical argument and make sure it is logical (i.e. upon processing returns either `TRUE` or `FALSE`).

Another case is when the input argument is logical but the returning values are out of bound of our data frame. Let us look at that example and what that means.


```r
# STEP1: Declaring logical
## Checking for Female in our data frame
argument_InVal <- data == "female"
# STEP2: Test the argument
which(argument_InVal)
#> [1]  86  94  95  98  99 100
```

Based on these results let us check which entry does one of these values correspond to.


```r
# Checking for 1 of the results, every input will have the same result
data[86, ]
#>    ID age bone_density weight gender
#> NA NA  NA         <NA>     NA   <NA>
```

Here we can see that there are no corresponding entries on the 86th row in our data set, which is expected as our data set had only 20 rows (20 IDs).

When we encounter this case, we can be sure about one thing: there are occurrences satisfying our declared argument, however to actually find them we need to go back and fix our declared argument.

Initially we were trying to check if every value in `data` equals female, instead we need to check in the right variable in our data frame.

Let us quickly fix that and see the results:


```r
# STEP1: Fix the declared logical argument
## Checking for Female under **gender** in our data frame
argument_Fix <- data$gender == "female"

# STEP2: Test the argument
which(argument_Fix)
#> [1]  6 14 15 18 19 20

# STEP3: Filter the data based on the specified condition and get the results
data %>%
  filter(ID %in% which(argument_Fix)) %>%
  select(ID, gender)
#>   ID gender
#> 1  6 female
#> 2 14 female
#> 3 15 female
#> 4 18 female
#> 5 19 female
#> 6 20 female
```

### Getting all the distinct entries `unique()`

Often we will encounter circumstances where we would like to know of all the unique entries or categories in our data frame. Furthermore, in certain cases a potential source of error might be duplicates in our data frame, in which case we would have to filter our data to get the unique occurrences. This is done using the `unique()` function.

#### Show me only the unique!

The ` unique()` function **takes in** a vector, matrix, or data frame and then **returns** a vector, matrix, or data frame containing only the unique entries. **NOTE** ` NA` as an entry in our data frame also counts as a unique entry. Let us now look at some of the examples to cement our ideas. \

#### Examples

##### Example 1

Let's say that details about hotel rooms (room size) are stored in a vector against their position, i.e. detail about room 2 is the second element in our vector, and details about room X will be on the $X^{th}$ position in our vector.

So now imagine a potential guest calls and wants to inquire about all the different rooms at our hotel, let us see how we can answer this question.


```r
# Declaring the room detail vector
room_size <- c(1, 2, 1, 3, 2)
# getting the unique options
unique(room_size)
#> [1] 1 2 3
```

Based in this we can inform them about the three possible options for room size; one, two, and three, person rooms are currently being offered at our hotel.

##### Example 2

Recall our bone density study, let's say we want to get an idea about the uniqueness of the age in our study. Let us see the steps involved in solving this problem:


```r
# Fetch the all the ages from our data frame
age <- data$age
# Get the all the unique ages
unique(age)
#> [1] 38 41 NA 35 39 40 42 45
```

Based on the result we can see that there are eight unique ages, including one `NA` value.
Let us continue to build on this example and incorporate some of our previously learned skills.

Although we can easily spot the ` NA` value in our result, in real world when dealing with large datasets it might get super difficult to spot these values. Let's go into ***unique-ception***.


```r
# check if there is a NA value
## returns a vector of TRUE & FALSE depending on the NA position
na_check <- is.na(unique(age))

# check the Unique entries in our vector
unique(na_check)
#> [1] FALSE  TRUE
```

Here first we are checking each value in `age` to see if it is `NA` which result in a vector containing logical values only, and then we are running our `unique()` function on the result to see if `TRUE` appears, indicating `NA` values in `age`.

As expected and with the presence of ` TRUE` in our result we know that there exists ` NA` in our data. Note the ease of reading this result makes it much more easier to identify the presence of ` NA` compared to `is.na()`.

#### Special case

Thus far we have looked at what happens when there are valid entries in our input data frame. Now let us now look at what to expect in the case where the input is pointing to an empty data frame.


```r
# declare the empty vector
empty <- c()
# test the result
unique(empty)
#> NULL
```

In the case where we have an empty data set the ` unique()` function returns ` NULL`. This is because our declared variable is storing a ` NULL` (empty) vector. In the case of an empty integer vector the return value will be ` integer(0)`.

Sometimes we might run into other funny yet complicated situations, so let's look at some examples and the results we will get.

Let's see if there is a way to distinguish between `double` and `integers` which are two different ways R stores numbers.


```r
## Comparing double and  integer
unique(c(as.double(-0.000), +as.integer(0)))
#> [1] 0
```

Based on this result we now know that unique is not able to distinguish between integers and double, so let us see what can be done to deal with **EXACT EQUALITY** in the following section.

### Finding if objects are exactly similar: `identical()`

When comparing if two objects (vector, matrix, data frame, list, etc.) are **EXACTLY** equal in the case when dealing with a higher degree of precision or when dealing with super large datasets where storage of data type (64-bit-double versus 32-bit-integer) will have a significant effect on the storage and processing of data, we find use cases of comparing the EXACT equality. In these cases we will be using the ` identical()` function.

Another super useful use-case is when comparing objects of different lengths, ideally we would like to get a definitive value whether one is equal to another however the standard ` == ` will not give us one definitive answer and sometimes with the difference of length of our objects or presence of `NA` we might run into some errors.

#### Check if they are same, `identical()`

The `identical()` function **takes in** two inputs that can be any R object (numbers, vectors, matrix, data frames, etc.) and **returns** a logical answer: ` TRUE` if the two objects match and ` FALSE` otherwise.

Let's look at some examples to further cement our understanding.

#### Examples

##### Example 1

Let us start with an intuitive example. Think about ID checks in the case when you might go to a bar versus when you are boarding for an international flight. In both the cases you can present your passport as an ID, however at a bar they might just compare your face and look at your age and the results of acceptance or rejection will be based on these factors. In the case of boarding a flight, there are much more extensive checks, where not only do they verify your ID but also run some checks in their database to verify your visa and confirm your identity.

Here in this example you can think of the case of the bar check as a simple comparison using ` ==` versus the airport example as the check using ` identical()`.

##### Example 2

Let us now build our knowledge with some examples in R. Let's start off with a simple example of where we are comparing two vectors.


```r
# declaring the vector
v1 <- c(1, 2, 3)
v2 <- c(3, 2, 3)
# comparing the vectors
identical(v1, v2)
#> [1] FALSE
```

As expected, the result is `FALSE`, however let us see how the result would differ if we were to use our classical way of comparing the vectors with ` ==`.


```r
v1 == v2
#> [1] FALSE  TRUE  TRUE
```

Here we can see that the result is a vector containing a **one-to-one** comparison of the entries of the vectors, and although this is useful, getting a single logical outcome is much more beneficial and easier to process and read.

Also (as mentioned before) in the case where the vectors are large or of unequal length, or contain `NA` values, we may run into problems.

Let us quickly look at some of these examples:


```r
v1 <- c(1, 2, 3)
v2 <- c(1, 2)
v1 == v2
#> [1]  TRUE  TRUE FALSE
```

Here we can see that we get a warning about the lengths of the vector not being equal. However we will not run into this problem with `identical()` as seen next.


```r
identical(v1, v2)
#> [1] FALSE
```

As expected we got one logical output which we should be expecting.

Let us now look at the example containing ` NA` and close this example:


```r
v1 <- c(11, 22, 33)
v2  <- c(1, 2, NA)
v1 == v2
#> [1] FALSE FALSE    NA
```

Here again we see if there is a `NA` in any of our values then ` ===` fails to get us the desired result, however let us see how to work around this.


```r
identical(v1, v2)
#> [1] FALSE
```

Here we can see that using the `identical()` function we are able to identify that the two vectors are not equal even if they contain `NA`. This is extremely useful while data-cleaning and also when merging 2 datasets.

***More on merging can be found in chapter: He was a d8er boi***

##### Example 3

Let's revisit the example from the previous section where we were comparing integers with double and see how the results differ.


```r
# declare our R objects
obj_int <- as.integer(0)
obj_float <- as.double(0)
# check if the objects are equal
identical(obj_int, obj_float)
#> [1] FALSE
```

Recall in the case when we used ` unique()` we were unable to distinguish between them, however here as expected we are able to distinguish one object type from the other.

Let us look at another case and see how to deal with it. Let us see how to differentiate between ` +0` and ` -0`. In an intuitive sense both of them are equal but on the number line in the case of `-0` we are approaching 0 from negative side (...,-2,-1,-0) and in the in the case of `+0` we are approaching the 0 from the positive side(...,2,1,0).


```r
identical(+2 * 0, -1 * 0)
#> [1] TRUE
```

Ahh! Interesting, as we should have expected to get a different result, however we didn't. Let us see if there is a way to work around this.

There are **built in arguments** which we can use to solve this issue, `identical(-x,+x, num.eq = FALSE)`. Here the new argument of ` num.eq = FALSE` is used to deal with this situation. Note by default it is set to ` TRUE` meaning that it does not compare on a bit-wise level. However by changing the argument to ` FALSE`, we are doing a **bit-wise comparison**(The numbers -0 and +0 have a different representation when translated into binary).

Let's see how this makes a difference.


```r
identical(+ 2 * 0, -1 * 0, num.eq = FALSE)
#> [1] FALSE
```

Here based on the output we can see that the `+0` and `-0`, are now treated differently which is expected as they are not bitwise equal.

#### Looking further

The `identical()` function can be used to compare not only datasets but also to compare objects in different environments(local/global). Furthermore, it is rare to run into errors using this function as most of the errors involved are due to an invalid pointer at C-lvl (variables being compared were not declared properly), but those are out of our current scope.

However to build up your knowledge and to get your paws dirty I would strongly encourage to study ` all.equal()` and see how it differs from the `identical()` function. Notes on `all.equal()` can be found [here](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/all.equal).


<!-- ```{r q1, echo=FALSE} -->
<!-- question("To check if every value in the data frame; `data.frame` is NA, which of the following code will you use?", -->
<!--   answer(" `is.na(data.frame)` ", correct = TRUE ), -->
<!--   answer(" `which(data.frame == NA)` ",  message = "Checks if the dataframe is set to `NULL`") -->
<!-- ) -->
<!-- ``` -->

<!-- ### Q2 -->
<!-- ```{r q2, echo=FALSE} -->
<!-- question("To get the location of values in the data data frame; `data.frame` that are NA, Which of the following code chuck will you use?", -->
<!--   answer(" `which(is.na(data.frame))` ", correct = TRUE ), -->
<!--   answer(" `which(data.frame == NA)` ",  message = "Invalid, but investigate why does this return 1?") -->
<!-- ) -->
<!-- ``` -->

<!-- ### Q3 -->
<!-- ```{r q3, echo=FALSE} -->
<!-- question("What is the result, when we run the `which()` function with the logical condition on the data frame and the data frame contains no value that matches our logical condition?", -->
<!--   answer(" `integer(0)` ", correct = TRUE ), -->
<!--   answer(" `NA` ",  message = "It returns an integer vector of 0 length ie. `integer(0)` "), -->
<!--   answer(" `logical(0)`",  message = "It returns an integer vector of 0 length ie. `integer(0)` ") -->
<!-- ) -->
<!-- ``` -->

<!-- ### Q4 -->
<!-- `rand_vector <-c("22","NA","hello", "world")` \ -->
<!-- `which(rand_vector == NA) ` \ -->
<!-- ```{r q4, echo=FALSE} -->
<!-- question("What is the result when you run the above code chuck? ", -->
<!--   answer(" `integer(0)` ", correct = TRUE ), -->
<!--   answer(" `NA` ",  message = "Check Data-types in the logical argument"), -->
<!--   answer(" `logical(0)`",  message = "Declared vector is of type character"), -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

<!-- ### Q5 -->
<!-- ```{r q5, echo=FALSE} -->
<!-- question("What is the output type of `is.na()` function on a dataframe? ", -->
<!--   answer(" logical Vector ",  message = "Type should match to that of the input" ), -->
<!--   answer(" logical Matrix ",  message = "Type should match to that of the input"), -->
<!--   answer(" Can be either",  correct = TRUE, message = "depending on the declaration of the dataframe" ), -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

<!-- ### Q6 -->
<!-- `empty <- c()` \ -->
<!-- `unique(empty)` \ -->
<!-- ```{r q6, echo=FALSE} -->
<!-- question("What is the output of the previous code code? ", -->
<!--   answer(" `NULL` ",  correct = TRUE), -->
<!--   answer("` NA` ",  message = "Close, try again ;) "), -->
<!--   answer(" `integer(0)`", message = "Note the declared variable is EMPTY" ), -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

<!-- ### Q7 -->
<!-- `vec <- c(1,1,3,NA)` \ -->
<!-- `unique(vec)` -->
<!-- ```{r q7, echo=FALSE} -->
<!-- question("What is the output of the previous code code? ", -->
<!--   answer(" Error, because of NA ",  message = "unique() identify `NA` as a value"), -->
<!--   answer("`1, 3, NA` ", correct = TRUE), -->
<!--   answer(" `1, 3`", message = "Close, try again ;)" ), -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

<!-- ### Q8 -->
<!-- ```{r q8, echo=FALSE} -->
<!-- question("What are some of the use cases for using identical() over the standard '==' to compare objects?", -->
<!--   answer("Easier to read the final result, when comparing large datasets", message = " and more... "), -->
<!--   answer("Much more reliable, deals with cases of NA values in the data frames", message = " and more... "), -->
<!--   answer("Comparison of datatype and sensitive values; double vs integer or -0 vs +0", message = " and more... " ), -->
<!--   answer("All of the above", correct = TRUE ), -->
<!--   allow_retry = TRUE -->
<!-- ) -->
<!-- ``` -->

<!-- ### Q9 -->
<!-- `v1 <- c(1,3,3,4, NA, NA)` \ -->
<!-- `v2 <- c(1,3,4,NA)` \ -->
<!-- `identical(unique(v1), v2)` \ -->
<!-- ```{r q9, echo=FALSE} -->
<!-- question("What is the output of the previous code code? ", -->
<!--   answer(" Error, because of `NA` ",  message = "unique(), identical() identify `NA` as a value"), -->
<!--   answer("`TRUE` ", correct = TRUE), -->
<!--   answer(" `FALSE`", message = "`unique(v1)` returns us an IDENTICAL copy of v2" ), -->
<!--   allow_retry = TRUE -->
<!-- ) -->

<!-- ``` -->

<!-- ### Q10 -->
<!-- For this question we will be writing the R-code in the provided code chunk to achieve the requested desired outcome. Furthermore, you may choose to concatenate your function call if you'd like.\ -->
<!-- ***Note, parts of this problem might seem challenging, breaking down the tasks into sub tasks would be a good place to start*** -->

<!-- This question we will mainly be working with `iris` data set. Let us first see what the data set looks like; \ -->
<!-- ```{r q10, exercise.eval = TRUE, exercise = TRUE, exercise.lines = 1} -->
<!-- head(iris) -->
<!-- ``` -->

<!-- a) Find if there are any NA values for the variable `Species` in our data and give the number of the total such occurring values; \ -->
<!-- Hint: Use a combination of functions, 'length()' function might be useful -->
<!-- ```{r q_10a, exercise.eval = TRUE, exercise = TRUE, exercise.lines = 5 } -->

<!-- ``` -->


<!-- ```{r q_10a-solution } -->
<!-- length(which(is.na(iris$Species))) -->
<!-- ``` -->


<!-- b) get the position of all the values which are from the "setosa" species AND have the sepal length > 5 -->
<!-- Hint: break down your logical argument first -->
<!-- ```{r q_10b, exercise.eval = TRUE, exercise = TRUE, exercise.lines = 5 } -->

<!-- ``` -->


<!-- ```{r q_10b-solution } -->
<!-- which( (iris$Species == "setosa") & (iris$Sepal.Length > 5)) -->
<!-- ``` -->



<!-- c) get the count of all the unique species of flowers in the `iris` dataframe. -->
<!-- Hint; Use a combination of functions, 'length()' function might be useful -->
<!-- ```{r q_10c, exercise.eval = TRUE, exercise = TRUE, exercise.lines = 5 } -->

<!-- ``` -->


<!-- ```{r q_10c-solution } -->
<!-- length(unique(iris$Species)) -->
<!-- ``` -->

<!-- d) For this part we will be also working with another data set, `iris3` and comparing one of the variable from this data set with our variable from the `iris` data set. \ -->
<!-- You are required to complete the code, your task is to check if the UNIQUE, Sepal lengths(`Sepal.Length`) for the "setosa" specie, between the 2 datasets are IDENTICAL. \ -->
<!-- Hint; `filter()` will come in handy for some of this task. \ -->
<!-- **The loading of  the required variable from the `iris3` data set has been completed for you.** \ -->


<!-- ```{r q_10d1, exercise.eval = TRUE, exercise = TRUE, exercise.lines = 10 } -->
<!-- setosa.Sepal.IR3 <-  tibble(Sepal.Length = as.data.frame(iris3)[, c(1)] ) -->

<!-- ``` -->


<!-- ```{r q_10d1-solution } -->
<!-- setosa.Sepal.IR3 <-  tibble(Sepal.Length = as.data.frame(iris3)[, c(1)]) -->

<!-- setosa.Sepal.IR <- iris %>% -->
<!--   filter(iris$Species == "setosa" ) %>% -->
<!--   select(Sepal.Length) -->

<!-- identical(unique(setosa.Sepal.IR3$Sepal.Length) , unique(setosa.Sepal.IR$Sepal.Length)) -->
<!-- ``` -->




## Refrences
- Data Simulation \
 [Facts on data](https://jech.bmj.com/content/jech/40/4/319.full.pdf) \
 [Generating random NA](https://www.youtube.com/watch?v=sNNoTd7xI-4&t=769s) \
 
- `is.na()` \
 [Documentation](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/NA) \
 [Example ideas](https://www.programmingr.com/tutorial/is-na/) \
 
- `which()` \
 [Documentation](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/which) \
 [Example ideas](https://www.journaldev.com/45274/which-function-in-r) \
 [More example ideas](https://www.r-bloggers.com/2017/03/which-function-in-r/) \

- `unique()` \
 [Documentation](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/unique) \
 [Example ideas](https://www.journaldev.com/44614/unique-function-r-programming) \
 
- `identical()` \
 [Documentation](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/identical) \
 [Example ideas](https://rdrr.io/r/base/identical.html) \
 [More example ideas](https://docs.tibco.com/pub/enterprise-runtime-for-R/5.0.0/doc/html/Language_Reference/base/identical.html) \
 [Bitwise comparison](https://www.datasciencemadesimple.com/test-equality-two-objects-using-identical-function-in-r/) \
 [More example ideas](https://stackoverflow.com/questions/3395696/whats-the-difference-between-identicalx-y-and-istrueall-equalx-y) \



## Exercises

### Question 1
To check if every value in the data frame; `data.frame` is NA, which of the following code will you use? \
a.  `is.na(data.frame)` \
b. `which(data.frame == NA)` \

### Question 2
To get the location of values in the data data frame; `data.frame` that are NA, Which of the following code chuck will you use? \
a.  `which(is.na(data.frame))` \
b. `which(data.frame == NA)` \

### Question 3
What is the result, when we run the `which()` function with the logical condition on the data frame and the data frame contains no value that matches our logical condition? \
a.  `integer(0)` \
b. `NA` \
c. `logical(0)` \

### Question 4
`rand_vector <-c("22","NA","hello", "world")` \
`which(rand_vector == NA) ` \ 

What is the result when you run the above code chuck? \
a.  `integer(0)` \
b. `NA` \
c. `logical(0)` \

### Question 5
What is the output type of `is.na()` function on a dataframe? \
a. `logical Vector` \
b. `logical Matrix` \
c.   Can be either \

### Question 6
`empty <- c()` \
`unique(empty)` \

What is the output of the previous code code? \
a.  `NULL` \ 
b. `NA` \
c. `integer(0)` \

### Question 7
`vec <- c(1,1,3,NA)` \
`unique(vec)` \

What is the output of the previous code code? \
a. Error, because of NA " \
b.  `1, 3, NA`  \
c. `1, 3`" \

### Question 8
What are some of the use cases for using identical() over the standard '==' to compare objects? \
a. Easier to read the final result, when comparing large datasets" \
b. Much more reliable, deals with cases of NA values in the data frames \
c. Comparison of datatype and sensitive values; double vs integer or -0 vs +0" \
d.  All of the above \

### Question 9
`v1 <- c(1,3,3,4, NA, NA)` \
`v2 <- c(1,3,4,NA)` \ 
`identical(unique(v1), v2)` \

What is the output of the previous code code? \
a. Error, because of `NA` \
b.  `TRUE` \
c. `FALSE` \

### Question 10
   !!!! Dynamic Question in .RMD commented out NEED TO CHANGE THE FORMAT and ADD Later !!! 
