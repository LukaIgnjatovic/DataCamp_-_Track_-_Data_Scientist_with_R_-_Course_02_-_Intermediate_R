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

## The apply family

Whenever you're using a for loop, you might want to revise your code and see whether you can use the lapply function instead. Learn all about this intuitive way of applying a function over a list or a vector, and its variants sapply and vapply.

<div align="middle">

> **Document:** ["Slides - The apply family"](./Slides/Chapter 04 - The apply family.pdf)

</div>

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 04 - Lecture 01 - lapply.mp4" type="video/mp4"/>

</div>

### Use lapply with a built-in R function

Before you go about solving the exercises below, have a look at the documentation of the `lapply()` function. The Usage section shows the following expression:

    lapply(X, FUN, ...)

To put it generally, `lapply` takes a vector or list `X`, and applies the function `FUN` to each of its members. If `FUN` requires additional arguments, you pass them after you've specified `X` and `FUN` (`...`). The output of `lapply()` is a list, the same length as `X`, where each element is the result of applying `FUN` on the corresponding element of `X`.

Now that you are truly brushing up on your data science skills, let's revisit some of the most relevant figures in data science history. We've compiled a vector of famous mathematicians/statisticians and the year they were born. Up to you to extract some information!

#### Instructions
* *Have a look at the* `strsplit()` *calls, that splits the strings in* `pioneers` *on the* `:` *sign. The result,* `split_math` *is a list of 4 character vectors: the first vector element represents the name, the second element the birth year.*
* *Use* `lapply()` *to convert the character vectors in* `split_math` *to lowercase letters: apply* `tolower()` *on each of the elements in* `split_math`*. Assign the result, which is a list, to a new variable* `split_low`*.*
* *Finally, inspect the contents of* `split_low` *with* `str()`*.*

```r
# The vector pioneers has already been created for you
pioneers <- c("GAUSS:1777", "BAYES:1702", "PASCAL:1623", "PEARSON:1857")

# Split names from birth year
split_math <- strsplit(pioneers, split = ":")

# Convert to lowercase strings: split_low
split_low <- lapply(split_math, tolower)

# Take a look at the structure of split_low
str(split_low)
```

```
## List of 4
##  $ : chr [1:2] "gauss" "1777"
##  $ : chr [1:2] "bayes" "1702"
##  $ : chr [1:2] "pascal" "1623"
##  $ : chr [1:2] "pearson" "1857"
```

**Great! Head over to the next exercise.**

### Use lapply with your own function

As Filip explained in the instructional video, you can use `lapply()` on your own functions as well. You just need to code a new function and make sure it is available in the workspace. After that, you can use the function inside `lapply()` just as you did with base R functions.

In the previous exercise you already used `lapply()` once to convert the information about your favorite pioneering statisticians to a list of vectors composed of two character strings. Let's write some code to select the names and the birth years separately.

The sample code already includes code that defined `select_first()`, that takes a vector as input and returns the first element of this vector.

#### Instructions
* *Apply* `select_first()` *over the elements of* `split_low` *with* `lapply()` *and assign the result to a new variable* `names`*.*
* *Next, write a function* `select_second()` *that does the exact same thing for the second element of an inputted vector.*
* *Finally, apply the* `select_second()` *function over* `split_low` *and assign the output to the variable* `years`*.*

```r
# Code from previous exercise:
pioneers <- c("GAUSS:1777", "BAYES:1702", "PASCAL:1623", "PEARSON:1857")
split <- strsplit(pioneers, split = ":")
split_low <- lapply(split, tolower)

# Write function select_first()
select_first <- function(x) {
  x[1]
}

# Apply select_first() over split_low: names
names <- lapply(split_low, select_first)

# Write function select_second()
select_second <- function(x) {
  x[2]
}

# Apply select_second() over split_low: years
years <- lapply(split_low, select_second)
```

**Nice one! Head over to the next exercise to learn about anonymous functions.**

### lapply and anonymous functions

Writing your own functions and then using them inside `lapply()` is quite an accomplishment! But defining functions to use them only once is kind of overkill, isn't it? That's why you can use so-called **anonymous functions** in R.

Previously, you learned that functions in R are objects in their own right. This means that they aren't automatically bound to a name. When you create a function, you can use the assignment operator to give the function a name. It's perfectly possible, however, to not give the function a name. This is called an anonymous function:

    # Named function
    triple <- function(x) { 3 * x }

    # Anonymous function with same implementation
    function(x) { 3 * x }

    # Use anonymous function inside lapply()
    lapply(list(1,2,3), function(x) { 3 * x })

#### Instructions
* *Transform the first call of* `lapply()` *such that it uses an anonymous function that does the same thing.*
* *In a similar fashion, convert the second call of* `lapply` *to use an anonymous version of the* `select_second()` *function.*
* *Remove both the definitions of* `select_first()` *and* `select_second()`*, as they are no longer useful.*

```r
# Definition of split_low
pioneers <- c("GAUSS:1777", "BAYES:1702", "PASCAL:1623", "PEARSON:1857")
split <- strsplit(pioneers, split = ":")
split_low <- lapply(split, tolower)

# Transform: use anonymous function inside lapply
names <- lapply(split_low, function(x) { x[1] })

# Transform: use anonymous function inside lapply
years <- lapply(split_low, function(x) { x[2] })
```

**Great! Now, there's another way to solve the issue of using the** `select_*()` **functions only once: you can make a more generic function that can be used in more places. Find out more about this in the next exercise.**

### Use lapply with additional arguments

In the video, the `triple()` function was transformed to the `multiply()` function to allow for a more generic approach. `lapply()` provides a way to handle functions that require more than one argument, such as the `multiply()` function:

    multiply <- function(x, factor) {
      x * factor
    }

    lapply(list(1,2,3), multiply, factor = 3)

On the right we've included a generic version of the select functions that you've coded earlier: `select_el()`. It takes a vector as its first argument, and an index as its second argument. It returns the vector's element at the specified index.

#### Instructions
*Use* `lapply()` *twice to call* `select_el()` *over all elements in* `split_low`*: once with the* `index` *equal to 1 and a second time with the index equal to 2. Assign the result to* `names` *and* `years`*, respectively.*

```r
# Definition of split_low
pioneers <- c("GAUSS:1777", "BAYES:1702", "PASCAL:1623", "PEARSON:1857")
split <- strsplit(pioneers, split = ":")
split_low <- lapply(split, tolower)

# Generic select function
select_el <- function(x, index) {
  x[index]
}

# Use lapply() twice on split_low: names and years
names <- lapply(split_low, select_el, index = 1)
years <- lapply(split_low, select_el, index = 2)
```

**Awesome! Your lapply skills are growing by the minute!**

### Apply functions that return NULL

In all of the previous exercises, it was assumed that the functions that were applied over vectors and lists actually returned a meaningful result. For example, the `tolower()` function simply returns the strings with the characters in lowercase. This won't always be the case. Suppose you want to display the structure of every element of a list. You could use the `str()` function for this, which returns `NULL`:

    lapply(list(1, "a", TRUE), str)

This call actually returns a list, the same size as the input list, containing all `NULL` values. On the other hand calling

    str(TRUE)

on its own prints only the structure of the logical to the console, not `NULL`. That's because `str()` uses `invisible()` behind the scenes, which returns an *invisible copy* of the return value, `NULL` in this case. This prevents it from being printed when the result of `str()` is not assigned.

What will the following code chunk return (`split_low` is already available in the workspace)? Try to reason about the result before simply executing it in the console!

    lapply(split_low, function(x) {
      if (nchar(x[1]) > 5) {
        return(NULL)
      } else {
        return(x[2])
      }
    })

*Possible answers:*

* *list(NULL, NULL, "1623", "1857")*
* *list("gauss", "bayes", NULL, NULL)*
* **list("1777", "1702", NULL, NULL)**
* *list("1777", "1702")*

**Wonderful! Feel free to experiment some more with your code in the console. Did you notice that** `lapply()` **always returns a list, no matter the input? This can be kind of annoying. In the next video tutorial you'll learn about** `sapply()` **to solve this.**

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 04 - Lecture 02 - sapply.mp4" type="video/mp4"/>

</div>

### How to use sapply

You can use `sapply()` similar to how you used `lapply()`. The first argument of `sapply()` is the list or vector `X` over which you want to apply a function, `FUN`. Potential additional arguments to this function are specified afterwards (`...`):

    sapply(X, FUN, ...)

In the next couple of exercises, you'll be working with the variable `temp`, that contains temperature measurements for 7 days. `temp` is a list of length 7, where each element is a vector of length 5, representing 5 measurements on a given day. This variable has already been defined in the workspace: type `str(temp)` to see its structure.

#### Instructions
* *Use* `lapply()` *to calculate the minimum (built-in function* `min()`*) of the temperature measurements for every day.*
* *Do the same thing but this time with* `sapply()`*. See how the output differs.*
* *Use* `lapply()` *to compute the the maximum (*`max()`*) temperature for each day.*
* *Again, use* `sapply()` *to solve the same question and see how* `lapply()` *and* `sapply()` *differ.*

```r
# Constructing temp variable
temp <- list(c(3, 7, 9, 6, -1), c(6, 9, 12, 13, 5), c(4, 8, 3, -1, -3), c(1, 4, 7, 2, -2), 
             c(5, 7, 9, 4, 2), c(-3, 5, 8, 9, 4), c(3, 6, 9, 4, 1))

# Use lapply() to find each day's minimum temperature
lapply(temp, min)
```

```
## [[1]]
## [1] -1
## 
## [[2]]
## [1] 5
## 
## [[3]]
## [1] -3
## 
## [[4]]
## [1] -2
## 
## [[5]]
## [1] 2
## 
## [[6]]
## [1] -3
## 
## [[7]]
## [1] 1
```

```r
# Use sapply() to find each day's minimum temperature
sapply(temp, min)
```

```
## [1] -1  5 -3 -2  2 -3  1
```

```r
# Use lapply() to find each day's maximum temperature
lapply(temp, max)
```

```
## [[1]]
## [1] 9
## 
## [[2]]
## [1] 13
## 
## [[3]]
## [1] 8
## 
## [[4]]
## [1] 7
## 
## [[5]]
## [1] 9
## 
## [[6]]
## [1] 9
## 
## [[7]]
## [1] 9
```

```r
# Use sapply() to find each day's maximum temperature
sapply(temp, max)
```

```
## [1]  9 13  8  7  9  9  9
```

**Nice! Can you tell the difference between the output of** `lapply()` **and** `sapply()`**? The former returns a list, while the latter returns a vector that is a simplified version of this list. Notice that this time, unlike in the cities example of the instructional video, the vector is not named.**

### sapply with your own function

Like `lapply()`, `sapply()` allows you to use self-defined functions and apply them over a vector or a list:

    sapply(X, FUN, ...)

Here, `FUN` can be one of R's built-in functions, but it can also be a function you wrote. This self-written function can be defined before hand, or can be inserted directly as an anonymous function.

#### Instructions
* *Finish the definition of* `extremes_avg()`*: it takes a vector of temperatures and calculates the average of the minimum and maximum temperatures of the vector.*
* *Next, use this function inside* `lapply()` *to apply it over the vectors inside* `temp`*.*
* *Use the same function over* `temp` *with* `sapply()` *and see how the outputs differ.*

```r
# temp is already defined in the workspace

# Finish function definition of extremes_avg
extremes_avg <- function(x) {
  (min(x) + max(x)) / 2
}

# Apply extremes_avg() over temp using lapply()
lapply(temp, extremes_avg)
```

```
## [[1]]
## [1] 4
## 
## [[2]]
## [1] 9
## 
## [[3]]
## [1] 2.5
## 
## [[4]]
## [1] 2.5
## 
## [[5]]
## [1] 5.5
## 
## [[6]]
## [1] 3
## 
## [[7]]
## [1] 5
```

```r
# Apply extremes_avg() over temp using sapply()
sapply(temp, extremes_avg)
```

```
## [1] 4.0 9.0 2.5 2.5 5.5 3.0 5.0
```

**Great job! Of course, you could have solved this exercise using an anonymous function, but this would require you to use the code inside the definition of** `extremes_avg()` **twice. Duplicating code should be avoided as much as possible!**

### sapply with function returning vector

In the previous exercises, you've seen how `sapply()` simplifies the list that `lapply()` would return by turning it into a vector. But what if the function you're applying over a list or a vector returns a vector of length greater than 1? If you don't remember from the video, don't waste more time in the valley of ignorance and head over to the instructions!

#### Instructions
* *Finish the definition of the* `extremes()` *function. It takes a vector of numerical values and returns a vector containing the minimum and maximum values of a given vector, with the names "min" and "max", respectively.*
* *Apply this function over the vector* `temp` *using* `lapply().`
* *Finally, apply this function over the vector* `temp` *using* `lapply()` *as well.*

```r
# temp is already available in the workspace

# Create a function that returns min and max of a vector: extremes
extremes <- function(x) {
  c(min = min(x), max = max(x))
}

# Apply extremes() over temp with lapply()
lapply(temp, extremes)
```

```
## [[1]]
## min max 
##  -1   9 
## 
## [[2]]
## min max 
##   5  13 
## 
## [[3]]
## min max 
##  -3   8 
## 
## [[4]]
## min max 
##  -2   7 
## 
## [[5]]
## min max 
##   2   9 
## 
## [[6]]
## min max 
##  -3   9 
## 
## [[7]]
## min max 
##   1   9
```

```r
# Apply extremes() over temp with sapply()
sapply(temp, extremes)
```

```
##     [,1] [,2] [,3] [,4] [,5] [,6] [,7]
## min   -1    5   -3   -2    2   -3    1
## max    9   13    8    7    9    9    9
```

**Wonderful! Have a final look at the console and see how** `sapply()` **did a great job at simplifying the rather uninformative 'list of vectors' that** `lapply()` **returns. It actually returned a nicely formatted matrix!**

### sapply can't simplify, now what?

It seems like we've hit the jackpot with `sapply()`. On all of the examples so far, `sapply()` was able to nicely simplify the rather bulky output of `lapply()`. But, as with life, there are things you can't simplify. How does `sapply()` react?

We already created a function, `below_zero()`, that takes a vector of numerical values and returns a vector that only contains the values that are strictly below zero.

#### Instructions
* *Apply* `below_zero()` *over* `temp` *using* `lapply()` *and store the result in* `freezing_s`*.*
* *Apply* `below_zero()` *over* `temp` *using* `sapply()`*. Save the resulting list in a variable* `freezing_l`*.*
* *Compare* `freezing_l` *to* `freezing_s` *using the* `identical()` *function.*

```r
# temp is already prepared for you in the workspace

# Definition of below_zero()
below_zero <- function(x) {
  return(x[x < 0])
}

# Apply below_zero over temp using lapply(): freezing_l
freezing_l <- lapply(temp, below_zero)

# Apply below_zero over temp using sapply(): freezing_s
freezing_s <- sapply(temp, below_zero)

# Are freezing_l and freezing_s identical?
identical(freezing_l, freezing_s)
```

```
## [1] TRUE
```

**Nice one! Given that the length of the output of** `below_zero()` **changes for different input vectors,** `sapply()` **is not able to nicely convert the output of** `lapply()` **to a nicely formatted matrix. Instead, the output values of** `sapply()` **and** `lapply()` **are exactly the same, as shown by the** `TRUE` **output of** `identical()`**.**

### sapply with functions that return NULL

You already have some apply tricks under your sleeve, but you're surely hungry for some more, aren't you? In this exercise, you'll see how `sapply()` reacts when it is used to apply a function that returns `NULL` over a vector or a list.

A function `print_info()`, that takes a vector and prints the average of this vector, has already been created for you. It uses the `cat()` function.

#### Instructions
* *Apply* `print_info()` *over the contents of* `temp` *with* `lapply()`*.*
* *Repeat this process with* `sapply()`*. Do you notice the difference?*

```r
# temp is already available in the workspace

# Definition of print_info()
print_info <- function(x) {
  cat("The average temperature is", mean(x), "\n")
}

# Apply print_info() over temp using lapply()
lapply(temp, print_info)
```

```
## The average temperature is 4.8 
## The average temperature is 9 
## The average temperature is 2.2 
## The average temperature is 2.4 
## The average temperature is 5.4 
## The average temperature is 4.6 
## The average temperature is 4.6
```

```
## [[1]]
## NULL
## 
## [[2]]
## NULL
## 
## [[3]]
## NULL
## 
## [[4]]
## NULL
## 
## [[5]]
## NULL
## 
## [[6]]
## NULL
## 
## [[7]]
## NULL
```

```r
# Apply print_info() over temp using sapply()
sapply(temp, print_info)
```

```
## The average temperature is 4.8 
## The average temperature is 9 
## The average temperature is 2.2 
## The average temperature is 2.4 
## The average temperature is 5.4 
## The average temperature is 4.6 
## The average temperature is 4.6
```

```
## [[1]]
## NULL
## 
## [[2]]
## NULL
## 
## [[3]]
## NULL
## 
## [[4]]
## NULL
## 
## [[5]]
## NULL
## 
## [[6]]
## NULL
## 
## [[7]]
## NULL
```

**Great! Notice here that, quite surprisingly,** `sapply()` **does not simplify the list of** `NULL`**'s. That's because the 'vector-version' of a list of** `NULL`**'s would simply be a** `NULL`**, which is no longer a vector with the same length as the input. Proceed to the next exercise.**

### Reverse engineering sapply
    
    sapply(list(runif (10), runif (10)), 
           function(x) c(min = min(x), mean = mean(x), max = max(x)))

Without going straight to the console to run the code, try to reason through which of the following statements are correct and why.

* (1) `sapply()` can't simplify the result that `lapply()` would return, and thus returns a list of vectors.  
* (2) This code generates a matrix with 3 rows and 2 columns.  
* (3) The function that is used inside `sapply()` is anonymous.  
* (4) The resulting data structure does not contain any names.  

Select the option that lists **all** correct statements.

*Possible answers:*

* *(1) and (3)*
* **(2) and (3)**
* *(1) and (4)*
* *(2), (3) and (4)*

**Great! This concludes the exercise set on** `sapply()`**. Head over to another video to learn all about** `vapply()`**!**

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 04 - Lecture 03 - vapply.mp4" type="video/mp4"/>

</div>

### Use vapply

Before you get your hands dirty with the third and last apply function that you'll learn about in this intermediate R course, let's take a look at its syntax. The function is called `vapply()`, and it has the following syntax:

    vapply(X, FUN, FUN.VALUE, ..., USE.NAMES = TRUE)

Over the elements inside `X`, the function `FUN` is applied. The `FUN.VALUE` argument expects a template for the return argument of this function `FUN`. `USE.NAMES` is `TRUE` by default; in this case `vapply()` tries to generate a named array, if possible.

For the next set of exercises, you'll be working on the `temp` list again, that contains 7 numerical vectors of length 5. We also coded a function `basics()` that takes a vector, and returns a named vector of length 3, containing the minimum, mean and maximum value of the vector respectively.

#### Instructions
*Apply the function* `basics()` *over the list of temperatures,* `temp`*, using* `vapply()`*. This time, you can use* `numeric(3)` *to specify the* `FUN.VALUE` *argument.*

```r
# temp is already available in the workspace

# Definition of basics()
basics <- function(x) {
  c(min = min(x), mean = mean(x), max = max(x))
}

# Apply basics() over temp using vapply()
vapply(temp, basics, numeric(3))
```

```
##      [,1] [,2] [,3] [,4] [,5] [,6] [,7]
## min  -1.0    5 -3.0 -2.0  2.0 -3.0  1.0
## mean  4.8    9  2.2  2.4  5.4  4.6  4.6
## max   9.0   13  8.0  7.0  9.0  9.0  9.0
```

**Perfect! Notice how, just as with** `sapply()`**,** `vapply()` **neatly transfers the names that you specify in the** `basics()` **function to the row names of the matrix that it returns.**

### Use vapply (2)

So far you've seen that `vapply()` mimics the behavior of `sapply()` if everything goes according to plan. But what if it doesn't?

In the video, Filip showed you that there are cases where the structure of the output of the function you want to apply, `FUN`, does not correspond to the template you specify in `FUN.VALUE`. In that case, `vapply()` will throw an error that informs you about the misalignment between expected and actual output.

#### Instructions
* *Inspect the code on the right and try to run it. If you haven't changed anything, an error should pop up. That's because* `vapply()` *still expects* `basics()` *to return a vector of length 3. The error message gives you an indication of what's wrong.*
* *Try to fix the error by editing the* `vapply()` *command.*

```r
# temp is already available in the workspace

# Definition of the basics() function
basics <- function(x) {
  c(min = min(x), mean = mean(x), median = median(x), max = max(x))
}

# Fix the error:
vapply(temp, basics, numeric(4))
```

```
##        [,1] [,2] [,3] [,4] [,5] [,6] [,7]
## min    -1.0    5 -3.0 -2.0  2.0 -3.0  1.0
## mean    4.8    9  2.2  2.4  5.4  4.6  4.6
## median  6.0    9  3.0  2.0  5.0  5.0  4.0
## max     9.0   13  8.0  7.0  9.0  9.0  9.0
```

**Great job! Head over to the next exercise.**

### From sapply to vapply

As highlighted before, `vapply()` can be considered a more robust version of `sapply()`, because you explicitly restrict the output of the function you want to apply. Converting your `sapply()` expressions in your own R scripts to `vapply()` expressions is therefore a good practice (and also a breeze!).

#### Instructions
*Convert all the* `sapply()` *expressions on the right to their* `vapply()` *counterparts. Their results should be exactly the same; you're only adding robustness. You'll need the templates* `numeric(1)` *and* `logical(1)`*.*

```r
# temp is already defined in the workspace

# Convert to vapply() expression
vapply(temp, max, numeric(1))
```

```
## [1]  9 13  8  7  9  9  9
```

```r
# Convert to vapply() expression
vapply(temp, function(x, y) { mean(x) > y }, y = 5, logical(1))
```

```
## [1] FALSE  TRUE FALSE FALSE  TRUE FALSE FALSE
```

**Great! You've got no more excuses to use** `sapply()` **in the future!**  
**You have finished the chapter "The apply family"!**
