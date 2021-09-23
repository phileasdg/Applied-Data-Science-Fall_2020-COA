---
title: "DataScience1-class_3"
author: "Phileas Dazeley Gaist"
date: "9/21/2021"
output: 
  html_document:
    keep_md: true
---
# # ---------------------------------------------------------------
# ┏━━━┓╋╋┏┓┏┓╋╋╋╋╋╋╋╋╋╋╋╋╋╋┏━┓╋┏┓┏┓╋╋╋╋╋┏━━━┓┏┓┏┓╋╋╋╋╋╋┏┓
# ┃┏━┓┃╋╋┃┃┃┃╋╋╋╋╋╋╋╋╋╋╋╋╋╋┃┏┛┏┛┗┫┃╋╋╋╋╋┃┏━┓┣┛┗┫┃╋╋╋╋╋┏┛┗┓
# ┃┃╋┗╋━━┫┃┃┃┏━━┳━━┳━━┓┏━━┳┛┗┓┗┓┏┫┗━┳━━┓┃┃╋┃┣┓┏┫┃┏━━┳━╋┓┏╋┳━━┓
# ┃┃╋┏┫┏┓┃┃┃┃┃┃━┫┏┓┃┃━┫┃┏┓┣┓┏┛╋┃┃┃┏┓┃┃━┫┃┗━┛┃┃┃┃┃┃┏┓┃┏┓┫┃┣┫┏━┛
# ┃┗━┛┃┗┛┃┗┫┗┫┃━┫┗┛┃┃━┫┃┗┛┃┃┃╋╋┃┗┫┃┃┃┃━┫┃┏━┓┃┃┗┫┗┫┏┓┃┃┃┃┗┫┃┗━┓
# ┗━━━┻━━┻━┻━┻━━┻━┓┣━━┛┗━━┛┗┛╋╋┗━┻┛┗┻━━┛┗┛╋┗┛┗━┻━┻┛┗┻┛┗┻━┻┻━━┛
# ╋╋╋╋╋╋╋╋╋╋╋╋╋╋┏━┛┃
# ╋╋╋╋╋╋╋╋╋╋╋╋╋╋┗━━┛       Applied Data Science I - Week 2, Class 1
# # ---------------------------------------------------------------




```r
# # ---------------------------------------------------------------
# Let's Practice Arithmetic 
# # ---------------------------------------------------------------

10 + 10 
```

```
## [1] 20
```

```r
2 - 1 
```

```
## [1] 1
```

```r
3 * 6 
```

```
## [1] 18
```

```r
2 / 7
```

```
## [1] 0.2857143
```

```r
2 ^ 5 
```

```
## [1] 32
```

```r
2 ** 5 
```

```
## [1] 32
```

```r
5 %% 2 
```

```
## [1] 1
```

```r
2 %/% 7 
```

```
## [1] 0
```

```r
1 / 1
```

```
## [1] 1
```

```r
1 / 0 # returns infinity instead of undefined
```

```
## [1] Inf
```

```r
0 / 0 # returns NaN (not a number)
```

```
## [1] NaN
```

```r
# All of the basic arithmetic operators 
# +	addition
# -	subtraction
# *	multiplication
# /	division
# ^ or **	exponentiation
# x %% y	modulus (x mod y) 5%%2 is 1
# x %/% y	integer division 5%/%2 is 2

# R uses a specific order of operations - BEDMAS (Brackets, Exponents, Division/Multiplication, Addition/Subtraction)
```


```r
# # ---------------------------------------------------------------
# Let's learn a couple of useful mathematical functions! 
# # ---------------------------------------------------------------

# Finds the sum of numbers or a series of numbers!
sum(2,3)
```

```
## [1] 5
```

```r
# Finds the absolute value of a number or series of numbers
abs(-15)
```

```
## [1] 15
```

```r
# Take the log! (the default base is 10, the natural logarithm)
log(10)
```

```
## [1] 2.302585
```

```r
# ...make sure you know which base you're working on!
log(x = 10, base = 10)
```

```
## [1] 1
```

```r
?log # any time you don't know how something works, this prompt takes you to the help doc for this function.
```

```
## starting httpd help server ... done
```

```r
# Same as above
log(10,10)
```

```
## [1] 1
```

```r
# Finds the exponential of a function
exp(2.3)
```

```
## [1] 9.974182
```

```r
?exp

# Find the square root of a number!
sqrt(9)
```

```
## [1] 3
```

```r
# Generate a sequence of numbers with : 

1:30
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
## [26] 26 27 28 29 30
```

```r
# Mix and match!

log(1:30, base = 2) # returns the log of every whole number between 1 and 30
```

```
##  [1] 0.000000 1.000000 1.584963 2.000000 2.321928 2.584963 2.807355 3.000000
##  [9] 3.169925 3.321928 3.459432 3.584963 3.700440 3.807355 3.906891 4.000000
## [17] 4.087463 4.169925 4.247928 4.321928 4.392317 4.459432 4.523562 4.584963
## [25] 4.643856 4.700440 4.754888 4.807355 4.857981 4.906891
```

```r
sqrt(sum(log(1:30), base = 2)) # returns the square root of the sum of the logarithms of every whole number between 1 and 30
```

```
## [1] 8.755469
```


```r
# # ---------------------------------------------------------------
# Let's Talk about Logic! 
# # ---------------------------------------------------------------

3 < 4 
```

```
## [1] TRUE
```

```r
5 <= 6
```

```
## [1] TRUE
```

```r
4 > 12 
```

```
## [1] FALSE
```

```r
3 >= 3
```

```
## [1] TRUE
```

```r
2 == 1 # are these things the same? evaluation operator
```

```
## [1] FALSE
```

```r
2 == 2 
```

```
## [1] TRUE
```

```r
# 2 = 2 # returns an error because it is an assignment operator
2 != 4
```

```
## [1] TRUE
```

```r
2+1i - 3+0i # complex and imaginary numbers
```

```
## [1] -1+1i
```

```r
# All of the basic logic operators 
# <	less than
# <=	less than or equal to
# >	greater than
# >=	greater than or equal to
# ==	exactly equal to
# !=	not equal to
# !x	Not x
#
# ... we'll talk more about these ones later
# x | y	x OR y
# x & y	x AND y
# isTRUE(x)	test if X is TRUE
```


```r
# # ---------------------------------------------------------------
# Let's Make Some ~v a r i a b l e s~
# # ---------------------------------------------------------------

# Why you shouldn't use the equals "=" sign in R, and you should instead use the "<-" sign: equals signs will work, but it's good practice not to use them in variable assignments, because the equals sign is always used in functions declarations.

# When you create a variable, it is recorded in your environment

my_age <- 35
philou_age <- 22
# This is a variable - which is also a vector of length one! 
my_age 
```

```
## [1] 35
```

```r
my_kids_ages <- c(4,7) # this is a vector, a container of objects that are all the same type. 

# This is a vector - of length two!
my_kids_ages
```

```
## [1] 4 7
```

```r
?c

c("Willa","Gideon") -> my_kids_names
my_kids_names
```

```
## [1] "Willa"  "Gideon"
```

```r
str(my_kids_names) # returns the structure of the object, in this case, a character class - [chr] - vector of length 2 - [1:2].
```

```
##  chr [1:2] "Willa" "Gideon"
```

```r
my_age * my_kids_ages
```

```
## [1] 140 245
```

```r
my_age + my_kids_ages
```

```
## [1] 39 42
```

```r
my_age^2
```

```
## [1] 1225
```

```r
# my_kids_names + my_kids_ages # this doesn't work because its asking to combine vectors of different types.

# you can combine vectors of different types into a dataframe:
# Create the data frame.
df <- data.frame(
   Age = my_kids_ages, 
   Names = my_kids_names
)

# to delete variables, you can do the following
rm(philou_age)
```


```r
# # ---------------------------------------------------------------
# Let's Talk about basic data types 
# # ---------------------------------------------------------------

# Numeric: Numbers that have a decimal value or are a fraction in nature have a data type as numeric.
class(my_age)
```

```
## [1] "numeric"
```

```r
class(my_kids_ages)
```

```
## [1] "numeric"
```

```r
# Character: As the name suggests, it can be a letter or a combination of letters enclosed by quotes is considered as a character data type by R. It can be alphabets or numbers. 
class(my_kids_names)
```

```
## [1] "character"
```

```r
# Integer: Integer: Numbers that do not contain decimal values have a data type as an integer. However, to create an integer data type, you explicitly use as.integer() and pass the variable as an argument.
class(as.integer(my_age)) # coerces the variable to be an integer
```

```
## [1] "integer"
```

```r
class(35L) # declares the variable to be an explicit integer. 
```

```
## [1] "integer"
```

```r
# Why L? Because it's 32 bits in length (so it's "long"). Also because i and l are too similar looking! 

# Logical: A variable that can have a value of True and False like a boolean is called a logical variable. 

my_age == 35
```

```
## [1] TRUE
```

```r
class(my_age == 35)
```

```
## [1] "logical"
```

```r
class(my_age == 25)
```

```
## [1] "logical"
```

```r
# Factor: They are a data type that is used to refer to a qualitative relationship like colors, good & bad, course or movie ratings, etc. They are useful in statistical modeling.

example <- factor(c("good", "bad", "ugly","good", "bad", "ugly"))
print(example)
```

```
## [1] good bad  ugly good bad  ugly
## Levels: bad good ugly
```

```r
class(example)
```

```
## [1] "factor"
```

```r
levels(example)
```

```
## [1] "bad"  "good" "ugly"
```

```r
nlevels(example)
```

```
## [1] 3
```

```r
class(levels(example))
```

```
## [1] "character"
```

```r
# Lists: These are a data type that is a collection of ... variables that basically don't have to be related to one another. Lists can be confusing, but powerful. 

kyle <- list(age = 35,
             nerd = TRUE,
             children = c("Willa","Gideon") 
)
kyle
```

```
## $age
## [1] 35
## 
## $nerd
## [1] TRUE
## 
## $children
## [1] "Willa"  "Gideon"
```

```r
class(kyle) 
```

```
## [1] "list"
```

```r
kyle$age # returns the age section of the kyle list
```

```
## [1] 35
```

```r
class(kyle$age) # returns the class of the elements inside the list
```

```
## [1] "numeric"
```

```r
# Data Frames: The real workhorses of R!

age <- c(17, 19, 21, 37, 18, 19, 47, 18, 19)
score <- c(12, 10, 11, 15, 16, 14, 25, 21, 29)
class_results <- data.frame(age,score) 
class_results
```

```
##   age score
## 1  17    12
## 2  19    10
## 3  21    11
## 4  37    15
## 5  18    16
## 6  19    14
## 7  47    25
## 8  18    21
## 9  19    29
```

```r
str(class_results)
```

```
## 'data.frame':	9 obs. of  2 variables:
##  $ age  : num  17 19 21 37 18 19 47 18 19
##  $ score: num  12 10 11 15 16 14 25 21 29
```

```r
class_results$age
```

```
## [1] 17 19 21 37 18 19 47 18 19
```

```r
names(class_results)
```

```
## [1] "age"   "score"
```



```r
# # ---------------------------------------------------------------
# Let's Talk about coercion 
# # ---------------------------------------------------------------

# my_kids_names + my_kids_ages # this doesn't work because its asking to combine vectors of different types.

# you can still put different vectors together, but R will implicitly coerce them into being the same type
my_kids <- c(my_kids_names,my_kids_ages)
# This is *implicit* coercion! (the numbers get coerced into being character)
str(my_kids)
```

```
##  chr [1:4] "Willa" "Gideon" "4" "7"
```

```r
my_kids
```

```
## [1] "Willa"  "Gideon" "4"      "7"
```

```r
my_kids <- data.frame(names = my_kids_names, ages = my_kids_ages)
my_kids
```

```
##    names ages
## 1  Willa    4
## 2 Gideon    7
```

```r
str(my_kids)
```

```
## 'data.frame':	2 obs. of  2 variables:
##  $ names: chr  "Willa" "Gideon"
##  $ ages : num  4 7
```

```r
# What is *explicit* coercion? When you explicitly want to force data to be read as a specific data type.

number_list <- 0:6
number_list
```

```
## [1] 0 1 2 3 4 5 6
```

```r
(as.logical(number_list))
```

```
## [1] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
```


```r
# # ---------------------------------------------------------------
# Let's go back to data frames and such ... 
# # ---------------------------------------------------------------

class_results
```

```
##   age score
## 1  17    12
## 2  19    10
## 3  21    11
## 4  37    15
## 5  18    16
## 6  19    14
## 7  47    25
## 8  18    21
## 9  19    29
```

```r
new_kid <- c(NA,22) # create a new observation to add to the data frame (NA class means that there is nothing there)

class_results <- rbind(class_results, new_kid) # example rbind

# rbind = binding rows, attaching rows to a dataframe
# cbind = binding columns, attaching columns to a dataframe

class_results
```

```
##    age score
## 1   17    12
## 2   19    10
## 3   21    11
## 4   37    15
## 5   18    16
## 6   19    14
## 7   47    25
## 8   18    21
## 9   19    29
## 10  NA    22
```

```r
is.na(class_results) # checks a data set for missing data (works well for small data sets)
```

```
##         age score
##  [1,] FALSE FALSE
##  [2,] FALSE FALSE
##  [3,] FALSE FALSE
##  [4,] FALSE FALSE
##  [5,] FALSE FALSE
##  [6,] FALSE FALSE
##  [7,] FALSE FALSE
##  [8,] FALSE FALSE
##  [9,] FALSE FALSE
## [10,]  TRUE FALSE
```

```r
sum(is.na(class_results)) # find the number of NAs in dataframe
```

```
## [1] 1
```

```r
complete.cases(class_results) # look across dataframes and see which rows aren't filled (works well for checking missing data in large dataframes)
```

```
##  [1]  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
```

```r
sum(!complete.cases(class_results)) # finds the number of incomplete rows in dataframe
```

```
## [1] 1
```

```r
sum(complete.cases(class_results)) # finds the number of complete rows in dataframe
```

```
## [1] 9
```


```r
# # ---------------------------------------------------------------
# Function declarations ... 
# # ---------------------------------------------------------------

summation <- function(vector){
  sum_total <- 0 
  for (i in series) {
     sum_total <- sum_total + i
  }
  return(sum_total)
}

series <- c(1,2,3,4,5,6,7,8,9,10)

summation(vector = series)
```

```
## [1] 55
```

