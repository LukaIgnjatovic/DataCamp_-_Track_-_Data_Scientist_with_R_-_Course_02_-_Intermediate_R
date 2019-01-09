---
title: "DataCamp - Intermediate R"
author: "[Luka Ignjatovi&#263;](https://github.com/LukaIgnjatovic)"
output:
  html_document:
    highlight: tango
    theme: united
    toc: yes
    toc_depth: 4
    keep_md: true
  md_document:
    toc: true
    toc_depth: 4
---

## Functions

Functions are an extremely important concept in almost every programming language; R is not different. After learning what a function is and how you can use one, you'll take full control by writing your own functions.

<div align="middle">

> **Document:** ["Slides - Functions"](./Slides/Chapter 03 - Functions.pdf)

</div>

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 03 - Lecture 01 - Introduction to functions.mp4" type="video/mp4"/>

</div>

### Function documentation

Before even thinking of using an R function, you should clarify which arguments it expects. All the relevant details such as a description, usage, and arguments can be found in the documentation. To consult the documentation on the `sample()` function, for example, you can use one of following R commands:

    help(sample)
    ?sample

If you execute these commands in the console of the DataCamp interface, you'll be redirected to www.rdocumentation.org.

A quick hack to see the arguments of the `sample()` function is the `args()` function. Try it out in the console:

    args(sample)

In the next exercises, you'll be learning how to use the `mean()` function with increasing complexity. The first thing you'll have to do is get acquainted with the `mean()` function.

#### Instructions
* *Consult the documentation on the* `mean()` *function:* `?mean` *or* `help(mean)`*.*
* *Inspect the arguments of the* `mean()` *function using the* `args()` *function.*

```r
# Consult the documentation on the mean() function
?mean

# Inspect the arguments of the mean() function
args(mean)
```

**Great! That wasn't too hard, was it? Take a look at the documentation and head over to the next exercise.**

### Use a function

The documentation on the `mean()` function gives us quite some information:

* The `mean()` function computes the arithmetic mean.
* The most general method takes multiple arguments: `x` and `...`.
* The `x` argument should be a vector containing numeric, logical or time-related information.

Remember that R can match arguments both by position and by name. Can you still remember the difference? You'll find out in this exercise!

Once more, you'll be working with the view counts of your social network profiles for the past 7 days. These are stored in the `linkedin` and `facebook` vectors and have already been defined in the editor on the right.

#### Instructions
* *Calculate the average number of views for both* `linkedin` *and* `facebook` *and assign the result to* `avg_li` *and* `avg_fb`*, respectively. Experiment with different types of argument matching!*
* *Print out both* `avg_li` *and* `avg_fb`*.*

```r
# The linkedin and facebook vectors have already been created for you
linkedin <- c(16, 9, 13, 5, 2, 17, 14)
facebook <- c(17, 7, 5, 16, 8, 13, 14)

# Calculate average number of views
avg_li <- mean(linkedin)
avg_fb <- mean(facebook)

# Inspect avg_li and avg_fb
avg_li
```

```
## [1] 10.85714
```

```r
avg_fb
```

```
## [1] 11.42857
```

**Nice! I'm sure you've already called more advanced R functions in your history as a programmer. Now you also know what actually happens under the hood.**

### Use a function (2)

Check the documentation on the `mean()` function again:

    ?mean

The Usage section of the documentation includes two versions of the `mean()` function. The first usage,

    mean(x, ...)

is the most general usage of the mean function. The 'Default S3 method', however, is:

    mean(x, trim = 0, na.rm = FALSE, ...)

The `...` is called the ellipsis. It is a way for R to pass arguments along without the function having to name them explicitly. The ellipsis will be treated in more detail in future courses.

For the remainder of this exercise, just work with the second usage of the mean function. Notice that both `trim` and `na.rm` have default values. This makes them **optional arguments**.

#### Instructions
* *Calculate the mean of the element-wise sum of* `linkedin` *and* `facebook` *and store the result in a variable* `avg_sum`*.*
* *Calculate the mean once more, but this time set the* `trim` *argument equal to 0.2 and assign the result to* `avg_sum_trimmed`*.*
* *Print out both* `avg_sum` *and* `avg_sum_trimmed`*; can you spot the difference?*

```r
# The linkedin and facebook vectors have already been created for you
linkedin <- c(16, 9, 13, 5, 2, 17, 14)
facebook <- c(17, 7, 5, 16, 8, 13, 14)

# Calculate the mean of the sum
avg_sum <- mean(linkedin + facebook)

# Calculate the trimmed mean of the sum
avg_sum_trimmed <- mean(linkedin + facebook, trim = 0.2)

# Inspect both new variables
avg_sum
```

```
## [1] 22.28571
```

```r
avg_sum_trimmed
```

```
## [1] 22.6
```

**Nice! When the** `trim` **argument is not zero, it chops off a fraction (equal to** `trim`**) of the vector you pass as argument** `x`**.**

### Use a function (3)

In the video, Filip guided you through the example of specifying arguments of the `sd()` function. The `sd()` function has an optional argument, `na.rm` that specified whether or not to remove missing values from the input vector before calculating the standard deviation.

If you've had a good look at the documentation, you'll know by now that the `mean()` function also has this argument, `na.rm`, and it does the exact same thing. By default, it is set to `FALSE`, as the Usage of the `Default S3 method` shows:

    mean(x, trim = 0, na.rm = FALSE, ...)

Let's see what happens if your vectors `linkedin` and `facebook` contain missing values (`NA`).

#### Instructions
* *Calculate the average number of LinkedIn profile views, without specifying any optional arguments. Simply print the result to the console.*
* *Calculate the average number of LinkedIn profile views, but this time tell R to strip missing values from the input vector.*

```r
# The linkedin and facebook vectors have already been created for you
linkedin <- c(16, 9, 13, 5, NA, 17, 14)
facebook <- c(17, NA, 5, 16, 8, 13, 14)

# Basic average of linkedin
mean(linkedin)
```

```
## [1] NA
```

```r
# Advanced average of linkedin
mean(linkedin, na.rm = TRUE)
```

```
## [1] 12.33333
```

**Awesome! Up to the next exercise!**

### Functions inside functions

You already know that R functions return objects that you can then use somewhere else. This makes it easy to use functions inside functions, as you've seen before:

    speed <- 31
    print(paste("Your speed is", speed))

Notice that both the `print()` and `paste()` functions use the ellipsis - `...` - as an argument. Can you figure out how they're used?

#### Instructions
*Use* `abs()` *on* `linkedin - facebook` *to get the absolute differences between the daily Linkedin and Facebook profile views. Next, use this function call inside* `mean()` *to calculate the Mean Absolute Deviation. In the* `mean()` *call, make sure to specify* `na.rm` *to treat missing values correctly!*

```r
# The linkedin and facebook vectors have already been created for you
linkedin <- c(16, 9, 13, 5, NA, 17, 14)
facebook <- c(17, NA, 5, 16, 8, 13, 14)

# Calculate the mean absolute deviation
mean(abs(linkedin - facebook), na.rm = TRUE)
```

```
## [1] 4.8
```

**Excellent! Proceed to the next exercise.**

### Required, or optional?

By now, you will probably have a good understanding of the difference between required and optional arguments. Let's refresh this difference by having one last look at the `mean()` function:

    mean(x, trim = 0, na.rm = FALSE, ...)

`x` is required; if you do not specify it, R will throw an error. `trim` and `na.rm` are optional arguments: they have a default value which is used if the arguments are not explicitly specified.

Which of the following statements about the `read.table()` function are true?

  1. `header`, `sep` and `quote` are all optional arguments.
  2. `row.names` and `fileEncoding` don't have default values.
  3. `read.table("myfile.txt", "-", TRUE)` will throw an error.
  4. `read.table("myfile.txt", sep = "-", header = TRUE)` will throw an error.

*Possible answers:*

* **(1) and (3)**
* *(2) and (4)*
* *(1), (2), and (3)*
* *(1), (2), and (4)*

**Great! Using functions that are already available in R is pretty straightforward, but how about writing your own functions to supercharge your R programs? The next video will tell you how.**

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 03 - Lecture 02 - Writing functions.mp4" type="video/mp4"/>

</div>

### Write your own function

Wow, things are getting serious... You're about to write your own function! Before you have a go at it, have a look at the following function template:

    my_fun <- function(arg1, arg2) {
      body
    }

Notice that this recipe uses the assignment operator (`<-`) just as if you were assigning a vector to a variable for example. This is not a coincidence. Creating a function in R basically is the assignment of a function object to a variable! In the recipe above, you're creating a new R variable `my_fun`, that becomes available in the workspace as soon as you execute the definition. From then on, you can use the `my_fun` as a function.

#### Instructions
* *Create a function* `pow_two()`*: it takes one argument and returns that number squared (that number times itself).*
* *Call this newly defined function with* `12` *as input.*
* *Next, create a function* `sum_abs()`*, that takes two arguments and returns the sum of the absolute values of both arguments.*
* *Finally, call the function* `sum_abs()` *with arguments* `-2` *and* `3` *afterwards.*

```r
# Create a function pow_two()
pow_two <- function(x) {
  x ** 2
}

# Use the function
pow_two(12)
```

```
## [1] 144
```

```r
# Create a function sum_abs()
sum_abs <- function(a, b) {
  abs(a) + abs(b)  
}

# Use the function
sum_abs(-2, 3)
```

```
## [1] 5
```

**Great! Step it up a notch in the next exercise!**

### Write your own function (2)

There are situations in which your function does not require an input. Let's say you want to write a function that gives us the random outcome of throwing a fair die:

    throw_die <- function() {
      number <- sample(1:6, size = 1)
      number
    }

    throw_die()

Up to you to code a function that doesn't take any arguments!

#### Instructions
* *Define a function,* `hello()`*. It prints out "Hi there!" and returns* `TRUE`*. It has no arguments.*
* *Call the function* `hello()`*, without specifying arguments of course.*

```r
# Define the function hello()
hello <- function() {
  print("Hi there!")
  return(TRUE)
}

# Call the function hello()
hello()
```

```
## [1] "Hi there!"
```

```
## [1] TRUE
```

**Truly impressive! Head over to the next exercise.**

### Write your own function (3)

Do you still remember the difference between an argument with and without default values? Have another look at the `sd()` function by typing `?sd` in the console. The usage section shows the following information:

    sd(x, na.rm = FALSE)

This tells us that `x` has to be defined for the `sd()` function to be called correctly, however, `na.rm` already has a default value. Not specifying this argument won't cause an error.

You can define default argument values in your own R functions as well. You can use the following recipe to do so:

    my_fun <- function(arg1, arg2 = val2) {
      body
    }
The editor on the right already includes an extended version of the `pow_two()` function from before. Can you finish it?

#### Instructions
* *Add an optional argument, named* `print_info`*, that is* `TRUE` *by default.*
* *Wrap an* `if` *construct around the* `print()` *function: this function should only be executed if* `print_info` *is* `TRUE`*.*
* *Feel free to experiment with the* `pow_two()` *function you've just coded.*

```r
# Finish the pow_two() function
pow_two <- function(x, print_info = TRUE) {
  y <- x ** 2
  if (print_info == TRUE){
    print(paste(x, "to the power two equals", y))
  }
  return(y)
}
```

**Wonderful! Have you tried calling this** `pow_two()` **function? Try** `pow_two(5)`**,** `pow_two(5, TRUE)` **and** `pow_two(5, FALSE)`**. Which ones give different results?**

### Function scoping

An issue that Filip did not discuss in the video is function scoping. It implies that variables that are defined inside a function are not accessible outside that function. Try running the following code and see if you understand the results:

    pow_two <- function(x) {
      y <- x ** 2
      return(y)
    }

    pow_two(4)
    y
    x

`y` was defined inside the `pow_two()` function and therefore it is not accessible outside of that function. This is also true for the function's arguments of course - `x` in this case.

Which statement is correct about the following chunk of code? The function `two_dice()` is already available in the workspace.

    two_dice <- function() {
      possibilities <- 1:6
      dice1 <- sample(possibilities, size = 1)
      dice2 <- sample(possibilities, size = 1)
      dice1 + dice2
    }

*Possible answers:*

* *Executing* `two_dice()` *causes an error.*
* *Executing* `res <- two_dice()` *makes the contents of* `dice1` *and* `dice2` *available outside the function.*
* **Whatever the way of calling the** `two_dice()` **function, R won't have access to** `dice1` **and** `dice2` **outside the function.**

**Great! If you're familiar with other programming languages, you might wonder whether R passes arguments *by value* or *by reference*. Find out in the next exercise!**

### R passes arguments by value

The title gives it away already: R passes arguments by value. What does this mean? Simply put, it means that an R function cannot change the variable that you input to that function. Let's look at a simple example (try it in the console):

    triple <- function(x) {
      x <- 3*x
      x
    }
    
    a <- 5
    triple(a)
    a

Inside the `triple()` function, the argument `x` gets overwritten with its value times three. Afterwards this new `x` is returned. If you call this function with a variable `a` set equal to 5, you obtain 15. But did the value of `a` change? If R were to pass `a` to `triple()` *by reference*, the override of the `x` *inside* the function would ripple through to the variable `a`, outside the function. However, R passes *by value*, so the R objects you pass to a function can never change unless you do an explicit assignment. `a` remains equal to 5, even after calling `triple(a)`.

Can you tell which one of the following statements is **false** about the following piece of code?

    increment <- function(x, inc = 1) {
      x <- x + inc
      x
    }
    
    count <- 5
    a <- increment(count, 2)
    b <- increment(count)
    count <- increment(count, 2)

*Possible answers:*

* `a` *and* `b` *equal 7 and 6 respectively after executing this code block.*
* *After the first call of* `increment()`*, where* `a` *is defined,* `a` *equals 7 and count equals 5.*
* **In the end,** `count` **will equal 10.**
* *In the last expression, the value of* `count` *was actually changed because of the explicit assignment.*

**Well done! Given that R passes arguments *by value* and not *by reference*, the value of** `count` **is not changed after the first two calls of** `increment()`**. Only in the final expression, where** `count` **is re-assigned explicitly, does the value of** `count` **change.**

### R you functional?

Now that you've acquired some skills in defining functions with different types of arguments and return values, you should try to create more advanced functions. As you've noticed in the previous exercises, it's perfectly possible to add control-flow constructs, loops and even other functions to your function body.

Remember our social media example? The vectors `linkedin` and `facebook` are already defined in the workspace so you can get your hands dirty straight away. As a first step, you will be writing a function that can interpret a single value of this vector. In the next exercise, you will write another function that can handle an entire vector at once.

#### Instructions
* *Finish the function definition for* `interpret()`*, that interprets the number of profile views on a single day:*
* *The function takes one argument,* `num_views`*.*
* *If* `num_views` *is greater than 15, the function prints out "You're popular!" to the console and returns* `num_views`*.*
* *Else, the function prints out "Try to be more visible!" and returns 0.*
* *Finally, call the* `interpret()` *function twice: on the first value of the* `linkedin` *vector and on the second element of the* `facebook` *vector.*

```r
# The linkedin and facebook vectors have already been created for you
linkedin <- c(16, 9, 13, 5, 2, 17, 14)
facebook <- c(17, 7, 5, 16, 8, 13, 14)

# Define the interpret function
interpret <- function(num_views) {
  if (num_views > 15) {
    print("You're popular!")
    return(num_views)
  } else {
    print("Try to be more visible!")
    return(0)
  }
}

# Call the interpret function twice
interpret(linkedin[1])
```

```
## [1] "You're popular!"
```

```
## [1] 16
```

```r
interpret(facebook[2])
```

```
## [1] "Try to be more visible!"
```

```
## [1] 0
```

**Funkadelic! The annoying thing here is that** `interpret()` **only takes one argument. Proceed to the next exercise to implement something more useful.**

### R you functional? (2)

A possible implementation of the `interpret()` function is already available in the editor. In this exercise you'll be writing another function that will use the `interpret()` function to interpret all the data from your daily profile views inside a vector. Furthermore, your function will return the sum of views on popular days, if asked for. A `for` loop is ideal for iterating over all the vector elements. The ability to return the sum of views on popular days is something you can code through a function argument with a default value.

#### Instructions
*Finish the template for the* `interpret_all()` *function:*

* *Make* `return_sum` *an optional argument, that is* `TRUE` *by default.*
* *Inside the* `for` *loop, iterate over all* `views`*: on every iteration, add the result of* `interpret(v)` *to* `count`*. Remember that* `interpret(v)` *returns* `v` *for popular days, and* `0` *otherwise. At the same time,* `interpret(v)` *will also do some printouts.*
* *Finish the* `if` *construct so that if* `return_sum` *is* `TRUE`*, return* `count` *and else, return* `NULL`*.*

*Call this newly defined function on both* `linkedin` *and* `facebook`*.*

```r
# The linkedin and facebook vectors have already been created for you
linkedin <- c(16, 9, 13, 5, 2, 17, 14)
facebook <- c(17, 7, 5, 16, 8, 13, 14)

# The interpret() can be used inside interpret_all()
interpret <- function(num_views) {
  if (num_views > 15) {
    print("You're popular!")
    return(num_views)
  } else {
    print("Try to be more visible!")
    return(0)
  }
}

# Define the interpret_all() function
# views: vector with data to interpret
# return_sum: return total number of views on popular days?
interpret_all <- function(views, return_sum = TRUE) {
  count <- 0

  for (v in views) {
    count <- count + interpret(v)
  }

  if (return_sum == TRUE) {
    return (count)
  } else {
    return (NULL)
  }
}

# Call the interpret_all() function on both linkedin and facebook
interpret_all(linkedin)
```

```
## [1] "You're popular!"
## [1] "Try to be more visible!"
## [1] "Try to be more visible!"
## [1] "Try to be more visible!"
## [1] "Try to be more visible!"
## [1] "You're popular!"
## [1] "Try to be more visible!"
```

```
## [1] 33
```

```r
interpret_all(facebook)
```

```
## [1] "You're popular!"
## [1] "Try to be more visible!"
## [1] "Try to be more visible!"
## [1] "You're popular!"
## [1] "Try to be more visible!"
## [1] "Try to be more visible!"
## [1] "Try to be more visible!"
```

```
## [1] 33
```

**Perfect! Have a look at the results; it appears that the sum of views on popular days are the same for Facebook and LinkedIn, what a coincidence! Your different social profiles must be fairly balanced. Head over to the next video!**

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 03 - Lecture 03 - R packages.mp4" type="video/mp4"/>

</div>

### Load an R Package

There are basically two extremely important functions when it comes down to R packages:

* `install.packages()`, which as you can expect, installs a given package.
* `library()` which loads packages, i.e. attaches them to the search list on your R workspace.

To install packages, you need administrator privileges. This means that `install.packages()` will thus not work in the DataCamp interface. However, almost all CRAN packages are installed on our servers. You can load them with `library()`.

In this exercise, you'll be learning how to load the `ggplot2` package, a powerful package for data visualization. You'll use it to create a plot of two variables of the `mtcars` data frame. The data has already been prepared for you in the workspace.

Before starting, execute the following commands in the console:

* `search()`, to look at the currently attached packages and
* `qplot(mtcars$wt, mtcars$hp)`, to build a plot of two variables of the `mtcars` data frame.

An error should occur, because you haven't loaded the `ggplot2` package yet!

#### Instructions
* *To fix the error you saw in the console, load the* `ggplot2` *package.*
* *Now, retry calling the* `qplot()` *function with the same arguments.*
* *Finally, check out the currently attached packages again.*

```r
# Load the ggplot2 package
library(ggplot2)

# Retry the qplot() function
qplot(mtcars$wt, mtcars$hp)
```

![](Chapter_03_-_Practice_-_Functions_files/figure-html/qplot example-1.png)<!-- -->

```r
# Check out the currently attached packages again
search()
```

```
##  [1] ".GlobalEnv"        "package:ggplot2"   "package:stats"    
##  [4] "package:graphics"  "package:grDevices" "package:utils"    
##  [7] "package:datasets"  "package:methods"   "Autoloads"        
## [10] "package:base"
```

**Awesome! Notice how** `search()` *and* `library()` *are closely interconnected functions. Head over to the next exercise.*

### Different ways to load a package

The `library()` and `require()` functions are not very picky when it comes down to argument types: both `library(rjson)` and `library("rjson")` work perfectly fine for loading a package.

Have a look at some more code chunks that (attempt to) load one or more packages:

    # Chunk 1
    library(data.table)
    require(rjson)

    # Chunk 2
    library("data.table")
    require(rjson)

    # Chunk 3
    library(data.table)
    require(rjson, character.only = TRUE)

    # Chunk 4
    library(c("data.table", "rjson"))

Select the option that lists **all** of the chunks that do not generate an error. The console on the right is yours to experiment in.

*Possible answers:*  

* *Only (1)*
* **(1) and (2)**
* *(1), (2) and (3)*
* *All of them are valid*  

**Great! Indeed, only chunk 1 and chunk 2 are correct. Can you figure out why the last two aren't valid? This exercise concludes the chapter on functions. Well done!**  
**You have finished the chapter "Functions"!**
