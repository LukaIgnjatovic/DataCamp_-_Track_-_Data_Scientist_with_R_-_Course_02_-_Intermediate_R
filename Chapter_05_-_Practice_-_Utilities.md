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

## Utilities

Mastering R programming is not only about understanding its programming concepts. Also a solid knowledge of a wide range of R functions is useful. This chapter introduces you to a bunch of useful functions for data structure manipulation, regular expressions and working with times and dates.

<div align="middle">

> **Document:** ["Slides - Utilities"](./Slides/Chapter 05 - Utilities.pdf)

</div>

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 05 - Lecture 01 - Useful functions.mp4" type="video/mp4"/>

</div>

### Mathematical utilities

Have another look at some useful math functions that R features:

* `abs()`: Calculate the absolute value.
* `sum()`: Calculate the sum of all the values in a data structure.
* `mean()`: Calculate the arithmetic mean.
* `round()`: Round the values to 0 decimal places by default. Try out `?round` in the console for variations of `round()` and ways to change the number of digits to round to.

As a data scientst in training, you've estimated a regression model on the sales data for the past six months. After evaluating your model, you see that the training error of your model is quite regular, showing both positive and negative values. The error values are already defined in the workspace on the right (`errors`).

#### Instructions
*Calculate the sum of the absolute rounded values of the training errors. You can work in parts, or with a single one-liner. There's no need to store the result in a variable, just have R print it.*

```r
# The errors vector has already been defined for you
errors <- c(1.9, -2.6, 4.0, -9.5, -3.4, 7.3)

# Sum of absolute rounded values of errors
sum(round(abs(errors)))
```

```
## [1] 29
```
**Great! Head over to the next exercise.**

### Find the error

We went ahead and included some code on the right, but there's still an error. Can you trace it and fix it?

In times of despair, help with functions such as `sum()` and `rev()` are a single command away; simply use `?sum` and `?rev` in the console.

#### Instructions
*Fix the error by including code on the last line. Remember: you want to call mean() only once!*

```r
# Don't edit these two lines
vec1 <- c(1.5, 2.5, 8.4, 3.7, 6.3)
vec2 <- rev(vec1)

# Fix the error
mean(abs(c(vec1, vec2)))
```

```
## [1] 4.48
```
**Nice work! If you check out the documentation of** `mean()`**, you'll see that only the first argument,** `x`**, should be a vector. If you also specify a second argument, R will match the arguments by position and expect a specification of the** `trim` **argument. Therefore, merging the two vectors is a must!**

### Data Utilities

R features a bunch of functions to juggle around with data structures:

* `seq()`: Generate sequences, by specifying the `from`, `to`, and `by` arguments.
* `rep()`: Replicate elements of vectors and lists.
* `sort()`: Sort a vector in ascending order. Works on numerics, but also on character strings and logicals.
* `rev()`: Reverse the elements in a data structures for which reversal is defined.
* `str()`: Display the structure of any R object.
* `append()`: Merge vectors or lists.
* `is.*()`: Check for the class of an R object.
* `as.*()`: Convert an R object from one class to another.
* `unlist()`: Flatten (possibly embedded) lists to produce a vector.

Remember the social media profile views data? Your LinkedIn and Facebook view counts for the last seven days are already defined as lists on the right.

#### Instructions
* *Convert both* `linkedin` *and* `facebook` *lists to a vector, and store them as* `li_vec` *and* `fb_vec` *respectively.*
* *Next, append* `fb_vec` *to the* `li_vec` *(Facebook data comes last). Save the result as* `social_vec`*.*
* *Finally, sort* `social_vec` *from high to low. Print the resulting vector.*

```r
# The linkedin and facebook lists have already been created for you
linkedin <- list(16, 9, 13, 5, 2, 17, 14)
facebook <- list(17, 7, 5, 16, 8, 13, 14)

# Convert linkedin and facebook to a vector: li_vec and fb_vec
li_vec <- unlist(linkedin)
fb_vec <- unlist(facebook)

# Append fb_vec to li_vec: social_vec
social_vec <- append(li_vec, fb_vec)

# Sort social_vec
sort(social_vec, decreasing = TRUE)
```

```
##  [1] 17 17 16 16 14 14 13 13  9  8  7  5  5  2
```
**Wonderful! These instructions required you to solve this challenge in a step-by-step approach. If you're comfortable with the functions, you can combine some of these steps into powerful one-liners.**

### Find the error (2)

Just as before, let's switch roles. It's up to you to see what unforgivable mistakes we've made. Go fix them!

#### Instructions
*Correct the expression. Make sure that your fix still uses the functions* `rep()` *and* `seq()`*.*

```r
# Fix me
rep(seq(1, 7, by = 2), times = 7)
```

```
##  [1] 1 3 5 7 1 3 5 7 1 3 5 7 1 3 5 7 1 3 5 7 1 3 5 7 1 3 5 7
```
**Wonderful! Debugging code is also a big part of the daily routine of a data scientist, and you seem to be great at it!**

### Beat Gauss using R

There is a popular story about young Gauss. As a pupil, he had a lazy teacher who wanted to keep the classroom busy by having them add up the numbers 1 to 100. Gauss came up with an answer almost instantaneously, 5050. On the spot, he had developed a formula for calculating the sum of an arithmetic series. There are more general formulas for calculating the sum of an arithmetic series with different starting values and increments. Instead of deriving such a formula, why not use R to calculate the sum of a sequence?

#### Instructions
* *Using the function* `seq()`*, create a sequence that ranges from 1 to 500 in increments of 3. Assign the resulting vector to a variable* `seq1`*.*
* *Again with the function* `seq()`*, create a sequence that ranges from 1200 to 900 in increments of -7. Assign it to a variable* `seq2`*.*
* *Calculate the total sum of the sequences, either by using the* `sum()` *function twice and adding the two results, or by first concatenating the sequences and then using the* `sum()` *function once. Print the result to the console.*

```r
# Create first sequence: seq1
seq1 <- seq(1, 500, by = 3)

# Create second sequence: seq2
seq2 <- seq(1200, 900, by = -7)

# Calculate total sum of the sequences
sum(c(seq1, seq2))
```

```
## [1] 87029
```
**Nice! Head over to the next video and learn more about regular expressions!**

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 05 - Lecture 02 - Regular expressions.mp4" type="video/mp4"/>

</div>

### grepl & grep

In their most basic form, regular expressions can be used to see whether a pattern exists inside a character string or a vector of character strings. For this purpose, you can use:

* `grepl()`, which returns `TRUE` when a pattern is found in the corresponding character string.
* `grep()`, which returns a vector of indices of the character strings that contains the pattern.

Both functions need a `pattern` and an `x` argument, where `pattern` is the regular expression you want to match for, and the `x` argument is the character vector from which matches should be sought.

In this and the following exercises, you'll be querying and manipulating a character vector of email addresses! The vector `emails` has already been defined in the editor on the right so you can begin with the instructions straight away!

#### Instructions
* *Use* `grepl()` *to generate a vector of logicals that indicates whether these email addressess contain* `"edu"`*. Print the result to the output.*
* *Do the same thing with* `grep()`*, but this time save the resulting indexes in a variable* `hits`*.*
* *Use the variable* `hits` *to select from the* `emails` *vector only the emails that contain* `"edu"`*.*

```r
# The emails vector has already been defined for you
emails <- c("john.doe@ivyleague.edu", 
            "education@world.gov", 
            "dalai.lama@peace.org",
            "invalid.edu", 
            "quant@bigdatacollege.edu", 
            "cookie.monster@sesame.tv")

# Use grepl() to match for "edu"
grepl("edu", emails)
```

```
## [1]  TRUE  TRUE FALSE  TRUE  TRUE FALSE
```

```r
# Use grep() to match for "edu", save result to hits
hits <- grep("edu", emails)

# Subset emails using hits
emails[hits]
```

```
## [1] "john.doe@ivyleague.edu"   "education@world.gov"     
## [3] "invalid.edu"              "quant@bigdatacollege.edu"
```
**Bellissimo! You can probably guess what we're trying to achieve here: select all the emails that end with ".edu". However, the strings** `education@world.gov` **and** `invalid.edu` **were also matched. Let's see in the next exercise what you can do to improve our pattern and remove these false positives.**

### grepl & grep (2)

You can use the caret, `^`, and the dollar sign, `$` to match the content located in the start and end of a string, respectively. This could take us one step closer to a correct pattern for matching only the ".edu" email addresses from our list of emails. But there's more that can be added to make the pattern more robust:

* `@`, because a valid email must contain an at-sign.
* `.*`, which matches any character (.) zero or more times (*). Both the dot and the asterisk are metacharacters. You can use them to match any character between the at-sign and the ".edu" portion of an email address.
* `\\.edu$`, to match the ".edu" part of the email at the end of the string. The `\\` part escapes the dot: it tells R that you want to use the `.` as an actual character.

#### Instructions
* *Use* `grepl()` *with the more advanced regular expression to return a logical vector. Simply print the result.*
* *Do a similar thing with* `grep()` *to create a vector of indices. Store the result in the variable* `hits`*.*
* *Use* `emails[hits]` *again to subset the emails vector.*

```r
# The emails vector has already been defined for you
emails <- c("john.doe@ivyleague.edu", 
            "education@world.gov", 
            "dalai.lama@peace.org",
            "invalid.edu", 
            "quant@bigdatacollege.edu", 
            "cookie.monster@sesame.tv")

# Use grepl() to match for .edu addresses more robustly
grepl("@.*\\.edu$", emails)
```

```
## [1]  TRUE FALSE FALSE FALSE  TRUE FALSE
```

```r
# Use grep() to match for .edu addresses more robustly, save result to hits
hits <- grep("@.*\\.edu$", emails)

# Subset emails using hits
emails[hits]
```

```
## [1] "john.doe@ivyleague.edu"   "quant@bigdatacollege.edu"
```
**Great! A careful construction of our regular expression leads to more meaningful matches. However, even our robust email selector will often match some incorrect email addresses (for instance kiara@@fakemail.edu). Let's not worry about this too much and continue with** `sub()` **and** `gsub()` **to actually edit the email addresses!**

### sub & gsub

While `grep()` and `grepl()` were used to simply check whether a regular expression could be matched with a character vector, `sub()` and `gsub()` take it one step further: you can specify a `replacement` argument. If inside the character vector `x`, the regular expression `pattern` is found, the matching element(s) will be replaced with `replacement`. `sub()` only replaces the first match, whereas `gsub()` replaces all matches.

Suppose that `emails` vector you've been working with is an excerpt of DataCamp's email database. Why not offer the owners of the .edu email addresses a new email address on the datacamp.edu domain? This could be quite a powerful marketing stunt: Online education is taking over traditional learning institutions! Convert your email and be a part of the new generation!

#### Instructions
*With the advanced regular expression* `"@.*\\.edu$"`*, use* `sub()` *to replace the match with* `"@datacamp.edu"`*. Since there will only be one match per character string,* `gsub()` *is not necessary here. Inspect the resulting output.*

```r
# The emails vector has already been defined for you
emails <- c("john.doe@ivyleague.edu", 
            "education@world.gov", 
            "global@peace.org",
            "invalid.edu", 
            "quant@bigdatacollege.edu", 
            "cookie.monster@sesame.tv")

# Use sub() to convert the email domains to datacamp.edu
sub("@.*\\.edu$", "@datacamp.edu", emails)
```

```
## [1] "john.doe@datacamp.edu"    "education@world.gov"     
## [3] "global@peace.org"         "invalid.edu"             
## [5] "quant@datacamp.edu"       "cookie.monster@sesame.tv"
```
**Awesome! Notice how only the valid .edu addresses are changed while the other emails remain unchanged. To get a taste of other things you can accomplish with regex, head over to the next exercise.**

### sub & gsub (2)

Regular expressions are a typical concept that you'll learn by doing and by seeing other examples. Before you rack your brains over the regular expression in this exercise, have a look at the new things that will be used:

* `.*`: A usual suspect! It can be read as "any character that is matched zero or more times".
* `\\s`: Match a space. The "s" is normally a character, escaping it (`\\`) makes it a metacharacter.
* `[0-9]+`: Match the numbers 0 to 9, at least once (+).
* `([0-9]+)`: The parentheses are used to make parts of the matching string available to define the replacement. The `\\1` in the `replacement` argument of `sub()` gets set to the string that is captured by the regular expression `[0-9]+`.  

What does this code chunk return: 

    awards <- c("Won 1 Oscar.", 
                "Won 1 Oscar. Another 9 wins & 24 nominations.", 
                "1 win and 2 nominations.", 
                "2 wins & 3 nominations.", 
                "Nominated for 2 Golden Globes. 1 more win & 2 nominations.", 
                "4 wins & 1 nomination.")
    
    sub(".*\\s([0-9]+)\\snomination.*$", "\\1", awards)

`awards` is already defined in the workspace so you can start playing in the console straight away.

*Possible answers:*

* *A vector of integers containing: 1, 24, 2, 3, 2, 1.*
* *The* `vector` *awards gets returned as there isn't a single element in* `awards` *that matches the regular expression.*
* *A vector of character strings containing "1", "24", "2", "3", "2", "1".*
* **A vector of character strings containing "Won 1 Oscar.", "24", "2", "3", "2", "1".**

**Great! Can you explain why all of this happened? The** `([0-9]+)` **selects the entire number that comes before the word "nomination" in the string, and the entire match gets replaced by this number because of the** `\\1` **that reference to the content inside the parentheses. The next video will get you up to speed with times and dates in R!**

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 05 - Lecture 03 - Times and dates.mp4" type="video/mp4"/>

</div>

### Right here, right now

In R, dates are represented by `Date` objects, while times are represented by `POSIXct` objects. Under the hood, however, these dates and times are simple numerical values. `Date` objects store the number of days since the 1st of January in 1970. `POSIXct` objects on the other hand, store the number of seconds since the 1st of January in 1970.

The 1st of January in 1970 is the common origin for representing times and dates in a wide range of programming languages. There is no particular reason for this; it is a simple convention. Of course, it's also possible to create dates and times before 1970; the corresponding numerical values are simply negative in this case.

#### Instructions
*Ask R for the current date, and store the result in a variable* `today`*.*
*To see what* `today` *looks like under the hood, call* `unclass()` *on it.*
*Ask R for the current time, and store the result in a variable,* `now`*.*
*To see the numerical value that corresponds to* `now`*, call* `unclass()` *on it.*

```r
# Get the current date: today
today <- Sys.Date()

# See what today looks like under the hood
unclass(today)
```

```
## [1] 17806
```

```r
# Get the current time: now
now <- Sys.time()

# See what now looks like under the hood
unclass(now)
```

```
## [1] 1538479089
```
**Great! Using R to get the current date and time is nice, but you should also know how to create dates and times from character strings. Find out how in the next exercises!**

### Create and format dates

To create a `Date` object from a simple character string in R, you can use the `as.Date()` function. The character string has to obey a format that can be defined using a set of symbols (the examples correspond to 13 January, 1982):

* `%Y`: 4-digit year (1982)
* `%y`: 2-digit year (82)
* `%m`: 2-digit month (01)
* `%d`: 2-digit day of the month (13)
* `%A`: weekday (Wednesday)
* `%a`: abbreviated weekday (Wed)
* `%B`: month (January)
* `%b`: abbreviated month (Jan)

The following R commands will all create the same `Date` object for the 13th day in January of 1982:

    as.Date("1982-01-13")
    as.Date("Jan-13-82", format = "%b-%d-%y")
    as.Date("13 January, 1982", format = "%d %B, %Y")

Notice that the first line here did not need a format argument, because by default R matches your character string to the formats `"%Y-%m-%d"` or `"%Y/%m/%d"`.

In addition to creating dates, you can also convert dates to character strings that use a different date notation. For this, you use the `format()` function. Try the following lines of code:

    today <- Sys.Date()
    format(Sys.Date(), format = "%d %B, %Y")
    format(Sys.Date(), format = "Today is a %A!")

#### Instructions
* *In the editor on the right, three character strings representing dates have been created. Convert them to dates using* `as.Date()`*, and assign them to* `date1`*,* `date2`*, and* `date3` *respectively. The code for* `date1` *is already included.*
* *Extract useful information from the dates as character strings using* `format()`*. From the first date, select the weekday. From the second date, select the day of the month. From the third date, you should select the abbreviated month and the 4-digit year, separated by a space.*

```r
# Definition of character strings representing dates
str1 <- "May 23, '96"
str2 <- "2012-03-15"
str3 <- "30/January/2006"

# Convert the strings to dates: date1, date2, date3
date1 <- as.Date(str1, format = "%b %d, '%y")
date2 <- as.Date(str2)
date3 <- as.Date(str3, format = "%d/%B/%Y")

# Convert dates to formatted strings
format(date1, "%A")
```

```
## [1] "Thursday"
```

```r
format(date2, "%d")
```

```
## [1] "15"
```

```r
format(date3, "%b %Y")
```

```
## [1] "Jan 2006"
```
**You're a date magician! You can use** `POSIXct` **objects, i.e. Time objects in R, in a similar fashion. Give it a try in the next exercise.**

### Create and format times

Similar to working with dates, you can use `as.POSIXct()` to convert from a character string to a `POSIXct` object, and `format()` to convert from a `POSIXct` object to a character string. Again, you have a wide variety of symbols:

* `%H`: hours as a decimal number (00-23)
* `%I`: hours as a decimal number (01-12)
* `%M`: minutes as a decimal number
* `%S`: seconds as a decimal number
* `%T`: shorthand notation for the typical format `%H:%M:%S`
* `%p`: AM/PM indicator

For a full list of conversion symbols, consult the strptime documentation in the console:

    ?strptime

Again, `as.POSIXct()` uses a default format to match character strings. In this case, it's `%Y-%m-%d %H:%M:%S`. In this exercise, abstraction is made of different time zones.

#### Instructions
* *Convert two strings that represent timestamps,* `str1` *and* `str2`*, to* `POSIXct` *objects called* `time1` *and* `time2`*.*
* *Using* `format()`*, create a string from* `time1` *containing only the minutes.*
* *From* `time2`*, extract the hours and minutes as "hours:minutes AM/PM". Refer to the assignment text above to find the correct conversion symbols!*

```r
# Definition of character strings representing times
str1 <- "May 23, '96 hours:23 minutes:01 seconds:45"
str2 <- "2012-3-12 14:23:08"

# Convert the strings to POSIXct objects: time1, time2
time1 <- as.POSIXct(str1, format = "%B %d, '%y hours:%H minutes:%M seconds:%S")
time2 <- as.POSIXct(str2)

# Convert times to formatted strings
format(time1, "%M")
```

```
## [1] "01"
```

```r
format(time2, "%I:%M %p")
```

```
## [1] "02:23 PM"
```
**Great!**

### Calculations with Dates

Both `Date` and `POSIXct` R objects are represented by simple numerical values under the hood. This makes calculation with time and date objects very straightforward: R performs the calculations using the underlying numerical values, and then converts the result back to human-readable time information again.

You can increment and decrement `Date` objects, or do actual calculations with them (try it out in the console!):

    today <- Sys.Date()
    today + 1
    today - 1

    as.Date("2015-03-12") - as.Date("2015-02-27")

To control your eating habits, you decided to write down the dates of the last five days that you ate pizza. In the workspace, these dates are defined as five `Date` objects, `day1` to `day5`. The code on the right also contains a vector `pizza` with these 5 `Date` objects.

#### Instructions
* *Calculate the number of days that passed between the last and the first day you ate pizza. Print the result.*
* *Use the function* `diff()` *on pizza to calculate the differences between consecutive pizza days. Store the result in a new variable* `day_diff`*.*
* *Calculate the average period between two consecutive pizza days. Print the result.*

```r
# Constructing day1, day2, day3, day4 and day5 vectors
day1 <- as.Date("2016-11-21")
day2 <- as.Date("2016-11-16")
day3 <- as.Date("2016-11-27")
day4 <- as.Date("2016-11-14")
day5 <- as.Date("2016-12-02")

# Difference between last and first pizza day
day5-day1
```

```
## Time difference of 11 days
```

```r
# Create vector pizza
pizza <- c(day1, day2, day3, day4, day5)

# Create differences between consecutive pizza days: day_diff
day_diff <- diff(pizza, lag = 1, differences = 1)
day_diff
```

```
## Time differences in days
## [1]  -5  11 -13  18
```

```r
# Average period between two consecutive pizza days
print(mean(day_diff))
```

```
## Time difference of 2.75 days
```
**Great! Head over to the next exercise.**

### Calculations with Times

Calculations using `POSIXct` objects are completely analogous to those using `Date` objects. Try to experiment with this code to increase or decrease `POSIXct` objects:

    now <- Sys.time()
    now + 3600          # add an hour
    now - 3600 * 24     # subtract a day

Adding or substracting time objects is also straightforward:

    birth <- as.POSIXct("1879-03-14 14:37:23")
    death <- as.POSIXct("1955-04-18 03:47:12")
    einstein <- death - birth
    einstein

You're developing a website that requires users to log in and out. You want to know what is the total and average amount of time a particular user spends on your website. This user has logged in 5 times and logged out 5 times as well. These times are gathered in the vectors `login` and `logout`, which are already defined in the workspace.

#### Instructions
* *Calculate the difference between the two vectors* `logout` *and* `login`*, i.e. the time the user was online in each independent session. Store the result in a variable* `time_online`*.*
* *Inspect the variable* `time_online` *by printing it.*
* *Calculate the total time that the user was online. Print the result.*
* *Calculate the average time the user was online. Print the result.*

```r
# Constructing login and logout vectors
login <- as.POSIXct(c("2016-11-18 10:18:04 UTC", 
                      "2016-11-23 09:14:18 UTC", 
                      "2016-11-23 12:21:51 UTC", 
                      "2016-11-23 12:37:24 UTC", 
                      "2016-11-25 21:37:55 UTC"))

logout <- as.POSIXct(c("2016-11-18 10:56:29 UTC", 
                       "2016-11-23 09:14:52 UTC", 
                       "2016-11-23 12:35:48 UTC",
                       "2016-11-23 13:17:22 UTC", 
                       "2016-11-25 22:08:47 UTC"))

# Calculate the difference between login and logout: time_online
time_online <- logout - login

# Inspect the variable time_online
time_online
```

```
## Time differences in secs
## [1] 2305   34  837 2398 1852
```

```r
# Calculate the total time online
sum(time_online)
```

```
## Time difference of 7426 secs
```

```r
# Calculate the average time online
mean(time_online)
```

```
## Time difference of 1485.2 secs
```
**Great! Time to tackle the final exercise of this course!**

### Time is of the essence

The dates when a season begins and ends can vary depending on who you ask. People in Australia will tell you that spring starts on September 1st. The Irish people in the Northern hemisphere will swear that spring starts on February 1st, with the celebration of St. Brigid's Day. Then there's also the difference between astronomical and meteorological seasons: while astronomers are used to equinoxes and solstices, meteorologists divide the year into 4 fixed seasons that are each three months long. (Source: [Time and Date](http://www.timeanddate.com))

A vector `astro`, which contains character strings representing the dates on which the 4 astronomical seasons start, has been defined on your workspace. Similarly, a vector `meteo` has already been created for you, with the meteorological beginnings of a season.

#### Instructions
* *Use *`as.Date()` *to convert the astro vector to a vector containing* `Date` *objects. You will need the* `%d`*,* `%b` *and* `%Y` *symbols to specify the* `format`*. Store the resulting vector as* `astro_dates`*.*
* *Use* `as.Date()` *to convert the* `meteo` *vector to a vector with* `Date` *objects. This time, you will need the* `%B`*,* `%d` *and* `%y` *symbols for the* `format` *argument. Store the resulting vector as* `meteo_dates`*.*
* *With a combination of* `max()`*,* `abs()` *and* `-`*, calculate the maximum absolute difference between the astronomical and the meteorological beginnings of a season, i.e.* `astro_dates` *and* `meteo_dates`*. Simply print this maximum difference to the console output.*

```r
# Constructing astro and meteo vectors
astro <- c("20-Mar-2015", "25-Jun-2015", "23-Sep-2015", "22-Dec-2015")
names(astro) <- c("spring", "summer", "fall", "winter")

meteo <- c("March 1, 15", "June 1, 15", "September 1, 15", "December 1, 15")
names(meteo) <- c("spring", "summer", "fall", "winter")

# Convert astro to vector of Date objects: astro_dates
astro_dates <- as.Date(astro, format = "%d-%b-%Y")

# Convert meteo to vector of Date objects: meteo_dates
meteo_dates <- as.Date(meteo, format = "%B %d, %y")

# Calculate the maximum absolute difference between astro_dates and meteo_dates
max(abs(astro_dates - meteo_dates))
```

```
## Time difference of 24 days
```
**Impressive! Great job on finishing this course!**  
**You have finished the chapter "Utilities"!**
