---
title: "week 3 - class 2 - Intro to R"
author: "Phileas Dazeley Gaist"
date: "10/1/2021"
output: 
  html_document:
    keep_md: true
---


```r
# # ---------------------------------------------------------------
# ┏━━━┓╋╋┏┓┏┓╋╋╋╋╋╋╋╋╋╋╋╋╋╋┏━┓╋┏┓┏┓╋╋╋╋╋┏━━━┓┏┓┏┓╋╋╋╋╋╋┏┓
# ┃┏━┓┃╋╋┃┃┃┃╋╋╋╋╋╋╋╋╋╋╋╋╋╋┃┏┛┏┛┗┫┃╋╋╋╋╋┃┏━┓┣┛┗┫┃╋╋╋╋╋┏┛┗┓
# ┃┃╋┗╋━━┫┃┃┃┏━━┳━━┳━━┓┏━━┳┛┗┓┗┓┏┫┗━┳━━┓┃┃╋┃┣┓┏┫┃┏━━┳━╋┓┏╋┳━━┓
# ┃┃╋┏┫┏┓┃┃┃┃┃┃━┫┏┓┃┃━┫┃┏┓┣┓┏┛╋┃┃┃┏┓┃┃━┫┃┗━┛┃┃┃┃┃┃┏┓┃┏┓┫┃┣┫┏━┛
# ┃┗━┛┃┗┛┃┗┫┗┫┃━┫┗┛┃┃━┫┃┗┛┃┃┃╋╋┃┗┫┃┃┃┃━┫┃┏━┓┃┃┗┫┗┫┏┓┃┃┃┃┗┫┃┗━┓
# ┗━━━┻━━┻━┻━┻━━┻━┓┣━━┛┗━━┛┗┛╋╋┗━┻┛┗┻━━┛┗┛╋┗┛┗━┻━┻┛┗┻┛┗┻━┻┻━━┛
# ╋╋╋╋╋╋╋╋╋╋╋╋╋╋┏━┛┃
# ╋╋╋╋╋╋╋╋╋╋╋╋╋╋┗━━┛       Applied Data Science I - Week 3, Class 2
# # ---------------------------------------------------------------
```



**What makes a data set tidy ?**

- Every column in a data set is a variable
- Every row is an observation
- Every cell is a distinct element (perfect grid)

Often, "untidy" formats are super simple for data entry and collection. 

You'll use pivot longer a lot to prepare data to plot.
You'll use pivot wider a lot when you need to prepare data for analysis, tidy things up. 


```r
# Today we are going to learn about just TWO verbs!
#
# "pivot_wider" and "pivot_longer"
# 
# We're also going to reinforce the tidy data principles - namely, a dataset is tidy IF and ONLY IF: 
# 
# Every column is a VARIABLE
# Every row is an OBSERVATION
# Every cell is a SINGLE VALUE 

# ---------------------------------------------------------------
# Verb #1: pivot_longer()
# ---------------------------------------------------------------

library(tidyverse)
```

```
## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --
```

```
## v ggplot2 3.3.5     v purrr   0.3.4
## v tibble  3.1.4     v dplyr   1.0.7
## v tidyr   1.1.3     v stringr 1.4.0
## v readr   2.0.1     v forcats 0.5.1
```

```
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
data("relig_income")
relig_income
```

```
## # A tibble: 18 x 11
##    religion `<$10k` `$10-20k` `$20-30k` `$30-40k` `$40-50k` `$50-75k` `$75-100k`
##    <chr>      <dbl>     <dbl>     <dbl>     <dbl>     <dbl>     <dbl>      <dbl>
##  1 Agnostic      27        34        60        81        76       137        122
##  2 Atheist       12        27        37        52        35        70         73
##  3 Buddhist      27        21        30        34        33        58         62
##  4 Catholic     418       617       732       670       638      1116        949
##  5 Don’t k~      15        14        15        11        10        35         21
##  6 Evangel~     575       869      1064       982       881      1486        949
##  7 Hindu          1         9         7         9        11        34         47
##  8 Histori~     228       244       236       238       197       223        131
##  9 Jehovah~      20        27        24        24        21        30         15
## 10 Jewish        19        19        25        25        30        95         69
## 11 Mainlin~     289       495       619       655       651      1107        939
## 12 Mormon        29        40        48        51        56       112         85
## 13 Muslim         6         7         9        10         9        23         16
## 14 Orthodox      13        17        23        32        32        47         38
## 15 Other C~       9         7        11        13        13        14         18
## 16 Other F~      20        33        40        46        49        63         46
## 17 Other W~       5         2         3         4         2         7          3
## 18 Unaffil~     217       299       374       365       341       528        407
## # ... with 3 more variables: $100-150k <dbl>, >150k <dbl>,
## #   Don't know/refused <dbl>
```

```r
# What makes this dataset untidy?
# ...
# ...
# The column names are are VALUES, not VARIABLES 

# What if I wanted to know how many people identified as agnostic in this dataset? 

sum(relig_income[1,2:11])
```

```
## [1] 826
```

```r
# What if I wanted to know how many people identified as agnostic OR atheist but NOT catholic and made at least 75k a year? 
# ...it would be annoying!
# So let's tidy this data up! 

relig_income %>% 
  pivot_longer(!religion, names_to = "income", values_to = "count")
```

```
## # A tibble: 180 x 3
##    religion income             count
##    <chr>    <chr>              <dbl>
##  1 Agnostic <$10k                 27
##  2 Agnostic $10-20k               34
##  3 Agnostic $20-30k               60
##  4 Agnostic $30-40k               81
##  5 Agnostic $40-50k               76
##  6 Agnostic $50-75k              137
##  7 Agnostic $75-100k             122
##  8 Agnostic $100-150k            109
##  9 Agnostic >150k                 84
## 10 Agnostic Don't know/refused    96
## # ... with 170 more rows
```

```r
# translation: ignore the religion column, 
# take all values from every column and make a single column called income with every row containing income values for each religious group.
# take all count values from the input data set and put them in a single new column called "count" 

# Let's actually answer the question above 

relig_income %>% 
  pivot_longer(!religion, names_to = 'income', values_to = 'count') %>% 
  filter(religion != 'Catholic' & religion %in% c('Agnostic','Atheist'),
         income %in% c('$75-100k','$100-150k')) %>%
  summarize(count = sum(count))
```

```
## # A tibble: 1 x 1
##   count
##   <dbl>
## 1   363
```


```r
# ---------------------------------------------------------------
# Verb #2: pivot_wider
# ---------------------------------------------------------------

data(us_rent_income)
us_rent_income
```

```
## # A tibble: 104 x 5
##    GEOID NAME       variable estimate   moe
##    <chr> <chr>      <chr>       <dbl> <dbl>
##  1 01    Alabama    income      24476   136
##  2 01    Alabama    rent          747     3
##  3 02    Alaska     income      32940   508
##  4 02    Alaska     rent         1200    13
##  5 04    Arizona    income      27517   148
##  6 04    Arizona    rent          972     4
##  7 05    Arkansas   income      23789   165
##  8 05    Arkansas   rent          709     5
##  9 06    California income      29454   109
## 10 06    California rent         1358     3
## # ... with 94 more rows
```

```r
# hmmmm, this is not tidy! Let's tidy it up. 

us_rent_income %>%
  pivot_wider(names_from = variable, values_from = c(estimate, moe))
```

```
## # A tibble: 52 x 6
##    GEOID NAME                 estimate_income estimate_rent moe_income moe_rent
##    <chr> <chr>                          <dbl>         <dbl>      <dbl>    <dbl>
##  1 01    Alabama                        24476           747        136        3
##  2 02    Alaska                         32940          1200        508       13
##  3 04    Arizona                        27517           972        148        4
##  4 05    Arkansas                       23789           709        165        5
##  5 06    California                     29454          1358        109        3
##  6 08    Colorado                       32401          1125        109        5
##  7 09    Connecticut                    35326          1123        195        5
##  8 10    Delaware                       31560          1076        247       10
##  9 11    District of Columbia           43198          1424        681       17
## 10 12    Florida                        25952          1077         70        3
## # ... with 42 more rows
```

```r
# now we can answer questions about it!
```


```r
# ---------------------------------------------------------------
# General Tidy Data Practice! 
# ---------------------------------------------------------------

data(billboard)
billboard
```

```
## # A tibble: 317 x 79
##    artist   track   date.entered   wk1   wk2   wk3   wk4   wk5   wk6   wk7   wk8
##    <chr>    <chr>   <date>       <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1 2 Pac    Baby D~ 2000-02-26      87    82    72    77    87    94    99    NA
##  2 2Ge+her  The Ha~ 2000-09-02      91    87    92    NA    NA    NA    NA    NA
##  3 3 Doors~ Krypto~ 2000-04-08      81    70    68    67    66    57    54    53
##  4 3 Doors~ Loser   2000-10-21      76    76    72    69    67    65    55    59
##  5 504 Boyz Wobble~ 2000-04-15      57    34    25    17    17    31    36    49
##  6 98^0     Give M~ 2000-08-19      51    39    34    26    26    19     2     2
##  7 A*Teens  Dancin~ 2000-07-08      97    97    96    95   100    NA    NA    NA
##  8 Aaliyah  I Don'~ 2000-01-29      84    62    51    41    38    35    35    38
##  9 Aaliyah  Try Ag~ 2000-03-18      59    53    38    28    21    18    16    14
## 10 Adams, ~ Open M~ 2000-08-26      76    76    74    69    68    67    61    58
## # ... with 307 more rows, and 68 more variables: wk9 <dbl>, wk10 <dbl>,
## #   wk11 <dbl>, wk12 <dbl>, wk13 <dbl>, wk14 <dbl>, wk15 <dbl>, wk16 <dbl>,
## #   wk17 <dbl>, wk18 <dbl>, wk19 <dbl>, wk20 <dbl>, wk21 <dbl>, wk22 <dbl>,
## #   wk23 <dbl>, wk24 <dbl>, wk25 <dbl>, wk26 <dbl>, wk27 <dbl>, wk28 <dbl>,
## #   wk29 <dbl>, wk30 <dbl>, wk31 <dbl>, wk32 <dbl>, wk33 <dbl>, wk34 <dbl>,
## #   wk35 <dbl>, wk36 <dbl>, wk37 <dbl>, wk38 <dbl>, wk39 <dbl>, wk40 <dbl>,
## #   wk41 <dbl>, wk42 <dbl>, wk43 <dbl>, wk44 <dbl>, wk45 <dbl>, wk46 <dbl>, ...
```

```r
# Let's clean this up! 

billboard %>% 
  pivot_longer(
    wk1:wk76
  )
```

```
## # A tibble: 24,092 x 5
##    artist track                   date.entered name  value
##    <chr>  <chr>                   <date>       <chr> <dbl>
##  1 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk1      87
##  2 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk2      82
##  3 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk3      72
##  4 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk4      77
##  5 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk5      87
##  6 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk6      94
##  7 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk7      99
##  8 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk8      NA
##  9 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk9      NA
## 10 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk10     NA
## # ... with 24,082 more rows
```

```r
billboard %>% 
  pivot_longer(
    # this identifies which rows we want to pivot!
    wk1:wk76, 
    # this tells us the new name of the column
    names_to = "week", 
    # this tells us which values to focus on!
    values_to = "rank"
  )
```

```
## # A tibble: 24,092 x 5
##    artist track                   date.entered week   rank
##    <chr>  <chr>                   <date>       <chr> <dbl>
##  1 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk1      87
##  2 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk2      82
##  3 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk3      72
##  4 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk4      77
##  5 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk5      87
##  6 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk6      94
##  7 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk7      99
##  8 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk8      NA
##  9 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk9      NA
## 10 2 Pac  Baby Don't Cry (Keep... 2000-02-26   wk10     NA
## # ... with 24,082 more rows
```

```r
# That's much better! Let's go even a little farther ...

billboard_cleaned <- billboard %>% 
  pivot_longer(
    wk1:wk76, 
    names_to = "week", 
    values_to = "rank", 
    values_drop_na = TRUE
  ) %>% 
  mutate(
    # this cleans up the "week" column and turns it into an integer - helpful for ordering! 
    week = as.integer(gsub("wk", "", week)),
    # this makes sure that the "date.entered" column becomes a date! 
    date = as.Date(date.entered) + 7 * (week - 1),
  ) %>% 
  # this drops the now unnecessary date column! 
  select(-date.entered)

# Let's answer a couple of questions about the data:

# Which artists had the best average rank in this data set?

billboard_cleaned %>% 
  group_by(artist) %>% 
  summarise(avg_by_artist = mean(rank)) %>% 
  arrange(avg_by_artist)
```

```
## # A tibble: 228 x 2
##    artist                           avg_by_artist
##    <chr>                                    <dbl>
##  1 "Santana"                                 10.5
##  2 "Elliott, Missy \"Misdemeanor\""          14.3
##  3 "matchbox twenty"                         18.6
##  4 "N'Sync"                                  18.6
##  5 "Janet"                                   19.4
##  6 "Destiny's Child"                         19.8
##  7 "Ruff Endz"                               19.9
##  8 "Pink"                                    20.1
##  9 "Aguilera, Christina"                     21.1
## 10 "Madonna"                                 21.5
## # ... with 218 more rows
```

```r
# Which artist was in the charts for the longest time?

billboard_cleaned %>% 
  group_by(artist) %>% 
  summarise(count = n()) %>% 
  arrange(desc(count)) 
```

```
## # A tibble: 228 x 2
##    artist              count
##    <chr>               <int>
##  1 Creed                 104
##  2 Lonestar               95
##  3 Destiny's Child        92
##  4 N'Sync                 74
##  5 Sisqo                  74
##  6 3 Doors Down           73
##  7 Jay-Z                  73
##  8 Aguilera, Christina    67
##  9 Hill, Faith            67
## 10 Houston, Whitney       67
## # ... with 218 more rows
```

```r
# Which artist has the largest number of songs on the billboard?

billboard_cleaned %>% 
  group_by(artist, track) %>% 
  summarise(count = n()) %>% 
  arrange(desc(count)) %>% 
  ungroup() %>% # Yes, you can ungroup things in the tidyverse.
  group_by(artist) %>% 
  summarise(count = n()) %>% 
  arrange(desc(count))
```

```
## `summarise()` has grouped output by 'artist'. You can override using the `.groups` argument.
```

```
## # A tibble: 228 x 2
##    artist               count
##    <chr>                <int>
##  1 Jay-Z                    5
##  2 Dixie Chicks, The        4
##  3 Houston, Whitney         4
##  4 Aguilera, Christina      3
##  5 Backstreet Boys, The     3
##  6 Braxton, Toni            3
##  7 Destiny's Child          3
##  8 DMX                      3
##  9 Eminem                   3
## 10 Jackson, Alan            3
## # ... with 218 more rows
```

```r
billboard_cleaned %>% 
  group_by(artist) %>% 
  summarise(count = n()) %>% 
  arrange(desc(count))
```

```
## # A tibble: 228 x 2
##    artist              count
##    <chr>               <int>
##  1 Creed                 104
##  2 Lonestar               95
##  3 Destiny's Child        92
##  4 N'Sync                 74
##  5 Sisqo                  74
##  6 3 Doors Down           73
##  7 Jay-Z                  73
##  8 Aguilera, Christina    67
##  9 Hill, Faith            67
## 10 Houston, Whitney       67
## # ... with 218 more rows
```

```r
# How many songs are there by Jay-Z?

billboard_cleaned %>% 
  filter(artist == "Jay-Z") %>% 
  select(track) %>% 
  distinct()
```

```
## # A tibble: 5 x 1
##   track                  
##   <chr>                  
## 1 Anything               
## 2 Big Pimpin'            
## 3 Do It Again (Put Ya ...
## 4 Hey Papi               
## 5 I Just Wanna Love U ...
```

**gsub function:** gsub(pattern, thing you want to replace pattern with, vector of strings that you want to replace things in)


```r
# ---------------------------------------------------------------
# Let's practice some more! 
# ---------------------------------------------------------------

devtools::install_github("uc-cfss/rcfss")
```

```
## WARNING: Rtools is required to build R packages, but is not currently installed.
## 
## Please download and install Rtools 4.0 from https://cran.r-project.org/bin/windows/Rtools/.
```

```
## Skipping install of 'rcfss' from a github remote, the SHA1 (5b60f614) has not changed since last install.
##   Use `force = TRUE` to force installation
```

```r
library(rcfss)


data(grades)

# what's wrong with this dataset? 

# one way to fix it! 

grades %>% 
  pivot_longer(
    Fall:Winter,
    names_to = "Season",
    values_to = "Score"
  )
```

```
## # A tibble: 36 x 5
##       ID Test     Year Season Score
##    <dbl> <chr>   <dbl> <chr>  <dbl>
##  1     1 Math     2008 Fall      15
##  2     1 Math     2008 Spring    16
##  3     1 Math     2008 Winter    19
##  4     1 Math     2009 Fall      12
##  5     1 Math     2009 Spring    13
##  6     1 Math     2009 Winter    27
##  7     1 Writing  2008 Fall      22
##  8     1 Writing  2008 Spring    22
##  9     1 Writing  2008 Winter    24
## 10     1 Writing  2009 Fall      10
## # ... with 26 more rows
```

```r
# ahhh, but we still have an issue - we have multiple rows per observation (see row 1 and row 7). One more step! 

grades %>% 
  pivot_longer(
    Fall:Winter,
    names_to = "Season",
    values_to = "Score"
  ) %>% 
  pivot_wider(
    names_from = Test,
    values_from = Score
  )
```

```
## # A tibble: 18 x 5
##       ID  Year Season  Math Writing
##    <dbl> <dbl> <chr>  <dbl>   <dbl>
##  1     1  2008 Fall      15      22
##  2     1  2008 Spring    16      22
##  3     1  2008 Winter    19      24
##  4     1  2009 Fall      12      10
##  5     1  2009 Spring    13      14
##  6     1  2009 Winter    27      20
##  7     2  2008 Fall      12      13
##  8     2  2008 Spring    13      11
##  9     2  2008 Winter    25      29
## 10     2  2009 Fall      16      23
## 11     2  2009 Spring    14      20
## 12     2  2009 Winter    21      26
## 13     3  2008 Fall      11      17
## 14     3  2008 Spring    12      12
## 15     3  2008 Winter    22      23
## 16     3  2009 Fall      13      14
## 17     3  2009 Spring    11       9
## 18     3  2009 Winter    27      31
```
