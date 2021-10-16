---
title: "Data Science Written HW 1"
author: "Phileas Dazeley Gaist"
date: "10/11/2021"
output: 
  html_document:
    df_print: paged
    keep_md: true
---



# Written Assignment #2

**Collaboratively worked on with Adel Misherghi and Lisa-Marie Kotthoff.**

## Details

- Due Date:
  * 2021-10-15 (this Friday!) prior to the start of class (i.e., needs to be submitted before 1PM EST).
- Format:
  * You’ll submit this via Google Classroom. Again, it can be in whatever format you like so long as it uploads! Take care if you’re trying to use a Google Doc, however, as the copy/paste function of code seems to be a little funky.
- Working Style
  * You can do this individually or as a group - it is entirely up to you! If you do work in groups, please make note in the document that you did so and list everyone’s name.

## Data

Everyone complains about bad drivers - but which state has the worst bad drivers? Let’s explore that question and see if we can find any interesting relationships.

The data and data dictionary/context are available here. You can download the data directly with these commands:


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
library(PerformanceAnalytics)
```

```
## Loading required package: xts
```

```
## Loading required package: zoo
```

```
## 
## Attaching package: 'zoo'
```

```
## The following objects are masked from 'package:base':
## 
##     as.Date, as.Date.numeric
```

```
## 
## Attaching package: 'xts'
```

```
## The following objects are masked from 'package:dplyr':
## 
##     first, last
```

```
## 
## Attaching package: 'PerformanceAnalytics'
```

```
## The following object is masked from 'package:graphics':
## 
##     legend
```

```r
library(Hmisc)
```

```
## Loading required package: lattice
```

```
## Loading required package: survival
```

```
## Loading required package: Formula
```

```
## 
## Attaching package: 'Hmisc'
```

```
## The following objects are masked from 'package:dplyr':
## 
##     src, summarize
```

```
## The following objects are masked from 'package:base':
## 
##     format.pval, units
```

```r
data <- read_csv(url("https://raw.githubusercontent.com/fivethirtyeight/data/master/bad-drivers/bad-drivers.csv"))
```

```
## Rows: 51 Columns: 8
```

```
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr (1): State
## dbl (7): Number of drivers involved in fatal collisions per billion miles, P...
```

```
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
data
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["State"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Number of drivers involved in fatal collisions per billion miles"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["Percentage Of Drivers Involved In Fatal Collisions Who Were Speeding"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["Percentage Of Drivers Involved In Fatal Collisions Who Were Alcohol-Impaired"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["Percentage Of Drivers Involved In Fatal Collisions Who Were Not Distracted"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["Percentage Of Drivers Involved In Fatal Collisions Who Had Not Been Involved In Any Previous Accidents"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["Car Insurance Premiums ($)"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["Losses incurred by insurance companies for collisions per insured driver ($)"],"name":[8],"type":["dbl"],"align":["right"]}],"data":[{"1":"Alabama","2":"18.8","3":"39","4":"30","5":"96","6":"80","7":"784.55","8":"145.08"},{"1":"Alaska","2":"18.1","3":"41","4":"25","5":"90","6":"94","7":"1053.48","8":"133.93"},{"1":"Arizona","2":"18.6","3":"35","4":"28","5":"84","6":"96","7":"899.47","8":"110.35"},{"1":"Arkansas","2":"22.4","3":"18","4":"26","5":"94","6":"95","7":"827.34","8":"142.39"},{"1":"California","2":"12.0","3":"35","4":"28","5":"91","6":"89","7":"878.41","8":"165.63"},{"1":"Colorado","2":"13.6","3":"37","4":"28","5":"79","6":"95","7":"835.50","8":"139.91"},{"1":"Connecticut","2":"10.8","3":"46","4":"36","5":"87","6":"82","7":"1068.73","8":"167.02"},{"1":"Delaware","2":"16.2","3":"38","4":"30","5":"87","6":"99","7":"1137.87","8":"151.48"},{"1":"District of Columbia","2":"5.9","3":"34","4":"27","5":"100","6":"100","7":"1273.89","8":"136.05"},{"1":"Florida","2":"17.9","3":"21","4":"29","5":"92","6":"94","7":"1160.13","8":"144.18"},{"1":"Georgia","2":"15.6","3":"19","4":"25","5":"95","6":"93","7":"913.15","8":"142.80"},{"1":"Hawaii","2":"17.5","3":"54","4":"41","5":"82","6":"87","7":"861.18","8":"120.92"},{"1":"Idaho","2":"15.3","3":"36","4":"29","5":"85","6":"98","7":"641.96","8":"82.75"},{"1":"Illinois","2":"12.8","3":"36","4":"34","5":"94","6":"96","7":"803.11","8":"139.15"},{"1":"Indiana","2":"14.5","3":"25","4":"29","5":"95","6":"95","7":"710.46","8":"108.92"},{"1":"Iowa","2":"15.7","3":"17","4":"25","5":"97","6":"87","7":"649.06","8":"114.47"},{"1":"Kansas","2":"17.8","3":"27","4":"24","5":"77","6":"85","7":"780.45","8":"133.80"},{"1":"Kentucky","2":"21.4","3":"19","4":"23","5":"78","6":"76","7":"872.51","8":"137.13"},{"1":"Louisiana","2":"20.5","3":"35","4":"33","5":"73","6":"98","7":"1281.55","8":"194.78"},{"1":"Maine","2":"15.1","3":"38","4":"30","5":"87","6":"84","7":"661.88","8":"96.57"},{"1":"Maryland","2":"12.5","3":"34","4":"32","5":"71","6":"99","7":"1048.78","8":"192.70"},{"1":"Massachusetts","2":"8.2","3":"23","4":"35","5":"87","6":"80","7":"1011.14","8":"135.63"},{"1":"Michigan","2":"14.1","3":"24","4":"28","5":"95","6":"77","7":"1110.61","8":"152.26"},{"1":"Minnesota","2":"9.6","3":"23","4":"29","5":"88","6":"88","7":"777.18","8":"133.35"},{"1":"Mississippi","2":"17.6","3":"15","4":"31","5":"10","6":"100","7":"896.07","8":"155.77"},{"1":"Missouri","2":"16.1","3":"43","4":"34","5":"92","6":"84","7":"790.32","8":"144.45"},{"1":"Montana","2":"21.4","3":"39","4":"44","5":"84","6":"85","7":"816.21","8":"85.15"},{"1":"Nebraska","2":"14.9","3":"13","4":"35","5":"93","6":"90","7":"732.28","8":"114.82"},{"1":"Nevada","2":"14.7","3":"37","4":"32","5":"95","6":"99","7":"1029.87","8":"138.71"},{"1":"New Hampshire","2":"11.6","3":"35","4":"30","5":"87","6":"83","7":"746.54","8":"120.21"},{"1":"New Jersey","2":"11.2","3":"16","4":"28","5":"86","6":"78","7":"1301.52","8":"159.85"},{"1":"New Mexico","2":"18.4","3":"19","4":"27","5":"67","6":"98","7":"869.85","8":"120.75"},{"1":"New York","2":"12.3","3":"32","4":"29","5":"88","6":"80","7":"1234.31","8":"150.01"},{"1":"North Carolina","2":"16.8","3":"39","4":"31","5":"94","6":"81","7":"708.24","8":"127.82"},{"1":"North Dakota","2":"23.9","3":"23","4":"42","5":"99","6":"86","7":"688.75","8":"109.72"},{"1":"Ohio","2":"14.1","3":"28","4":"34","5":"99","6":"82","7":"697.73","8":"133.52"},{"1":"Oklahoma","2":"19.9","3":"32","4":"29","5":"92","6":"94","7":"881.51","8":"178.86"},{"1":"Oregon","2":"12.8","3":"33","4":"26","5":"67","6":"90","7":"804.71","8":"104.61"},{"1":"Pennsylvania","2":"18.2","3":"50","4":"31","5":"96","6":"88","7":"905.99","8":"153.86"},{"1":"Rhode Island","2":"11.1","3":"34","4":"38","5":"92","6":"79","7":"1148.99","8":"148.58"},{"1":"South Carolina","2":"23.9","3":"38","4":"41","5":"96","6":"81","7":"858.97","8":"116.29"},{"1":"South Dakota","2":"19.4","3":"31","4":"33","5":"98","6":"86","7":"669.31","8":"96.87"},{"1":"Tennessee","2":"19.5","3":"21","4":"29","5":"82","6":"81","7":"767.91","8":"155.57"},{"1":"Texas","2":"19.4","3":"40","4":"38","5":"91","6":"87","7":"1004.75","8":"156.83"},{"1":"Utah","2":"11.3","3":"43","4":"16","5":"88","6":"96","7":"809.38","8":"109.48"},{"1":"Vermont","2":"13.6","3":"30","4":"30","5":"96","6":"95","7":"716.20","8":"109.61"},{"1":"Virginia","2":"12.7","3":"19","4":"27","5":"87","6":"88","7":"768.95","8":"153.72"},{"1":"Washington","2":"10.6","3":"42","4":"33","5":"82","6":"86","7":"890.03","8":"111.62"},{"1":"West Virginia","2":"23.8","3":"34","4":"28","5":"97","6":"87","7":"992.61","8":"152.56"},{"1":"Wisconsin","2":"13.8","3":"36","4":"33","5":"39","6":"84","7":"670.31","8":"106.62"},{"1":"Wyoming","2":"17.4","3":"42","4":"32","5":"81","6":"90","7":"791.14","8":"122.04"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

Note: for full credit, you must provide the functions you used to obtain your answers!

## Questions

Answer these as thoroughly as you can and please provide the code that you’ve used to generate your answer.

**1.** Which state(s) has the highest number of drivers involved in fatal collisions per billion miles?

**Answer:** The two states with the highest number of drivers involved in fatal collisions per billion miles are North Dakota and South Carolina.


```r
data %>% 
  arrange(desc(`Number of drivers involved in fatal collisions per billion miles`)) %>% 
  select(State, `Number of drivers involved in fatal collisions per billion miles`) %>% 
  head(2)
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["State"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Number of drivers involved in fatal collisions per billion miles"],"name":[2],"type":["dbl"],"align":["right"]}],"data":[{"1":"North Dakota","2":"23.9"},{"1":"South Carolina","2":"23.9"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

**2** What is the state-level average percentage of drivers involved in fatal collisions who were alcohol-impaired? (Note: remember which of these data elements are US states and which ones are not!)

**Answer:** The mean percentage of drivers involved in fatal collisions who were alcohol-impaired for all US-States is 30.76%.


```r
data %>% 
  filter(State != "District of Columbia") %>% 
  summarise("mean percentage fatal accident alcohol" = mean(`Percentage Of Drivers Involved In Fatal Collisions Who Were Alcohol-Impaired`))
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["mean percentage fatal accident alcohol"],"name":[1],"type":["dbl"],"align":["right"]}],"data":[{"1":"30.76"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

**3** Identify if a given state is above or below the median car insurance premiums from this data set. Now test, using a two-sided t-test, if the average number of drivers involved in fatal collisions per billion miles is different between these two groups. Use a confidence threshold of 90%. Answer the question by referring back to the hypothesis you’re testing.

**Answer:** 

$H_{0}$: There is no statistically significant difference between the mean number of drivers involved in fatal collisions per billion miles in states above ($\overline{A}$) or below ($\overline{B}$) the median state-level car insurance premiums. $\overline{A} = \overline{B}$

$H_{1}$: There is a statistically significant difference between the mean number of drivers involved in fatal collisions per billion miles in states above ($\overline{A}$) or below ($\overline{B}$) the median state-level car insurance premiums. $\overline{A} \neq \overline{B}$

Since the result of a Student's two-tailed T-test shows a T-statistic of 0.34, and a p-value > 0.1 (p = 0.73), we cannot reject $H_{0}$. It is likely that $H_{0}$ is true. 


```r
data %>% 
  filter(State != "District of Columbia") %>% 
  mutate(premium_group = ifelse(`Car Insurance Premiums ($)` > median(`Car Insurance Premiums ($)`), "above median premiums", "below median premiums")) %>% 
  do(tidy(t.test(`Number of drivers involved in fatal collisions per billion miles` ~ premium_group, data = ., conf.level = 0.9)))
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["estimate"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["estimate1"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["estimate2"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["statistic"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["p.value"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["parameter"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["conf.low"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["conf.high"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["method"],"name":[9],"type":["chr"],"align":["left"]},{"label":["alternative"],"name":[10],"type":["chr"],"align":["left"]}],"data":[{"1":"0.384","2":"16.18","3":"15.796","4":"0.3439351","5":"0.7324444","6":"46.53404","7":"-1.489765","8":"2.257765","9":"Welch Two Sample t-test","10":"two.sided"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

**However,** I note that the results differ when I calculate the median outside of the pipe chain. The results are noticeably different, but not enough to change my conclusions about $H_{0}$ and $H_{1}$ My best guess is that the difference could be due to rounding differences in the way the median is calculated using either approach.


```r
median_premiums <- median(data$`Car Insurance Premiums ($)`)

data %>% 
  filter(State != "District of Columbia") %>% 
  mutate(premium_group = ifelse(`Car Insurance Premiums ($)` > median_premiums, "above median premiums", "below median premiums")) %>% 
  do(tidy(t.test(`Number of drivers involved in fatal collisions per billion miles` ~ premium_group, data = ., conf.level = 0.9)))
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["estimate"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["estimate1"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["estimate2"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["statistic"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["p.value"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["parameter"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["conf.low"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["conf.high"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["method"],"name":[9],"type":["chr"],"align":["left"]},{"label":["alternative"],"name":[10],"type":["chr"],"align":["left"]}],"data":[{"1":"-0.249359","2":"15.85833","3":"16.10769","4":"-0.222534","5":"0.8248592","6":"47.16225","7":"-2.129419","8":"1.630701","9":"Welch Two Sample t-test","10":"two.sided"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

What is odd about this, but not particularly concerning since the null hypothesis was not rejected, is that the T-statistic is positive when using the first approach, and negative when using the second, although their absolute values are quite close to each other for either of the two. 

**4** Compare the average percentage of drivers involved in fatal collisions while speeding between states on the West Coast (including Alaska and Hawaii) to every state on the East Coast (Florida up through Maine) using a t-test. Test if the East Coast drivers have a lower average percentage than West Coast (hint: use a one-sided test!) using a 95% confidence threshold.

**Answer:** 

$H_{0}$: There is no statistically significant difference between the mean percentage of drivers involved in fatal collisions while speeding in states on the east ($\overline{A}$) and west ($\overline{B}$) coasts of the US. $\overline{A} = \overline{B}$

$H_{1}$: The mean percentage of drivers involved in fatal collisions while speeding in states on the east coast of the US ($\overline{A}$) is statistically significantly lower than the mean percentage of drivers involved in fatal collisions while speeding in states on the west coast of the US ($\overline{B}$). $\overline{A} < \overline{B}$

Since the result of a Student's T-test shows a T-statistic of -2.11, and a p-value < 0.05 (p = 0.03), we can reject $H_{0}$ and support $H_{1}$. It is likely that $H_{1}$ is true.


```r
west_c_states <- c("Alaska", "Hawaii", "California", "Oregon", "Washington")
east_c_states <- c("Florida", "Georgia", "South Carolina", "North Carolina", "Virginia", "Maryland", "Delaware", "New Jersey", "New York", "Connecticut", "Rhode Island", "Massachussets", "New Hampshire", "Maine")

coast_data <- data %>% 
  filter(State %in%  c(west_c_states, east_c_states)) %>% 
  # Assign groups: West coast = 1, East coast = 2
  mutate(coast = ifelse(State %in%  west_c_states, "west coast", "east coast"))

coast_data %>% 
  # Do t-test:
  do(tidy(t.test(`Percentage Of Drivers Involved In Fatal Collisions Who Were Speeding` ~ coast, alternative="less", data = ., conf.level = 0.95)))
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["estimate"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["estimate1"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["estimate2"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["statistic"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["p.value"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["parameter"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["conf.low"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["conf.high"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["method"],"name":[9],"type":["chr"],"align":["left"]},{"label":["alternative"],"name":[10],"type":["chr"],"align":["left"]}],"data":[{"1":"-9.538462","2":"31.46154","3":"41","4":"-2.11025","5":"0.03306543","6":"8.42164","7":"-Inf","8":"-1.187419","9":"Welch Two Sample t-test","10":"less"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

```r
coast_data %>% 
  # Let's plot a box plot too just to support the results visually:
  ggplot(aes(coast, `Percentage Of Drivers Involved In Fatal Collisions Who Were Speeding`)) + geom_boxplot() # I note the outlier in the west coast data.
```

![](Data_Science_Written_HW_2_Phileas_Dazeley-Gaist_files/figure-html/unnamed-chunk-6-1.png)<!-- -->
**Personal note:** While the tidy way of doing t.tests is nice visually, it annoys me that I can't see which estimate is associated with which sample group at a glance. For this, the classic base r t.test is much better.

**5** Is there evidence of a statistically significant correlation between the percentage of drivers involved in fatal collisions who were alcohol impaired and the number of drivers involved in fatal collisions per billion miles? Use a confidence threshold of 90%

**Answer:** 

$H_{0}$: The population correlation coefficient is not significantly different from 0. There is no significant linear relationship between the percentage of drivers involved in fatal collisions who were alcohol impaired and the number of drivers in fatal collisions per billion miles in the population. $\rho = 0$

$H_{1}$: The population correlation coefficient is significantly different from zero. There is a significan linear relationship between the percentage of drivers involved in fatal collisions who were alcohol impaired and the number of drivers in fatal collisions per billion miles in the population. $\rho \neq 0$

Since the result of a Pearson's product-moment correlation shows an r-value of 0.2 and p-value > 0.05 (p = 0.16), we cannot reject $H_{0}$. It is likely that $H_{0}$ is true. There is no evidence of a statistically significant correlation between the percentage of drivers involved in fatal collisions who were alcohol impaired and the number of drivers involved in fatal collisions per billion miles.


```r
# We can calculate the correlation between the two variables like so:
cor.test(data$`Percentage Of Drivers Involved In Fatal Collisions Who Were Alcohol-Impaired`, data$`Number of drivers involved in fatal collisions per billion miles`, alternative = "two.sided", conf.level = 0.9)
```

```
## 
## 	Pearson's product-moment correlation
## 
## data:  data$`Percentage Of Drivers Involved In Fatal Collisions Who Were Alcohol-Impaired` and data$`Number of drivers involved in fatal collisions per billion miles`
## t = 1.4246, df = 49, p-value = 0.1606
## alternative hypothesis: true correlation is not equal to 0
## 90 percent confidence interval:
##  -0.03526448  0.41327074
## sample estimates:
##       cor 
## 0.1994263
```


```r
# We can also visualise a scatter plot of the data to confirm results visually:
data %>% 
  ggplot(aes(x = `Percentage Of Drivers Involved In Fatal Collisions Who Were Alcohol-Impaired`, y = `Number of drivers involved in fatal collisions per billion miles`)) + 
  geom_point() +
  labs(x = "% drivers fatal inv. alcohol", y = "n drivers inv. fatal/billion miles")
```

![](Data_Science_Written_HW_2_Phileas_Dazeley-Gaist_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

**6** Examine all of the possible correlations between the numeric variables and reported which variables, if any, are statistically correlated. Make sure you report the correlation coefficient for each pair of variable and that you’re using a confidence threshold of 95% each time.

**Answer:** Of the 21 unique combinations of numeric variables in the data set, only two show significant statistical correlation using a confidence threshold of 95%: 

1. Percentage Of Drivers Involved In Fatal Collisions Who Were Alcohol-Impaired + 	Percentage Of Drivers Involved In Fatal Collisions Who Were Speeding: r = 0.29, p = 0.04
2. Losses incurred by insurance companies for collisions per insured driver (usd) + 	Car Insurance Premiums (usd): r = 0.62, p < 0.001

The remaining combinations' r and p values can be consulted in the correlation table below.

Code below partially adapted from [this page](http://www.sthda.com/english/wiki/correlation-matrix-a-quick-start-guide-to-analyze-format-and-visualize-a-correlation-matrix-using-r-software#use-chart.correlation-draw-scatter-plots).


```r
# Let's plot the data frame to get an idea of where some of the juiciest correlations in the data might lie:
data_clean <- data %>% 
  select(-State)
plot(data_clean)
```

![](Data_Science_Written_HW_2_Phileas_Dazeley-Gaist_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

```r
# Hmm... Hard to see where there potential correlations of interest lie, but we can plot that additional info easily enough: (p-values(0, 0.001, 0.01, 0.05, 0.1, 1) <=> symbols(“***”, “**”, “*”, “.”, " “))
chart.Correlation(data_clean, histogram = TRUE, pch = 19)
```

![](Data_Science_Written_HW_2_Phileas_Dazeley-Gaist_files/figure-html/unnamed-chunk-9-2.png)<!-- -->

```r
# Let's make a table of all the r and p value results of Pearson's product-moment correlation test for every combination of numeric variables in the data set and display it:
cor_matrix <- rcorr(as.matrix(data_clean),type="pearson")

lower_triangle <- lower.tri(cor_matrix$r)

correlation_table <- data.frame(
    var1 = rownames(cor_matrix$r)[row(cor_matrix$r)[lower_triangle]],
    var2 = rownames(cor_matrix$r)[col(cor_matrix$r)[lower_triangle]],
    cor  =(cor_matrix$r)[lower_triangle],
    p = round(cor_matrix$P[lower_triangle], 2)
    )

correlation_table
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["var1"],"name":[1],"type":["chr"],"align":["left"]},{"label":["var2"],"name":[2],"type":["chr"],"align":["left"]},{"label":["cor"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["p"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"Percentage Of Drivers Involved In Fatal Collisions Who Were Speeding","2":"Number of drivers involved in fatal collisions per billion miles","3":"-0.029080146","4":"0.84"},{"1":"Percentage Of Drivers Involved In Fatal Collisions Who Were Alcohol-Impaired","2":"Number of drivers involved in fatal collisions per billion miles","3":"0.199426344","4":"0.16"},{"1":"Percentage Of Drivers Involved In Fatal Collisions Who Were Not Distracted","2":"Number of drivers involved in fatal collisions per billion miles","3":"0.009781764","4":"0.95"},{"1":"Percentage Of Drivers Involved In Fatal Collisions Who Had Not Been Involved In Any Previous Accidents","2":"Number of drivers involved in fatal collisions per billion miles","3":"-0.017941877","4":"0.90"},{"1":"Car Insurance Premiums ($)","2":"Number of drivers involved in fatal collisions per billion miles","3":"-0.199701946","4":"0.16"},{"1":"Losses incurred by insurance companies for collisions per insured driver ($)","2":"Number of drivers involved in fatal collisions per billion miles","3":"-0.036011082","4":"0.80"},{"1":"Percentage Of Drivers Involved In Fatal Collisions Who Were Alcohol-Impaired","2":"Percentage Of Drivers Involved In Fatal Collisions Who Were Speeding","3":"0.286244171","4":"0.04"},{"1":"Percentage Of Drivers Involved In Fatal Collisions Who Were Not Distracted","2":"Percentage Of Drivers Involved In Fatal Collisions Who Were Speeding","3":"0.131737796","4":"0.36"},{"1":"Percentage Of Drivers Involved In Fatal Collisions Who Had Not Been Involved In Any Previous Accidents","2":"Percentage Of Drivers Involved In Fatal Collisions Who Were Speeding","3":"0.014066221","4":"0.92"},{"1":"Car Insurance Premiums ($)","2":"Percentage Of Drivers Involved In Fatal Collisions Who Were Speeding","3":"0.042541263","4":"0.77"},{"1":"Losses incurred by insurance companies for collisions per insured driver ($)","2":"Percentage Of Drivers Involved In Fatal Collisions Who Were Speeding","3":"-0.061240523","4":"0.67"},{"1":"Percentage Of Drivers Involved In Fatal Collisions Who Were Not Distracted","2":"Percentage Of Drivers Involved In Fatal Collisions Who Were Alcohol-Impaired","3":"0.043379788","4":"0.76"},{"1":"Percentage Of Drivers Involved In Fatal Collisions Who Had Not Been Involved In Any Previous Accidents","2":"Percentage Of Drivers Involved In Fatal Collisions Who Were Alcohol-Impaired","3":"-0.245455060","4":"0.08"},{"1":"Car Insurance Premiums ($)","2":"Percentage Of Drivers Involved In Fatal Collisions Who Were Alcohol-Impaired","3":"-0.017450713","4":"0.90"},{"1":"Losses incurred by insurance companies for collisions per insured driver ($)","2":"Percentage Of Drivers Involved In Fatal Collisions Who Were Alcohol-Impaired","3":"-0.083915929","4":"0.56"},{"1":"Percentage Of Drivers Involved In Fatal Collisions Who Had Not Been Involved In Any Previous Accidents","2":"Percentage Of Drivers Involved In Fatal Collisions Who Were Not Distracted","3":"-0.195264522","4":"0.17"},{"1":"Car Insurance Premiums ($)","2":"Percentage Of Drivers Involved In Fatal Collisions Who Were Not Distracted","3":"0.019578112","4":"0.89"},{"1":"Losses incurred by insurance companies for collisions per insured driver ($)","2":"Percentage Of Drivers Involved In Fatal Collisions Who Were Not Distracted","3":"-0.058466772","4":"0.68"},{"1":"Car Insurance Premiums ($)","2":"Percentage Of Drivers Involved In Fatal Collisions Who Had Not Been Involved In Any Previous Accidents","3":"0.075533138","4":"0.60"},{"1":"Losses incurred by insurance companies for collisions per insured driver ($)","2":"Percentage Of Drivers Involved In Fatal Collisions Who Had Not Been Involved In Any Previous Accidents","3":"0.042770136","4":"0.77"},{"1":"Losses incurred by insurance companies for collisions per insured driver ($)","2":"Car Insurance Premiums ($)","3":"0.623116439","4":"0.00"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

```r
# finally, let's filter out all rows with p-values > 0.05
correlation_table %>% 
  filter(p<=0.05)
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["var1"],"name":[1],"type":["chr"],"align":["left"]},{"label":["var2"],"name":[2],"type":["chr"],"align":["left"]},{"label":["cor"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["p"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"Percentage Of Drivers Involved In Fatal Collisions Who Were Alcohol-Impaired","2":"Percentage Of Drivers Involved In Fatal Collisions Who Were Speeding","3":"0.2862442","4":"0.04"},{"1":"Losses incurred by insurance companies for collisions per insured driver ($)","2":"Car Insurance Premiums ($)","3":"0.6231164","4":"0.00"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
