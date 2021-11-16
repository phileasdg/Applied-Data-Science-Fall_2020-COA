---
title: "Data Science Written HW 1"
author: "Phileas Dazeley Gaist"
date: "10/25/2021"
output: 
  html_document:
    df_print: paged
    keep_md: true
---



# Written Assignment #3

##Details

**Collaboratively worked on with Adel Misherghi** 

- Due Date:
  * 2021-10-29 (this Friday!) prior to the start of class (i.e., needs to be submitted before 1PM EST).
- Format:
  * You’ll submit this via Google Classroom. Again, it can be in whatever format you like so long as it uploads! Take care if you’re trying to use a Google Doc, however, as the copy/paste function of code seems to be a little funky.
- Working Style
  * You can do this individually or as a group - it is entirely up to you! If you do work in groups, please make note in the document that you did so and list everyone’s name.

## Data

In the spirit of the holiday - we’re going to examine some halloween candy data!

The data is available here. You can gather more information about the data set here. You can use the code below to download the data.


```r
library(tidyverse)
```

```
## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --
```

```
## v ggplot2 3.3.5     v purrr   0.3.4
## v tibble  3.1.5     v dplyr   1.0.7
## v tidyr   1.1.4     v stringr 1.4.0
## v readr   2.0.1     v forcats 0.5.1
```

```
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(broom)
candy <- read_csv(url("https://raw.githubusercontent.com/kylescotshank/applied_data_science/master/data/candy-data.csv"))
```

```
## Rows: 85 Columns: 13
```

```
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr  (1): competitorname
## dbl (12): chocolate, fruity, caramel, peanutyalmondy, nougat, crispedricewaf...
```

```
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
candy
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["competitorname"],"name":[1],"type":["chr"],"align":["left"]},{"label":["chocolate"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["fruity"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["caramel"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["peanutyalmondy"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["nougat"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["crispedricewafer"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["hard"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["bar"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["pluribus"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["sugarpercent"],"name":[11],"type":["dbl"],"align":["right"]},{"label":["pricepercent"],"name":[12],"type":["dbl"],"align":["right"]},{"label":["winpercent"],"name":[13],"type":["dbl"],"align":["right"]}],"data":[{"1":"100 Grand","2":"1","3":"0","4":"1","5":"0","6":"0","7":"1","8":"0","9":"1","10":"0","11":"0.732","12":"0.860","13":"66.97173"},{"1":"3 Musketeers","2":"1","3":"0","4":"0","5":"0","6":"1","7":"0","8":"0","9":"1","10":"0","11":"0.604","12":"0.511","13":"67.60294"},{"1":"One dime","2":"0","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"0","11":"0.011","12":"0.116","13":"32.26109"},{"1":"One quarter","2":"0","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"0","11":"0.011","12":"0.511","13":"46.11650"},{"1":"Air Heads","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"0","11":"0.906","12":"0.511","13":"52.34146"},{"1":"Almond Joy","2":"1","3":"0","4":"0","5":"1","6":"0","7":"0","8":"0","9":"1","10":"0","11":"0.465","12":"0.767","13":"50.34755"},{"1":"Baby Ruth","2":"1","3":"0","4":"1","5":"1","6":"1","7":"0","8":"0","9":"1","10":"0","11":"0.604","12":"0.767","13":"56.91455"},{"1":"Boston Baked Beans","2":"0","3":"0","4":"0","5":"1","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.313","12":"0.511","13":"23.41782"},{"1":"Candy Corn","2":"0","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.906","12":"0.325","13":"38.01096"},{"1":"Caramel Apple Pops","2":"0","3":"1","4":"1","5":"0","6":"0","7":"0","8":"0","9":"0","10":"0","11":"0.604","12":"0.325","13":"34.51768"},{"1":"Charleston Chew","2":"1","3":"0","4":"0","5":"0","6":"1","7":"0","8":"0","9":"1","10":"0","11":"0.604","12":"0.511","13":"38.97504"},{"1":"Chewey Lemonhead Fruit Mix","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.732","12":"0.511","13":"36.01763"},{"1":"Chiclets","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.046","12":"0.325","13":"24.52499"},{"1":"Dots","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.732","12":"0.511","13":"42.27208"},{"1":"Dum Dums","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"1","9":"0","10":"0","11":"0.732","12":"0.034","13":"39.46056"},{"1":"Fruit Chews","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.127","12":"0.034","13":"43.08892"},{"1":"Fun Dip","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"1","9":"0","10":"0","11":"0.732","12":"0.325","13":"39.18550"},{"1":"Gobstopper","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"1","9":"0","10":"1","11":"0.906","12":"0.453","13":"46.78335"},{"1":"Haribo Gold Bears","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.465","12":"0.465","13":"57.11974"},{"1":"Haribo Happy Cola","2":"0","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.465","12":"0.465","13":"34.15896"},{"1":"Haribo Sour Bears","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.465","12":"0.465","13":"51.41243"},{"1":"Haribo Twin Snakes","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.465","12":"0.465","13":"42.17877"},{"1":"HersheyÕs Kisses","2":"1","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.127","12":"0.093","13":"55.37545"},{"1":"HersheyÕs Krackel","2":"1","3":"0","4":"0","5":"0","6":"0","7":"1","8":"0","9":"1","10":"0","11":"0.430","12":"0.918","13":"62.28448"},{"1":"HersheyÕs Milk Chocolate","2":"1","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"1","10":"0","11":"0.430","12":"0.918","13":"56.49050"},{"1":"HersheyÕs Special Dark","2":"1","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"1","10":"0","11":"0.430","12":"0.918","13":"59.23612"},{"1":"Jawbusters","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"1","9":"0","10":"1","11":"0.093","12":"0.511","13":"28.12744"},{"1":"Junior Mints","2":"1","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.197","12":"0.511","13":"57.21925"},{"1":"Kit Kat","2":"1","3":"0","4":"0","5":"0","6":"0","7":"1","8":"0","9":"1","10":"0","11":"0.313","12":"0.511","13":"76.76860"},{"1":"Laffy Taffy","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"0","11":"0.220","12":"0.116","13":"41.38956"},{"1":"Lemonhead","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"1","9":"0","10":"0","11":"0.046","12":"0.104","13":"39.14106"},{"1":"Lifesavers big ring gummies","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"0","11":"0.267","12":"0.279","13":"52.91139"},{"1":"Peanut butter M&MÕs","2":"1","3":"0","4":"0","5":"1","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.825","12":"0.651","13":"71.46505"},{"1":"M&MÕs","2":"1","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.825","12":"0.651","13":"66.57458"},{"1":"Mike & Ike","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.872","12":"0.325","13":"46.41172"},{"1":"Milk Duds","2":"1","3":"0","4":"1","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.302","12":"0.511","13":"55.06407"},{"1":"Milky Way","2":"1","3":"0","4":"1","5":"0","6":"1","7":"0","8":"0","9":"1","10":"0","11":"0.604","12":"0.651","13":"73.09956"},{"1":"Milky Way Midnight","2":"1","3":"0","4":"1","5":"0","6":"1","7":"0","8":"0","9":"1","10":"0","11":"0.732","12":"0.441","13":"60.80070"},{"1":"Milky Way Simply Caramel","2":"1","3":"0","4":"1","5":"0","6":"0","7":"0","8":"0","9":"1","10":"0","11":"0.965","12":"0.860","13":"64.35334"},{"1":"Mounds","2":"1","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"1","10":"0","11":"0.313","12":"0.860","13":"47.82975"},{"1":"Mr Good Bar","2":"1","3":"0","4":"0","5":"1","6":"0","7":"0","8":"0","9":"1","10":"0","11":"0.313","12":"0.918","13":"54.52645"},{"1":"Nerds","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"1","9":"0","10":"1","11":"0.848","12":"0.325","13":"55.35405"},{"1":"Nestle Butterfinger","2":"1","3":"0","4":"0","5":"1","6":"0","7":"0","8":"0","9":"1","10":"0","11":"0.604","12":"0.767","13":"70.73564"},{"1":"Nestle Crunch","2":"1","3":"0","4":"0","5":"0","6":"0","7":"1","8":"0","9":"1","10":"0","11":"0.313","12":"0.767","13":"66.47068"},{"1":"Nik L Nip","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.197","12":"0.976","13":"22.44534"},{"1":"Now & Later","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.220","12":"0.325","13":"39.44680"},{"1":"Payday","2":"0","3":"0","4":"0","5":"1","6":"1","7":"0","8":"0","9":"1","10":"0","11":"0.465","12":"0.767","13":"46.29660"},{"1":"Peanut M&Ms","2":"1","3":"0","4":"0","5":"1","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.593","12":"0.651","13":"69.48379"},{"1":"Pixie Sticks","2":"0","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.093","12":"0.023","13":"37.72234"},{"1":"Pop Rocks","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"1","9":"0","10":"1","11":"0.604","12":"0.837","13":"41.26551"},{"1":"Red vines","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.581","12":"0.116","13":"37.34852"},{"1":"ReeseÕs Miniatures","2":"1","3":"0","4":"0","5":"1","6":"0","7":"0","8":"0","9":"0","10":"0","11":"0.034","12":"0.279","13":"81.86626"},{"1":"ReeseÕs Peanut Butter cup","2":"1","3":"0","4":"0","5":"1","6":"0","7":"0","8":"0","9":"0","10":"0","11":"0.720","12":"0.651","13":"84.18029"},{"1":"ReeseÕs pieces","2":"1","3":"0","4":"0","5":"1","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.406","12":"0.651","13":"73.43499"},{"1":"ReeseÕs stuffed with pieces","2":"1","3":"0","4":"0","5":"1","6":"0","7":"0","8":"0","9":"0","10":"0","11":"0.988","12":"0.651","13":"72.88790"},{"1":"Ring pop","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"1","9":"0","10":"0","11":"0.732","12":"0.965","13":"35.29076"},{"1":"Rolo","2":"1","3":"0","4":"1","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.860","12":"0.860","13":"65.71629"},{"1":"Root Beer Barrels","2":"0","3":"0","4":"0","5":"0","6":"0","7":"0","8":"1","9":"0","10":"1","11":"0.732","12":"0.069","13":"29.70369"},{"1":"Runts","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"1","9":"0","10":"1","11":"0.872","12":"0.279","13":"42.84914"},{"1":"Sixlets","2":"1","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.220","12":"0.081","13":"34.72200"},{"1":"Skittles original","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.941","12":"0.220","13":"63.08514"},{"1":"Skittles wildberry","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.941","12":"0.220","13":"55.10370"},{"1":"Nestle Smarties","2":"1","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.267","12":"0.976","13":"37.88719"},{"1":"Smarties candy","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"1","9":"0","10":"1","11":"0.267","12":"0.116","13":"45.99583"},{"1":"Snickers","2":"1","3":"0","4":"1","5":"1","6":"1","7":"0","8":"0","9":"1","10":"0","11":"0.546","12":"0.651","13":"76.67378"},{"1":"Snickers Crisper","2":"1","3":"0","4":"1","5":"1","6":"0","7":"1","8":"0","9":"1","10":"0","11":"0.604","12":"0.651","13":"59.52925"},{"1":"Sour Patch Kids","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.069","12":"0.116","13":"59.86400"},{"1":"Sour Patch Tricksters","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.069","12":"0.116","13":"52.82595"},{"1":"Starburst","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.151","12":"0.220","13":"67.03763"},{"1":"Strawberry bon bons","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"1","9":"0","10":"1","11":"0.569","12":"0.058","13":"34.57899"},{"1":"Sugar Babies","2":"0","3":"0","4":"1","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.965","12":"0.767","13":"33.43755"},{"1":"Sugar Daddy","2":"0","3":"0","4":"1","5":"0","6":"0","7":"0","8":"0","9":"0","10":"0","11":"0.418","12":"0.325","13":"32.23100"},{"1":"Super Bubble","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"0","11":"0.162","12":"0.116","13":"27.30386"},{"1":"Swedish Fish","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.604","12":"0.755","13":"54.86111"},{"1":"Tootsie Pop","2":"1","3":"1","4":"0","5":"0","6":"0","7":"0","8":"1","9":"0","10":"0","11":"0.604","12":"0.325","13":"48.98265"},{"1":"Tootsie Roll Juniors","2":"1","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"0","11":"0.313","12":"0.511","13":"43.06890"},{"1":"Tootsie Roll Midgies","2":"1","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.174","12":"0.011","13":"45.73675"},{"1":"Tootsie Roll Snack Bars","2":"1","3":"0","4":"0","5":"0","6":"0","7":"0","8":"0","9":"1","10":"0","11":"0.465","12":"0.325","13":"49.65350"},{"1":"Trolli Sour Bites","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.313","12":"0.255","13":"47.17323"},{"1":"Twix","2":"1","3":"0","4":"1","5":"0","6":"0","7":"1","8":"0","9":"1","10":"0","11":"0.546","12":"0.906","13":"81.64291"},{"1":"Twizzlers","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"0","11":"0.220","12":"0.116","13":"45.46628"},{"1":"Warheads","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"1","9":"0","10":"0","11":"0.093","12":"0.116","13":"39.01190"},{"1":"WelchÕs Fruit Snacks","2":"0","3":"1","4":"0","5":"0","6":"0","7":"0","8":"0","9":"0","10":"1","11":"0.313","12":"0.313","13":"44.37552"},{"1":"WertherÕs Original Caramel","2":"0","3":"0","4":"1","5":"0","6":"0","7":"0","8":"1","9":"0","10":"0","11":"0.186","12":"0.267","13":"41.90431"},{"1":"Whoppers","2":"1","3":"0","4":"0","5":"0","6":"0","7":"1","8":"0","9":"0","10":"1","11":"0.872","12":"0.848","13":"49.52411"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

Note: for full credit, you must provide the functions you used to obtain your answers!

# Questions

Answer these as thoroughly as you can and please provide the code that you’ve used to generate your answer.

**1.** Generate a facet grid of bar plots showing the distribution of each variable. Your output should show a grid of bar plots where you get a bar for TRUE and FALSE counts of each variable. Note: this will be much, much easier if you remember to use the pivot_longer command). Provide a written interpretation of your visualization.

**Answer:** 

The visualisation is an array of counts of candies all candies in the data set which are or are not of a certain type. (IV = column variable candy attribute, DV = count).

The following visualisation shows that our data set contains:

- 21 candies that are bars, and 64 that are not
- 14 candies that are caramel, and 71 that are not
- 37 candies that are chocolate, and 48 that are not
- 7 candies that are crisped rice wafers, and 78 that are not
- 38 candies that are fruity, and 47 that are not
- 15 candies that are hard, and 70 that are not
- 7 candies that are nougat, and 78 that are not
- 14 candies that are peanuty-almondy, and 71 that are not
- 44 candies that come as one of many in a bag or box, and 41 that do not


```r
# prepare the candy data for ggplot
candy_pivoted <- candy %>% 
  select(-c(sugarpercent, pricepercent, winpercent)) %>% 
  pivot_longer(!competitorname, names_to = "property", values_to = "presence") %>% 
  group_by(property, presence) %>% 
  summarise(property_count = n())
```

```
## `summarise()` has grouped output by 'property'. You can override using the `.groups` argument.
```

```r
# plot a facet wrap of bar plots showing the distribution of each variable (dropping non-logical variables). Here, I chose to generate a facet wrap rather than a facet grid because the facet_wrap allows us to plot across a single variable (ingredient) over multiple rows of the plot, which is easier to read in this case. 
candy_pivoted %>% 
  ggplot() +
  geom_col(aes(as.factor(as.logical(presence)), property_count)) +
  labs(x = "Property presence", y = "Count") +
  facet_wrap(vars(property)) +
  theme_bw()
```

![](Data_Science_Written_HW_3_Phileas_Dazeley-Gaist_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```r
# This is nice, but we can improve the plot further by replacing the x-axis with a colour-coded legend, since the axis only contains 2 values (TRUE and FALSE), and the colour will more intuitively communicate that information.
candy_pivoted %>%
  ggplot() + 
  geom_col(aes(as.factor(as.logical(presence)), property_count, fill = as.factor(as.logical(presence)))) +
  theme(axis.title.x = element_blank(),
        axis.text.x = element_blank(),
        axis.ticks.x = element_blank()) +
  facet_wrap(vars(property)) +
  labs(y = "Count", fill = 'Presence of property')
```

![](Data_Science_Written_HW_3_Phileas_Dazeley-Gaist_files/figure-html/unnamed-chunk-2-2.png)<!-- -->

**2.** Generate a plot where you show competitorname of each candy bar and that candy bar's value for pricepercent. Make sure that this plot has competitorname on the y-axis and the pricepercent on the x-axis. Order the chart so that the values go from largest to smallest (top to bottom). Note: you’ll need to use coord_flip() to do this! Make sure you look up that function with ?coord_flip to see how it works works. You’ll also need to reorder the bars - to do this, use the reorder() function. Use ?reorder to see how it works.

**Answer:** The procedure described above produces the following plot:

![Price percent by competitor name](Price_percent_by_competitor_name.png)


```r
# Plot a bar graph of competitor name by price percent, and flip it.
candy %>% 
  ggplot() +
  geom_col(aes(x = reorder(competitorname, pricepercent), y = pricepercent)) +
  labs(x = "Competitor name", y = "Price percent") +
  coord_flip() + # This can be skipped by simply swapping the x and y axes variables
  theme_bw()
```

```r
ggsave("Price_percent_by_competitor_name.png", height = 10)
```

```
## Saving 7 x 10 in image
```

**3.** Run a t-test that compares the average of sugarpercent between candy bars that are chocolate versus those that are not. Report the results and interpret your findings. Visualize the differences between these groups with a boxplot.

**Answer:** 

$H_{0}$: There is no statistically significant difference between the mean sugar percent of candy bars in this data set that are chocolate ($\overline{A}$), and the mean sugar percent of candy bars in this data set that are not chocolate ($\overline{B}$). In consequence: $\overline{A} = \overline{B}$

$H_{1}$: There is a statistically significant difference between the mean sugar percent of candy bars in this data set that are chocolate ($\overline{A}$), and the mean sugar percent of candy bars in this data set that are not chocolate ($\overline{B}$). In consequence: $\overline{A} \neq \overline{B}$

Since the result of a Student's two-tailed T-test shows a T-statistic of approximately 0.99, and a p-value > 0.1 (p = 0.33), we cannot reject $H_{0}$. It is likely that $H_{0}$ is true. (Confidence threshold = 0.95)


```r
# filter for candy bars that are chocolate vs those that are not
# candy %>% filter(bar == 1) %>% filter(chocolate == 0)
# I did not do this because it results in too few values to conduct a t-test. I am interpreting the prompt as indifferent as to whether the candy is a bar or not.

# perform t-test
candy %>% 
  do(tidy(t.test(sugarpercent ~ chocolate, data = ., conf.level = 0.95)))
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["estimate"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["estimate1"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["estimate2"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["statistic"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["p.value"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["parameter"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["conf.low"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["conf.high"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["method"],"name":[9],"type":["chr"],"align":["left"]},{"label":["alternative"],"name":[10],"type":["chr"],"align":["left"]}],"data":[{"1":"-0.0590625","2":"0.4529375","3":"0.512","4":"-0.9856381","5":"0.3271756","6":"82.9904","7":"-0.1782473","8":"0.06012235","9":"Welch Two Sample t-test","10":"two.sided"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

```r
# plot boxplot
candy %>% 
  ggplot(aes(x = as.factor(as.logical(chocolate)), y = sugarpercent)) +
  geom_jitter(alpha = 0.2) + 
  geom_boxplot(fill = NA, color = "coral") + 
  labs(x = "Presence of chocolate", y = "Sugar percent") +
  theme_bw()
```

![](Data_Science_Written_HW_3_Phileas_Dazeley-Gaist_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

**4.** Create a scatterplot showing the variable sugarpercent on the x-axis and winpercent on the y-axis. Color the points based on whether or not the candybar is fruity or chocolate. Add linear regressions that show the different relationships for chocolate and fruity candybar types. Provide a written interpretation of your visualization.

**Answer:** 
The regression lines on the first plot show that there is a slight positive linear relation between sugar percent (IV) and win percent (IV) for candies that are fruity or chocolate, and a slight negative linear relation between these two variables for other candies. 

The regression lines on the second plot illustrate the same ideas, but adds that the slight positive linear relation persists for candies that are chocolate, or fruity, when considered individually.


```r
# interpreting "Color the points based on whether or not the candybar is fruity or chocolate" as an instruction to colour the points different colours based on whether the candy is fruity or chocolate, or is neither:

candy %>%
  mutate(choc_fruit = if_else(chocolate == 1 | fruity == 1, TRUE, FALSE)) %>% 
  ggplot(aes(x = sugarpercent, y = winpercent, colour = choc_fruit)) +
  geom_point() +
  geom_smooth(method = "lm") +
  labs(x = "Sugar percent", y = "Win percent", colour = "Chocolate or Fruity") +
  theme_bw()
```

```
## `geom_smooth()` using formula 'y ~ x'
```

![](Data_Science_Written_HW_3_Phileas_Dazeley-Gaist_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

```r
# interpreting "Color the points based on whether or not the candybar is fruity or chocolate" as an instruction to colour the points different colours based on whether the candy is fruity, chocolate, or is neither:


candy %>%
  mutate(choc_fruit = if_else(chocolate == 1, "Chocolate", if_else(fruity == 1, "Fruity", "Other"))) %>% 
  ggplot(aes(x = sugarpercent, y = winpercent, colour = choc_fruit)) +
  geom_point() +
  geom_smooth(method = "lm") +
  labs(x = "Sugar percent", y = "Win percent", colour = "Group") +
  theme_bw()
```

```
## `geom_smooth()` using formula 'y ~ x'
```

![](Data_Science_Written_HW_3_Phileas_Dazeley-Gaist_files/figure-html/unnamed-chunk-5-2.png)<!-- -->

**5.** Run a regression with winpercent as the dependent variable and everything else as independent variables. Print the summary() of the output of this model. Plot all of the coefficients of this model as a bar chart from largest to smallest. Color the bars based on whether or not the coefficients are positive or negative. Hint: you’ll want to use the tidy() function to easily get the coefficients out of your summary to plot them!. Provide a written interpretation of your visualization.

**Answer:** The visualisation of the coefficients of the linear regression of win percent (DV) and all other variables except competitor name (IVs) as a bar chart tells us that pluribus, price percent, and the property of being hard candy negatively linearly relate to win percent for candies in the data set, and that all others positively linearly relate to win percent. 

In other words, candies which are sold in bags of multiple candies, are more expensive, or are hard are less popular, all other variables excluded, while candies with attributes corresponding to other individual variables are more popular, ceteris paribus.  


```r
# run a linear regression with winpercent as DV and all other numeric variables as IVs.
lm1 <- lm(winpercent ~ . - winpercent - competitorname, data = candy)
lm1_summary <- tidy(summary(lm1))
lm1_summary
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["term"],"name":[1],"type":["chr"],"align":["left"]},{"label":["estimate"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["std.error"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["statistic"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["p.value"],"name":[5],"type":["dbl"],"align":["right"]}],"data":[{"1":"(Intercept)","2":"34.5339784","3":"4.319899","4":"7.99416378","5":"1.444217e-11"},{"1":"chocolate","2":"19.7480670","3":"3.898725","4":"5.06526325","5":"2.962842e-06"},{"1":"fruity","2":"9.4223221","3":"3.762990","4":"2.50394550","5":"1.451657e-02"},{"1":"caramel","2":"2.2244814","3":"3.657364","4":"0.60821988","5":"5.449294e-01"},{"1":"peanutyalmondy","2":"10.0706885","3":"3.615847","4":"2.78515303","5":"6.811194e-03"},{"1":"nougat","2":"0.8043306","3":"5.716427","4":"0.14070514","5":"8.884904e-01"},{"1":"crispedricewafer","2":"8.9189698","3":"5.267879","4":"1.69308550","5":"9.470290e-02"},{"1":"hard","2":"-6.1653265","3":"3.455143","4":"-1.78439129","5":"7.851525e-02"},{"1":"bar","2":"0.4415401","3":"5.061054","4":"0.08724271","5":"9.307175e-01"},{"1":"pluribus","2":"-0.8544995","3":"3.040122","4":"-0.28107409","5":"7.794487e-01"},{"1":"sugarpercent","2":"9.0867629","3":"4.659456","4":"1.95017669","5":"5.499517e-02"},{"1":"pricepercent","2":"-5.9283614","3":"5.513243","4":"-1.07529474","5":"2.857840e-01"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

```r
# interpreting "Color the bars based on whether or not the coefficients are positive or negative." as a prompt to colour bars based on the logical attribute "is >= 0", assigning a colour for positive values, and another for negative values:
lm1_summary %>% 
  mutate(is_positive = if_else(estimate >= 0, "Positive", "Negative")) %>% 
  ggplot(aes(x = reorder(term, estimate), y = estimate, fill = is_positive)) +
  geom_col() +
  labs(x = "Estimate", y = "Term", fill = "Group") +
  coord_flip()
```

![](Data_Science_Written_HW_3_Phileas_Dazeley-Gaist_files/figure-html/unnamed-chunk-6-1.png)<!-- -->
