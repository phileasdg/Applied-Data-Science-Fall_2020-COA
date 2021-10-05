---
title: "week 4 - class 1 - Statistics! - Central Tendency"
author: "Phileas Dazeley Gaist"
date: "10/5/2021"
output: 
  html_document:
    df_print: paged
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
# ╋╋╋╋╋╋╋╋╋╋╋╋╋╋┗━━┛       Applied Data Science I - Week 4, Class 1
# # ---------------------------------------------------------------
```




```r
# Today we are going to learn about measures of central tendency!
#
#
#
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
#
# Today's dataset is all about TROPICAL STOOORRMMMSS
data("storms")
```

# Mathematical/statistical moments:
"In mathematics, the moments of a function are quantitative measures related to the shape of the function's graph" [Wikipedia](https://en.wikipedia.org/wiki/Moment_(mathematics)) Estimates of the shape of data's distribution.


```r
# # ---------------------------------------------------------------
#
# Moment #1: The Mean! 
#
# # ---------------------------------------------------------------


# Remember that the mean is the 1st statistical moment of the distribution of your data.
# ...that is a fancy way to say that the mean describes the *location* of your distribution - it's center of gravity. 

hist(storms$wind)
```

![](week-4---class-1---Statistics!---Central-Tendency_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

```r
# The function to calculate the mean is - Surprise! - mean() 

mean(storms$wind)
```

```
## [1] 53.495
```

```r
# This is the average windspeed across the entire dataset (i.e. - across all measures!)
# As you know, mean also works with pipes and summarize()! 

# Let's use %>% and summarize to look at the average windspeed by status for storms in 1986 
storms %>% 
  filter(year == 1986) %>%
  group_by(status) %>% 
  summarize(avg_wind_speed = mean(wind)) %>% 
  arrange(desc(avg_wind_speed))
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["status"],"name":[1],"type":["chr"],"align":["left"]},{"label":["avg_wind_speed"],"name":[2],"type":["dbl"],"align":["right"]}],"data":[{"1":"hurricane","2":"68.00000"},{"1":"tropical storm","2":"44.88095"},{"1":"tropical depression","2":"24.44444"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

```r
# Let's maybe see if hurricanes are getting "stronger" and group by year with the mean 
storms %>%
  filter(status == 'hurricane') %>% 
  group_by(year) %>% 
  summarize(avg_wind_speed = mean(wind)) %>%
  arrange(year)
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["avg_wind_speed"],"name":[2],"type":["dbl"],"align":["right"]}],"data":[{"1":"1975","2":"81.52174"},{"1":"1976","2":"84.31818"},{"1":"1977","2":"84.00000"},{"1":"1978","2":"72.00000"},{"1":"1979","2":"88.37209"},{"1":"1980","2":"75.23810"},{"1":"1981","2":"81.03175"},{"1":"1982","2":"87.39130"},{"1":"1983","2":"75.31250"},{"1":"1984","2":"75.47297"},{"1":"1985","2":"80.74324"},{"1":"1986","2":"68.00000"},{"1":"1987","2":"78.75000"},{"1":"1988","2":"101.76471"},{"1":"1989","2":"90.14925"},{"1":"1990","2":"73.67021"},{"1":"1991","2":"85.71429"},{"1":"1992","2":"95.98361"},{"1":"1993","2":"78.25000"},{"1":"1994","2":"68.33333"},{"1":"1995","2":"82.37255"},{"1":"1996","2":"87.50000"},{"1":"1997","2":"79.39024"},{"1":"1998","2":"85.85859"},{"1":"1999","2":"99.76190"},{"1":"2000","2":"80.27559"},{"1":"2001","2":"81.87500"},{"1":"2002","2":"85.00000"},{"1":"2003","2":"97.51852"},{"1":"2004","2":"98.43949"},{"1":"2005","2":"91.48045"},{"1":"2006","2":"77.31707"},{"1":"2007","2":"102.22222"},{"1":"2008","2":"89.36170"},{"1":"2009","2":"87.65306"},{"1":"2010","2":"85.10870"},{"1":"2011","2":"81.32911"},{"1":"2012","2":"74.75410"},{"1":"2013","2":"72.69231"},{"1":"2014","2":"83.86667"},{"1":"2015","2":"88.80000"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

```r
storms %>%
  filter(status == 'hurricane') %>% 
  group_by(year) %>% 
  summarize(avg_wind_speed = mean(wind)) %>%
  arrange(year) %>% 
  ggplot(aes(x = year, y = avg_wind_speed)) + geom_line() + theme_bw()
```

![](week-4---class-1---Statistics!---Central-Tendency_files/figure-html/unnamed-chunk-3-2.png)<!-- -->


```r
# # ---------------------------------------------------------------
#
# Moment #2: Variance and Standard Deviations! 
#
# # ---------------------------------------------------------------

# Variance is the 2nd statistical moment of your distribution - it describes the *spread* of your data. 
# Often times, we want to have this spread described in the same units as mean. To do that, we take the square root. 
# The square root of the variance is the standard deviation (which you can think of as the average spread). 
# High values are more spread out than smaller values.

# Let's maybe see if hurricanes have a wider "spread" amongst their averages when we group by year

storms %>%
  filter(status == 'hurricane') %>% 
  group_by(year) %>% 
  summarize(avg_wind_speed = mean(wind),
            sd_wind_speed = sd(wind)) %>%
  arrange(year)
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["avg_wind_speed"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["sd_wind_speed"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"1975","2":"81.52174","3":"13.351437"},{"1":"1976","2":"84.31818","3":"11.981678"},{"1":"1977","2":"84.00000","3":"25.628931"},{"1":"1978","2":"72.00000","3":"7.582875"},{"1":"1979","2":"88.37209","3":"25.741268"},{"1":"1980","2":"75.23810","3":"10.373220"},{"1":"1981","2":"81.03175","3":"13.294394"},{"1":"1982","2":"87.39130","3":"15.657525"},{"1":"1983","2":"75.31250","3":"13.350250"},{"1":"1984","2":"75.47297","3":"10.859278"},{"1":"1985","2":"80.74324","3":"14.445989"},{"1":"1986","2":"68.00000","3":"4.216370"},{"1":"1987","2":"78.75000","3":"14.317821"},{"1":"1988","2":"101.76471","3":"24.037960"},{"1":"1989","2":"90.14925","3":"20.628656"},{"1":"1990","2":"73.67021","3":"10.528393"},{"1":"1991","2":"85.71429","3":"14.701618"},{"1":"1992","2":"95.98361","3":"23.484386"},{"1":"1993","2":"78.25000","3":"11.687710"},{"1":"1994","2":"68.33333","3":"3.256695"},{"1":"1995","2":"82.37255","3":"17.027029"},{"1":"1996","2":"87.50000","3":"20.273718"},{"1":"1997","2":"79.39024","3":"16.777780"},{"1":"1998","2":"85.85859","3":"19.725790"},{"1":"1999","2":"99.76190","3":"19.603060"},{"1":"2000","2":"80.27559","3":"15.083196"},{"1":"2001","2":"81.87500","3":"16.695263"},{"1":"2002","2":"85.00000","3":"17.431183"},{"1":"2003","2":"97.51852","3":"22.846618"},{"1":"2004","2":"98.43949","3":"23.037410"},{"1":"2005","2":"91.48045","3":"26.247812"},{"1":"2006","2":"77.31707","3":"12.995074"},{"1":"2007","2":"102.22222","3":"30.908670"},{"1":"2008","2":"89.36170","3":"18.797650"},{"1":"2009","2":"87.65306","3":"15.814749"},{"1":"2010","2":"85.10870","3":"19.458616"},{"1":"2011","2":"81.32911","3":"15.845991"},{"1":"2012","2":"74.75410","3":"9.996951"},{"1":"2013","2":"72.69231","3":"5.633007"},{"1":"2014","2":"83.86667","3":"17.155358"},{"1":"2015","2":"88.80000","3":"21.298654"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

```r
# Let's try visualizing this one - might help! 

storms %>%
  filter(status == 'hurricane') %>% 
  group_by(year) %>% 
  summarize(avg_wind_speed = mean(wind),
            sd_wind_speed = sd(wind)) %>%
  ggplot(aes(x = year, y = avg_wind_speed)) + 
  geom_line(alpha = 0.3) + geom_point() + 
  geom_errorbar(aes(ymin=avg_wind_speed-sd_wind_speed, ymax=avg_wind_speed+sd_wind_speed), width=.2,
                position=position_dodge(0.05), color = 'red') + 
  theme_bw()
```

![](week-4---class-1---Statistics!---Central-Tendency_files/figure-html/unnamed-chunk-4-1.png)<!-- -->


```r
# # ---------------------------------------------------------------
#
# Moment #3: Skewness! 
#
# # ---------------------------------------------------------------

# Skewness is the 3rd statistical moment of your distribution - it describes the *lean* of your distribution. 
# A positive skew means you have a left lean and a long right tail. 
# This means that the mean (center of gravity) is to the right of the bulk of your data.
# Skewness will matter a lot when we start talking about linear models, as they give us an idea of 
# how far our distribution is "deviating" from normal - as well perhaps which direction contains the most outliers. 

# First, let's calculate the skewness! There is no base R function that does this, so we need to install and
# use a package. Let's use PerformanceAnalytics. 

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
storms %>%
  filter(status == 'hurricane') %>%
  select(wind) %>%
  skewness()
```

```
## [1] 1.024806
```

```r
# The rule of thumb seems to be: If the skewness is between -0.5 and 0.5, the data are fairly symmetrical. 
# If the skewness is between -1 and – 0.5 or between 0.5 and 1, the data are moderately skewed. 
# If the skewness is less than -1 or greater than 1, the data are highly skewed.

# Let's look at the probability density plot to get an idea of how "skewed" our data may be on hurricane wind speeds. 

storms %>%
  filter(status == 'hurricane') %>% 
  group_by(year) %>% 
  ggplot(aes(x = wind)) + 
  stat_density(geom = "line", alpha = 1, colour = "cornflowerblue") + 
  theme_bw()
```

![](week-4---class-1---Statistics!---Central-Tendency_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

```r
# Let's add some flavor to visualize this a little better ...

storms_data <- storms %>%
  filter(status == 'hurricane') %>% 
  select(wind)

median <- median(storms_data$wind)
mean <- mean(storms_data$wind)

base_plot <- storms_data %>% 
  ggplot(aes(x = wind)) + 
  stat_density(geom = "line", alpha = 1, colour = "cornflowerblue") + 
  theme_bw()

shaded_area_data <- 
  ggplot_build(base_plot)$data[[1]] %>% 
  filter(x < mean(storms_data$wind))

median_line_data <- 
  ggplot_build(base_plot)$data[[1]] %>% 
  filter(x <= median)

mean_line_data <- 
  ggplot_build(base_plot)$data[[1]] %>% 
  filter(x <= mean)

base_plot +
  geom_segment(data = shaded_area_data, aes(x = mean, y = 0, xend = mean, yend = density), 
               color = "red", linetype = "dotted") +
  annotate(geom = "text", x = median, y = 0.01, label = "median", color = "red", 
           fontface = "plain", angle = 90, alpha = .8, vjust =  -1.75) +
  geom_segment(data = median_line_data, aes(x = median, y = 0, xend = median, yend = density), 
               color = "red", linetype = "dotted") +
  annotate(geom = "text", x = mean, y = 0.02, label = "mean", 
           fontface = "plain", angle = 90, alpha = .8, vjust =  1.75) +
  geom_segment(data = mean_line_data, aes(x = mean, y = 0, xend = mean, yend = density), 
               color = "black", linetype = "dotted") +
  ggtitle("Density Plot Illustrating Skewness")
```

![](week-4---class-1---Statistics!---Central-Tendency_files/figure-html/unnamed-chunk-5-2.png)<!-- -->


```r
# # ---------------------------------------------------------------
#
# Moment #4: Kurtosis! 
#
# # ---------------------------------------------------------------

# The 4th statistical moment is the kurtosis which describes how "fat" the distribution's tails are/how pointy the distribution is. 
# It tells you how likely it is to find extreme values in your data.
# You'll also see people talk about this as a measure of "peakedness" - which is weird and kind of wrong. 

# First, let's calculate the kurtosis value! There is no base R function that does this, we again turn to a package.

storms %>%
  filter(status == 'hurricane') %>%
  select(wind) %>%
  kurtosis()
```

```
## [1] 0.3340022
```

```r
# The rule of thumb for kurtosis: If the kurtosis is between -3 and 3, the data are fine (also called "mesokurtic" lol)
# If the kurtosis is greater than 3 then this is *leptokurtic*: Distribution is longer, tails are fatter. Peak is higher and sharper than mesokurtic, which means that data are heavy-tailed or profusion of outliers.
# If the kurtosis is less than 3 then this is *platykurtic*: Distribution is shorter, tails are thinner than the normal distribution.
# Note that the kurtosis() function above SUBTRACTS 3 - so its the "excess kurtosis" - so this value is slightly leptokurtic. 

storms %>%
  filter(status == 'hurricane') %>% 
  group_by(year) %>% 
  ggplot(aes(x = wind)) + 
  stat_density(geom = "line", alpha = 1, colour = "cornflowerblue") + 
  theme_bw()
```

![](week-4---class-1---Statistics!---Central-Tendency_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

```r
# This is probably a Poisson distribution.
```


```r
# # ---------------------------------------------------------------
#
# "Robust" measures: Median and Median Absolute Deviation! 
#
# # ---------------------------------------------------------------


# Remember how we saw that the mean and median were different? The median is more "robust" in that it is much less
# sensitive to outliers. Median absolute deviation (MAD) is the same - it's a "robust" measure of variance! 

storms %>%
  filter(status == 'hurricane') %>%
  select(wind) %>%
  summarize(mean = mean(wind),
            sd = sd(wind),
            median = median(wind),
            mad = mad(wind))
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["mean"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["sd"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["median"],"name":[3],"type":["int"],"align":["right"]},{"label":["mad"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"85.96894","2":"20.31805","3":"80","4":"14.826"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

```r
# This code will give you some of the same information:
summary(storms$wind)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   10.00   30.00   45.00   53.49   65.00  160.00
```

