---
title: "Data Science Written HW 1"
author: "Phileas Dazeley Gaist"
date: "9/27/2021"
output: 
  html_document:
    keep_md: true
---



# Written Assignment #1

**Collaboratively worked on with Adel Misherghi, Lisa-Marie Kotthoff, and Quint Nigro.**

For this assignment, I elected to prioritise solutions which made use of dplyr, tidyverse, and the %>% operator (which I am mostly new to) over other approaches. Within these constraints, I also chose to prioritise code readability over conciseness, although I attempted to keep my solutions as short as I could without making them too obtuse. 

## Details

- Due Date:
  * 2021-10-01 (this Friday!) prior to the start of class (i.e., needs to be submitted before 1PM EST).
- Format: 
  * You’ll submit this via Google Classroom. It can be in whatever format you like - so long as it uploads!
- Working Style: 
  * You can do this individually or as a group - it is entirely up to you! If you do work in groups, please make note in the document that you did so and list everyone’s name.

## Data

Hungry? If you’re not - you’re about to be. We’re going to be diving into a data set about delicious, sugary, probably-pretty-bad-for-you American breakfast cerals!

The context and background of this data can be found [here](https://www.kaggle.com/crawford/80-cereals?select=cereal.csv). You’ll need to look here to see what the columns mean (this is also known as a “data dictionary”).

The data itself can be downloaded from [here](https://www.kaggle.com/crawford/80-cereals/download). If you would like to get the .csv file without having to unzip it, you can grab it from the course github in the /data directory [here](https://github.com/kylescotshank/applied_data_science/tree/master/data).

**Setting things up:**


```r
cereals <- read_csv(url("https://raw.githubusercontent.com/kylescotshank/applied_data_science/master/data/cereal.csv"))
```

```
## Rows: 77 Columns: 16
```

```
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr  (3): name, mfr, type
## dbl (13): calories, protein, fat, sodium, fiber, carbo, sugars, potass, vita...
```

```
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
cereals
```

```
## # A tibble: 77 x 16
##    name      mfr   type  calories protein   fat sodium fiber carbo sugars potass
##    <chr>     <chr> <chr>    <dbl>   <dbl> <dbl>  <dbl> <dbl> <dbl>  <dbl>  <dbl>
##  1 100% Bran N     C           70       4     1    130  10     5        6    280
##  2 100% Nat~ Q     C          120       3     5     15   2     8        8    135
##  3 All-Bran  K     C           70       4     1    260   9     7        5    320
##  4 All-Bran~ K     C           50       4     0    140  14     8        0    330
##  5 Almond D~ R     C          110       2     2    200   1    14        8     -1
##  6 Apple Ci~ G     C          110       2     2    180   1.5  10.5     10     70
##  7 Apple Ja~ K     C          110       2     0    125   1    11       14     30
##  8 Basic 4   G     C          130       3     2    210   2    18        8    100
##  9 Bran Chex R     C           90       2     1    200   4    15        6    125
## 10 Bran Fla~ P     C           90       3     0    210   5    13        5    190
## # ... with 67 more rows, and 5 more variables: vitamins <dbl>, shelf <dbl>,
## #   weight <dbl>, cups <dbl>, rating <dbl>
```

# Questions

Answer these as thoroughly as you can and please provide the code that you’ve used to generate your answer.

**1.** What are the dimensions of this data set?

**Answer:** The dimensions of this data set are 77 observations by 16 variables, 77 rows by 16 columns.


```r
dim(cereals)
```

```
## [1] 77 16
```

**2.** How many columns in this data set have a character data type?

**Answer:** Three columns from this data set have a character data type.


```r
cereals %>% 
    select_if(is.character) %>% 
    ncol()
```

```
## [1] 3
```

**3.** Which manufacturer has the most cereals in this data? How many rows of the dataset does this manufacturer represent?

**Answer:** The manufacturer who owns the most cereal brands in these data is Kellogg's, whose data represent 23 rows of the data set. 


```r
cereals %>% 
  group_by(mfr) %>% 
  summarise(count = n()) %>% 
  arrange(desc(count)) %>% 
  filter(row_number() == 1)
```

```
## # A tibble: 1 x 2
##   mfr   count
##   <chr> <int>
## 1 K        23
```

*or, alternatively*


```r
sort(table(cereals$mfr))[length(table(cereals$mfr))]
```

```
##  K 
## 23
```

**4.** What is the name of the cereal manufactured by American Home Food Products?

**Answer:** The cereal manufactured by American Home Food Products is Maypo.


```r
cereals %>%  
  filter(mfr == "A" ) %>% 
  select(name)
```

```
## # A tibble: 1 x 1
##   name 
##   <chr>
## 1 Maypo
```

**5.** Which three breakfast cereals have the lowest calorie count per serving?

**Answer:** The three breakfast cereals which have the lowest calorie count per serving are
- All-Bran with Extra Fiber,
- Puffed Rice,
- Puffed Wheat,
all three of which are tied at 50 calories per serving.


```r
# The three breakfast cereals which have the lowest calorie count per serving are
# - All-Bran with Extra Fiber,
# - Puffed Rice,
# - Puffed Wheat,
# all three of which are tied at 50 calories per serving.

cereals %>% 
  arrange(calories) %>% 
  select(name, calories) %>% 
  filter(row_number() <= 3)
```

```
## # A tibble: 3 x 2
##   name                      calories
##   <chr>                        <dbl>
## 1 All-Bran with Extra Fiber       50
## 2 Puffed Rice                     50
## 3 Puffed Wheat                    50
```

**6.** Which cold breakfast cereal from Quaker Oats has the highest overall rating?

**Answer:** The cold breakfast cereal brand owned by Quaker Oats which has the highest overall rating is Puffed Wheat, with an approximate rating of 63.


```r
cereals %>% 
  arrange(desc(rating)) %>% 
  filter(type == "C", mfr == "Q") %>%
  select(name, rating) %>% 
  filter(row_number() == 1)
```

```
## # A tibble: 1 x 2
##   name         rating
##   <chr>         <dbl>
## 1 Puffed Wheat   63.0
```

**7.** If you sum the grams of sugar and grams of carbohydrates, which hot cereal brand has the highest combination?

**Answer:** The hot cereal brand which hast the highest combined total grams of sugar and carbohydrates is Nabisco's Cream of Wheat (Quick).


```r
cereals %>% 
  mutate(sugs.carbs = sugars + carbo) %>% 
  filter(type == "H") %>% 
  arrange(desc(sugs.carbs))%>% 
  select(name) %>% 
  filter(row_number() == 1)
```

```
## # A tibble: 1 x 1
##   name                  
##   <chr>                 
## 1 Cream of Wheat (Quick)
```

**8.** How many rows in this data set contain a negative value?

**Answer:** Three rows in this data set contain at least one negative value.


```r
cereals %>% 
  filter_all(any_vars(. < 0)) %>% 
  nrow()
```

```
## [1] 3
```

**9.** Which cereal on the 1st display shelf has the highest amount of fiber and the lowest amount of sodium?

**Answer:** The cereal on the first display shelf with the highest amount of fiber and the lowest amount of sodium is Nabisco's Shredded Wheat 'n'Bran, a box (presumably) of which contains 4 grams of dietary fiber, and 0 milligrams of sodium.


```r
cereals %>% 
  filter(shelf == 1) %>% 
  arrange(desc(fiber), sodium) %>% 
  select(name, fiber, sodium) %>% 
  filter(row_number() == 1)
```

```
## # A tibble: 1 x 3
##   name                   fiber sodium
##   <chr>                  <dbl>  <dbl>
## 1 Shredded Wheat 'n'Bran     4      0
```

**10.** What percentage of the cereals in this data set are hot breakfast cereals?

**Answer:** Approximately 3.9 percent of the cereals in this data set are hot breakfast cereals. 


```r
cereals %>% 
  group_by(type) %>% 
  summarise(type_counts = n()) %>% 
  pivot_wider(names_from = type, values_from = type_counts) %>%  # nifty
  summarise(percentage = 100*(H/(C+H)))
```

```
## # A tibble: 1 x 1
##   percentage
##        <dbl>
## 1       3.90
```

**11.** Which shelf has the highest mean (i.e., average) percentage of daily vitamins per serving?

**Answer:** The third shelf has the highest mean percentage of daily vitamins per serving. The mean for the third shelf stands at approximately 44.7 percent of the FDA daily intake recommendation.


```r
cereals %>% 
  group_by(shelf) %>% 
  summarise(avg_vit = mean(vitamins)) %>% 
  arrange(desc(avg_vit)) %>% 
  mutate(percent_avg_vit = 100 * avg_vit / sum(avg_vit)) %>% 
  filter(row_number() == 1)
```

```
## # A tibble: 1 x 3
##   shelf avg_vit percent_avg_vit
##   <dbl>   <dbl>           <dbl>
## 1     3    35.4            44.7
```

**12.** Which manufacturer has the highest percentage of cereals found on the 3rd shelf?

**Answer:** The manufacturer who owns the highest percentage of the cereal brands found on the third shelf is Kellogg's, whose share of the third shelf cereal brands stands at almost exactly 1/3, or 33.3 percent. 


```r
cereals %>% 
  filter(shelf == 3) %>% 
  group_by(mfr) %>% 
  summarise(mfr_counts = n()) %>% 
  arrange(desc(mfr_counts)) %>% 
  mutate(percent_shelf_3 = 100 * mfr_counts / sum(mfr_counts)) %>% 
  filter(row_number() == 1)
```

```
## # A tibble: 1 x 3
##   mfr   mfr_counts percent_shelf_3
##   <chr>      <int>           <dbl>
## 1 K             12            33.3
```

**13.** What is the range between the highest and lowest rating?

**Answer:** The range between the highest and lowest rating is approximately 75.7


```r
cereals %>% 
  summarise(range = max(rating)-min(rating))
```

```
## # A tibble: 1 x 1
##   range
##   <dbl>
## 1  75.7
```

**14.** Which cereal brand has the highest number of grams of fat per calorie?

**Answer:** The cereal brand with the highest number of grams of fat per calories is Quaker Oats' 100% Natural Bran, with approximately 0.04 grams of fat per calorie. 


```r
cereals %>% 
  mutate(fat_per_cal = fat/calories) %>% 
  arrange(desc(fat_per_cal)) %>% 
  filter(row_number() == 1) %>% 
  select(name, fat_per_cal)
```

```
## # A tibble: 1 x 2
##   name              fat_per_cal
##   <chr>                   <dbl>
## 1 100% Natural Bran      0.0417
```

**15.** If you had to guess which of these cereal brands may have had the most data input and/r data collection errors, which one would you guess and why?

**Answer:** My guess is that Quaker Oatmeal is the brand of cereal which faced the most data input and collection errors because it contains the most (impossible) negative numeric values. 

Since the data set is quite small, it is possible to tell at a glance that it does not contain NaN or NA values, so I did not bother running code to check for them. 


```r
cereals %>% 
  filter_all(any_vars(. < 0)) %>% 
  select(name | where(is.numeric)) %>% 
  pivot_longer(-name, names_to = "categories", values_to = "values") %>% 
  group_by(name) %>% 
  summarise(n_negatives = sum(values < 0)) %>% 
  arrange(desc(n_negatives)) %>% 
  filter(row_number() == 1)
```

```
## # A tibble: 1 x 2
##   name           n_negatives
##   <chr>                <int>
## 1 Quaker Oatmeal           2
```

**Bonus question:** which cereal brand has the most number of words in it’s name? To answer this, try taking a peek at the function str_count with ?str_count and see how it works. Just giving the answer to this doesn’t count - showing me a valid command or series of commands that produces it will be worth some extra credit!

**Answer:**


```r
?str_count
```

```
## starting httpd help server ... done
```

```r
cereals %>% 
  select(name) %>% 
  mutate(chr_count = str_count(name)) %>% 
  arrange(desc(chr_count)) %>% 
  filter(row_number() == 1)
```

```
## # A tibble: 1 x 2
##   name                                   chr_count
##   <chr>                                      <int>
## 1 Fruit & Fibre Dates; Walnuts; and Oats        38
```
