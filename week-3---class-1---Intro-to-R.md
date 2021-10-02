---
title: "week 3 - class 1 - Intro to R"
author: "Phileas Dazeley Gaist"
date: "9/28/2021"
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
# ╋╋╋╋╋╋╋╋╋╋╋╋╋╋┗━━┛       Applied Data Science I - Week 3, Class 1
# # ---------------------------------------------------------------
```




```r
# Today we are going to learn about verbs!
#
#
# ... not really, we're going to learn a bunch of great Tidyverse functions
# but they're slick because they look like verbs. 


# ---------------------------------------------------------------
# Getting Setup 
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
library(janitor)
```

```
## 
## Attaching package: 'janitor'
```

```
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

```r
# If you didn't install this the last class because we ran out of time - use install.packages("janitor")
```
# Setting things up:


```r
# For today, we're going to get a little noisy!
#
# Today's example data is from a Kaggle: https://www.kaggle.com/somesnm/partynyc?select=party_in_nyc.csv 
#
# This dataset contains all noise complaints calls that were received by the city police with complaint type "Loud music/Party" in 2016. 
# The data contains the time of the call, time of the police response, coordinates, and part of the city.

nyc_noise_complaints <- clean_names(read_csv(url("https://raw.githubusercontent.com/kylescotshank/applied_data_science/master/data/party_in_nyc.csv")))
```

```
## Rows: 225414 Columns: 8
```

```
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr  (3): Location Type, City, Borough
## dbl  (3): Incident Zip, Latitude, Longitude
## dttm (2): Created Date, Closed Date
```

```
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
nyc_noise_complaints
```

```
## # A tibble: 225,414 x 8
##    created_date        closed_date         location_type    incident_zip city   
##    <dttm>              <dttm>              <chr>                   <dbl> <chr>  
##  1 2015-12-31 00:01:15 2015-12-31 03:48:04 Store/Commercial        10034 NEW YO~
##  2 2015-12-31 00:02:48 2015-12-31 04:36:13 Store/Commercial        10040 NEW YO~
##  3 2015-12-31 00:03:25 2015-12-31 00:40:15 Residential Bui~        10026 NEW YO~
##  4 2015-12-31 00:03:26 2015-12-31 01:53:38 Residential Bui~        11231 BROOKL~
##  5 2015-12-31 00:05:10 2015-12-31 03:49:10 Residential Bui~        10033 NEW YO~
##  6 2015-12-31 00:08:05 2015-12-31 01:59:12 Residential Bui~        10467 BRONX  
##  7 2015-12-31 00:11:40 2015-12-31 06:24:00 Residential Bui~        11230 BROOKL~
##  8 2015-12-31 00:12:13 2015-12-31 00:38:09 Residential Bui~        11215 BROOKL~
##  9 2015-12-31 00:12:37 2015-12-31 05:03:39 Residential Bui~        10463 BRONX  
## 10 2015-12-31 00:14:13 2015-12-31 06:25:40 Store/Commercial        11372 JACKSO~
## # ... with 225,404 more rows, and 3 more variables: borough <chr>,
## #   latitude <dbl>, longitude <dbl>
```

```r
dim(nyc_noise_complaints)
```

```
## [1] 225414      8
```

```r
str(nyc_noise_complaints)
```

```
## spec_tbl_df [225,414 x 8] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ created_date : POSIXct[1:225414], format: "2015-12-31 00:01:15" "2015-12-31 00:02:48" ...
##  $ closed_date  : POSIXct[1:225414], format: "2015-12-31 03:48:04" "2015-12-31 04:36:13" ...
##  $ location_type: chr [1:225414] "Store/Commercial" "Store/Commercial" "Residential Building/House" "Residential Building/House" ...
##  $ incident_zip : num [1:225414] 10034 10040 10026 11231 10033 ...
##  $ city         : chr [1:225414] "NEW YORK" "NEW YORK" "NEW YORK" "BROOKLYN" ...
##  $ borough      : chr [1:225414] "MANHATTAN" "MANHATTAN" "MANHATTAN" "BROOKLYN" ...
##  $ latitude     : num [1:225414] 40.9 40.9 40.8 40.7 40.9 ...
##  $ longitude    : num [1:225414] -73.9 -73.9 -74 -74 -73.9 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   `Created Date` = col_datetime(format = ""),
##   ..   `Closed Date` = col_datetime(format = ""),
##   ..   `Location Type` = col_character(),
##   ..   `Incident Zip` = col_double(),
##   ..   City = col_character(),
##   ..   Borough = col_character(),
##   ..   Latitude = col_double(),
##   ..   Longitude = col_double()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

# Arrange data sets:


```r
# ---------------------------------------------------------------
# Verb #1: Arrange
# ---------------------------------------------------------------

# Arrange does exactly what you think it does - it orders the rows of a data frame by the values of selected columns (?dplyr::arrange)

nyc_noise_complaints %>% 
  arrange(created_date)
```

```
## # A tibble: 225,414 x 8
##    created_date        closed_date         location_type    incident_zip city   
##    <dttm>              <dttm>              <chr>                   <dbl> <chr>  
##  1 2015-12-31 00:01:15 2015-12-31 03:48:04 Store/Commercial        10034 NEW YO~
##  2 2015-12-31 00:02:48 2015-12-31 04:36:13 Store/Commercial        10040 NEW YO~
##  3 2015-12-31 00:03:25 2015-12-31 00:40:15 Residential Bui~        10026 NEW YO~
##  4 2015-12-31 00:03:26 2015-12-31 01:53:38 Residential Bui~        11231 BROOKL~
##  5 2015-12-31 00:05:10 2015-12-31 03:49:10 Residential Bui~        10033 NEW YO~
##  6 2015-12-31 00:08:05 2015-12-31 01:59:12 Residential Bui~        10467 BRONX  
##  7 2015-12-31 00:11:40 2015-12-31 06:24:00 Residential Bui~        11230 BROOKL~
##  8 2015-12-31 00:12:13 2015-12-31 00:38:09 Residential Bui~        11215 BROOKL~
##  9 2015-12-31 00:12:37 2015-12-31 05:03:39 Residential Bui~        10463 BRONX  
## 10 2015-12-31 00:14:13 2015-12-31 06:25:40 Store/Commercial        11372 JACKSO~
## # ... with 225,404 more rows, and 3 more variables: borough <chr>,
## #   latitude <dbl>, longitude <dbl>
```

```r
# This will arrange from smallest to biggest - or earliest to latest. 
# If you want to FLIP the order, use arrange(desc())

nyc_noise_complaints %>%
  arrange(desc(created_date))
```

```
## # A tibble: 225,414 x 8
##    created_date        closed_date         location_type     incident_zip city  
##    <dttm>              <dttm>              <chr>                    <dbl> <chr> 
##  1 2016-12-31 23:58:52 2017-01-01 00:59:52 Residential Buil~        10463 BRONX 
##  2 2016-12-31 23:56:41 2017-01-01 03:49:12 Residential Buil~        10040 NEW Y~
##  3 2016-12-31 23:56:20 2017-01-01 13:34:00 Residential Buil~        11104 SUNNY~
##  4 2016-12-31 23:55:01 2017-01-01 02:05:06 Residential Buil~        10032 NEW Y~
##  5 2016-12-31 23:53:57 2017-01-01 00:01:41 Store/Commercial         10003 NEW Y~
##  6 2016-12-31 23:52:24 2017-01-01 08:29:36 Residential Buil~        11230 BROOK~
##  7 2016-12-31 23:52:18 2017-01-02 03:50:04 Store/Commercial         11377 WOODS~
##  8 2016-12-31 23:48:41 2017-01-01 04:31:48 Residential Buil~        10035 NEW Y~
##  9 2016-12-31 23:48:25 2017-01-01 05:32:23 Residential Buil~        11229 BROOK~
## 10 2016-12-31 23:46:35 2017-01-01 02:05:01 Residential Buil~        10032 NEW Y~
## # ... with 225,404 more rows, and 3 more variables: borough <chr>,
## #   latitude <dbl>, longitude <dbl>
```

```r
# You can also order by multiple columns! 
# Let's order by created_date and incident zip! 

nyc_noise_complaints %>% 
  arrange(created_date,incident_zip)
```

```
## # A tibble: 225,414 x 8
##    created_date        closed_date         location_type    incident_zip city   
##    <dttm>              <dttm>              <chr>                   <dbl> <chr>  
##  1 2015-12-31 00:01:15 2015-12-31 03:48:04 Store/Commercial        10034 NEW YO~
##  2 2015-12-31 00:02:48 2015-12-31 04:36:13 Store/Commercial        10040 NEW YO~
##  3 2015-12-31 00:03:25 2015-12-31 00:40:15 Residential Bui~        10026 NEW YO~
##  4 2015-12-31 00:03:26 2015-12-31 01:53:38 Residential Bui~        11231 BROOKL~
##  5 2015-12-31 00:05:10 2015-12-31 03:49:10 Residential Bui~        10033 NEW YO~
##  6 2015-12-31 00:08:05 2015-12-31 01:59:12 Residential Bui~        10467 BRONX  
##  7 2015-12-31 00:11:40 2015-12-31 06:24:00 Residential Bui~        11230 BROOKL~
##  8 2015-12-31 00:12:13 2015-12-31 00:38:09 Residential Bui~        11215 BROOKL~
##  9 2015-12-31 00:12:37 2015-12-31 05:03:39 Residential Bui~        10463 BRONX  
## 10 2015-12-31 00:14:13 2015-12-31 06:25:40 Store/Commercial        11372 JACKSO~
## # ... with 225,404 more rows, and 3 more variables: borough <chr>,
## #   latitude <dbl>, longitude <dbl>
```

```r
# ^^ This sorts first by date, and then by incident zip code.

# What if we wanted to arrange first by zip code, then location type?

nyc_noise_complaints %>% 
  arrange(incident_zip, location_type)
```

```
## # A tibble: 225,414 x 8
##    created_date        closed_date         location_type     incident_zip city  
##    <dttm>              <dttm>              <chr>                    <dbl> <chr> 
##  1 2016-09-24 15:47:07 2016-09-25 18:39:29 Residential Buil~           83 CENTR~
##  2 2016-02-21 12:15:37 2016-02-21 14:28:01 Street/Sidewalk             83 CENTR~
##  3 2016-02-28 12:47:15 2016-02-28 23:39:58 Street/Sidewalk             83 CENTR~
##  4 2016-02-28 12:57:33 2016-02-28 23:39:57 Street/Sidewalk             83 CENTR~
##  5 2016-02-28 15:47:31 2016-02-28 23:39:55 Street/Sidewalk             83 CENTR~
##  6 2016-03-06 14:54:49 2016-03-06 20:57:54 Street/Sidewalk             83 CENTR~
##  7 2016-03-12 14:24:37 2016-03-12 14:39:24 Street/Sidewalk             83 CENTR~
##  8 2016-03-13 14:20:15 2016-03-13 16:29:58 Street/Sidewalk             83 CENTR~
##  9 2016-03-13 17:10:59 2016-03-13 17:28:36 Street/Sidewalk             83 CENTR~
## 10 2016-03-25 21:14:54 2016-03-26 07:34:18 Street/Sidewalk             83 CENTR~
## # ... with 225,404 more rows, and 3 more variables: borough <chr>,
## #   latitude <dbl>, longitude <dbl>
```

# Select columns:


```r
# ---------------------------------------------------------------
# Verb #2: Select
# ---------------------------------------------------------------

# Select variables in a data frame - similar to using $ or [,] - but much easier on the eyes

# Select one column...
nyc_noise_complaints %>%
  select(city)
```

```
## # A tibble: 225,414 x 1
##    city           
##    <chr>          
##  1 NEW YORK       
##  2 NEW YORK       
##  3 NEW YORK       
##  4 BROOKLYN       
##  5 NEW YORK       
##  6 BRONX          
##  7 BROOKLYN       
##  8 BROOKLYN       
##  9 BRONX          
## 10 JACKSON HEIGHTS
## # ... with 225,404 more rows
```

```r
# Select a few columns ... 
nyc_noise_complaints %>%
  select(city,borough)
```

```
## # A tibble: 225,414 x 2
##    city            borough  
##    <chr>           <chr>    
##  1 NEW YORK        MANHATTAN
##  2 NEW YORK        MANHATTAN
##  3 NEW YORK        MANHATTAN
##  4 BROOKLYN        BROOKLYN 
##  5 NEW YORK        MANHATTAN
##  6 BRONX           BRONX    
##  7 BROOKLYN        BROOKLYN 
##  8 BROOKLYN        BROOKLYN 
##  9 BRONX           BRONX    
## 10 JACKSON HEIGHTS QUEENS   
## # ... with 225,404 more rows
```

```r
# Maybe select everything but the weird lat/long stuff we're not going to use today
nyc_noise_complaints %>%
  select(-latitude, -longitude)
```

```
## # A tibble: 225,414 x 6
##    created_date        closed_date         location_type    incident_zip city   
##    <dttm>              <dttm>              <chr>                   <dbl> <chr>  
##  1 2015-12-31 00:01:15 2015-12-31 03:48:04 Store/Commercial        10034 NEW YO~
##  2 2015-12-31 00:02:48 2015-12-31 04:36:13 Store/Commercial        10040 NEW YO~
##  3 2015-12-31 00:03:25 2015-12-31 00:40:15 Residential Bui~        10026 NEW YO~
##  4 2015-12-31 00:03:26 2015-12-31 01:53:38 Residential Bui~        11231 BROOKL~
##  5 2015-12-31 00:05:10 2015-12-31 03:49:10 Residential Bui~        10033 NEW YO~
##  6 2015-12-31 00:08:05 2015-12-31 01:59:12 Residential Bui~        10467 BRONX  
##  7 2015-12-31 00:11:40 2015-12-31 06:24:00 Residential Bui~        11230 BROOKL~
##  8 2015-12-31 00:12:13 2015-12-31 00:38:09 Residential Bui~        11215 BROOKL~
##  9 2015-12-31 00:12:37 2015-12-31 05:03:39 Residential Bui~        10463 BRONX  
## 10 2015-12-31 00:14:13 2015-12-31 06:25:40 Store/Commercial        11372 JACKSO~
## # ... with 225,404 more rows, and 1 more variable: borough <chr>
```

```r
# Maybe just reorder the columns because we're feeling ~feisty~ 
nyc_noise_complaints %>% 
  select(location_type, borough, city, incident_zip, closed_date, created_date)
```

```
## # A tibble: 225,414 x 6
##    location_type              borough   city            incident_zip closed_date        
##    <chr>                      <chr>     <chr>                  <dbl> <dttm>             
##  1 Store/Commercial           MANHATTAN NEW YORK               10034 2015-12-31 03:48:04
##  2 Store/Commercial           MANHATTAN NEW YORK               10040 2015-12-31 04:36:13
##  3 Residential Building/House MANHATTAN NEW YORK               10026 2015-12-31 00:40:15
##  4 Residential Building/House BROOKLYN  BROOKLYN               11231 2015-12-31 01:53:38
##  5 Residential Building/House MANHATTAN NEW YORK               10033 2015-12-31 03:49:10
##  6 Residential Building/House BRONX     BRONX                  10467 2015-12-31 01:59:12
##  7 Residential Building/House BROOKLYN  BROOKLYN               11230 2015-12-31 06:24:00
##  8 Residential Building/House BROOKLYN  BROOKLYN               11215 2015-12-31 00:38:09
##  9 Residential Building/House BRONX     BRONX                  10463 2015-12-31 05:03:39
## 10 Store/Commercial           QUEENS    JACKSON HEIGHTS        11372 2015-12-31 06:25:40
## # ... with 225,404 more rows, and 1 more variable: created_date <dttm>
```

```r
# Maybe we just want columns that start with the letter c? 

nyc_noise_complaints %>%
  select(starts_with('c'))
```

```
## # A tibble: 225,414 x 3
##    created_date        closed_date         city           
##    <dttm>              <dttm>              <chr>          
##  1 2015-12-31 00:01:15 2015-12-31 03:48:04 NEW YORK       
##  2 2015-12-31 00:02:48 2015-12-31 04:36:13 NEW YORK       
##  3 2015-12-31 00:03:25 2015-12-31 00:40:15 NEW YORK       
##  4 2015-12-31 00:03:26 2015-12-31 01:53:38 BROOKLYN       
##  5 2015-12-31 00:05:10 2015-12-31 03:49:10 NEW YORK       
##  6 2015-12-31 00:08:05 2015-12-31 01:59:12 BRONX          
##  7 2015-12-31 00:11:40 2015-12-31 06:24:00 BROOKLYN       
##  8 2015-12-31 00:12:13 2015-12-31 00:38:09 BROOKLYN       
##  9 2015-12-31 00:12:37 2015-12-31 05:03:39 BRONX          
## 10 2015-12-31 00:14:13 2015-12-31 06:25:40 JACKSON HEIGHTS
## # ... with 225,404 more rows
```

```r
# There's all sorts of helper functions you may never use - check them out with
?dplyr::select
```

```
## starting httpd help server ... done
```

# Filter rows:


```r
# ---------------------------------------------------------------
# Verb #3: Filter
# ---------------------------------------------------------------

# Filter is just the row-wise version of Select: it gives you only the rows you want! 

# Let's just look at stuff in New York 

nyc_noise_complaints %>% 
  filter(city == 'NEW YORK')
```

```
## # A tibble: 64,112 x 8
##    created_date        closed_date         location_type      incident_zip city 
##    <dttm>              <dttm>              <chr>                     <dbl> <chr>
##  1 2015-12-31 00:01:15 2015-12-31 03:48:04 Store/Commercial          10034 NEW ~
##  2 2015-12-31 00:02:48 2015-12-31 04:36:13 Store/Commercial          10040 NEW ~
##  3 2015-12-31 00:03:25 2015-12-31 00:40:15 Residential Build~        10026 NEW ~
##  4 2015-12-31 00:05:10 2015-12-31 03:49:10 Residential Build~        10033 NEW ~
##  5 2015-12-31 00:16:28 2015-12-31 00:59:23 Store/Commercial          10033 NEW ~
##  6 2015-12-31 00:18:04 2015-12-31 03:49:12 Store/Commercial          10034 NEW ~
##  7 2015-12-31 00:19:43 2015-12-31 00:29:37 Club/Bar/Restaura~        10027 NEW ~
##  8 2015-12-31 00:28:24 2015-12-31 05:19:00 Club/Bar/Restaura~        10025 NEW ~
##  9 2015-12-31 00:31:59 2015-12-31 02:34:08 Residential Build~        10021 NEW ~
## 10 2015-12-31 00:35:11 2015-12-31 05:36:35 Residential Build~        10065 NEW ~
## # ... with 64,102 more rows, and 3 more variables: borough <chr>,
## #   latitude <dbl>, longitude <dbl>
```

```r
  # Note the == 

# Maybe let's look at stuff in New York that are JUST in Residential Buildings 

nyc_noise_complaints %>% 
  filter(city == 'NEW YORK' & location_type == 'Residential Building/House')
```

```
## # A tibble: 31,877 x 8
##    created_date        closed_date         location_type      incident_zip city 
##    <dttm>              <dttm>              <chr>                     <dbl> <chr>
##  1 2015-12-31 00:03:25 2015-12-31 00:40:15 Residential Build~        10026 NEW ~
##  2 2015-12-31 00:05:10 2015-12-31 03:49:10 Residential Build~        10033 NEW ~
##  3 2015-12-31 00:31:59 2015-12-31 02:34:08 Residential Build~        10021 NEW ~
##  4 2015-12-31 00:35:11 2015-12-31 05:36:35 Residential Build~        10065 NEW ~
##  5 2015-12-31 00:36:40 2015-12-31 06:22:27 Residential Build~        10019 NEW ~
##  6 2015-12-31 00:50:53 2015-12-31 06:39:27 Residential Build~        10025 NEW ~
##  7 2015-12-31 00:58:06 2015-12-31 02:45:22 Residential Build~        10033 NEW ~
##  8 2015-12-31 01:02:14 2015-12-31 01:34:03 Residential Build~        10009 NEW ~
##  9 2015-12-31 01:04:25 2015-12-31 02:05:54 Residential Build~        10011 NEW ~
## 10 2015-12-31 01:12:26 2015-12-31 01:32:49 Residential Build~        10032 NEW ~
## # ... with 31,867 more rows, and 3 more variables: borough <chr>,
## #   latitude <dbl>, longitude <dbl>
```

```r
# You can write the above in an easier way if you like because you don't like using & 

nyc_noise_complaints %>%
  filter(city == 'NEW YORK',
         location_type == 'Residential Building/House')
```

```
## # A tibble: 31,877 x 8
##    created_date        closed_date         location_type      incident_zip city 
##    <dttm>              <dttm>              <chr>                     <dbl> <chr>
##  1 2015-12-31 00:03:25 2015-12-31 00:40:15 Residential Build~        10026 NEW ~
##  2 2015-12-31 00:05:10 2015-12-31 03:49:10 Residential Build~        10033 NEW ~
##  3 2015-12-31 00:31:59 2015-12-31 02:34:08 Residential Build~        10021 NEW ~
##  4 2015-12-31 00:35:11 2015-12-31 05:36:35 Residential Build~        10065 NEW ~
##  5 2015-12-31 00:36:40 2015-12-31 06:22:27 Residential Build~        10019 NEW ~
##  6 2015-12-31 00:50:53 2015-12-31 06:39:27 Residential Build~        10025 NEW ~
##  7 2015-12-31 00:58:06 2015-12-31 02:45:22 Residential Build~        10033 NEW ~
##  8 2015-12-31 01:02:14 2015-12-31 01:34:03 Residential Build~        10009 NEW ~
##  9 2015-12-31 01:04:25 2015-12-31 02:05:54 Residential Build~        10011 NEW ~
## 10 2015-12-31 01:12:26 2015-12-31 01:32:49 Residential Build~        10032 NEW ~
## # ... with 31,867 more rows, and 3 more variables: borough <chr>,
## #   latitude <dbl>, longitude <dbl>
```

```r
# Maybe let's look at stuff in New York OR in Residential Buildings 

nyc_noise_complaints %>% 
  filter(city == 'NEW YORK' | location_type == 'Residential Building/House')
```

```
## # A tibble: 178,275 x 8
##    created_date        closed_date         location_type      incident_zip city 
##    <dttm>              <dttm>              <chr>                     <dbl> <chr>
##  1 2015-12-31 00:01:15 2015-12-31 03:48:04 Store/Commercial          10034 NEW ~
##  2 2015-12-31 00:02:48 2015-12-31 04:36:13 Store/Commercial          10040 NEW ~
##  3 2015-12-31 00:03:25 2015-12-31 00:40:15 Residential Build~        10026 NEW ~
##  4 2015-12-31 00:03:26 2015-12-31 01:53:38 Residential Build~        11231 BROO~
##  5 2015-12-31 00:05:10 2015-12-31 03:49:10 Residential Build~        10033 NEW ~
##  6 2015-12-31 00:08:05 2015-12-31 01:59:12 Residential Build~        10467 BRONX
##  7 2015-12-31 00:11:40 2015-12-31 06:24:00 Residential Build~        11230 BROO~
##  8 2015-12-31 00:12:13 2015-12-31 00:38:09 Residential Build~        11215 BROO~
##  9 2015-12-31 00:12:37 2015-12-31 05:03:39 Residential Build~        10463 BRONX
## 10 2015-12-31 00:15:36 2015-12-31 02:58:09 Residential Build~        11213 BROO~
## # ... with 178,265 more rows, and 3 more variables: borough <chr>,
## #   latitude <dbl>, longitude <dbl>
```

```r
# Because the dates were so helpfull stored as time, we can filter on them like numbers! 
# Let's look for everything in Manhattan that happened BEFORE the fourth of july in 2016 

nyc_noise_complaints %>%
  filter(borough == 'MANHATTAN',
         created_date < as.Date('2016-07-04'))
```

```
## # A tibble: 32,966 x 8
##    created_date        closed_date         location_type      incident_zip city 
##    <dttm>              <dttm>              <chr>                     <dbl> <chr>
##  1 2015-12-31 00:01:15 2015-12-31 03:48:04 Store/Commercial          10034 NEW ~
##  2 2015-12-31 00:02:48 2015-12-31 04:36:13 Store/Commercial          10040 NEW ~
##  3 2015-12-31 00:03:25 2015-12-31 00:40:15 Residential Build~        10026 NEW ~
##  4 2015-12-31 00:05:10 2015-12-31 03:49:10 Residential Build~        10033 NEW ~
##  5 2015-12-31 00:16:28 2015-12-31 00:59:23 Store/Commercial          10033 NEW ~
##  6 2015-12-31 00:18:04 2015-12-31 03:49:12 Store/Commercial          10034 NEW ~
##  7 2015-12-31 00:19:43 2015-12-31 00:29:37 Club/Bar/Restaura~        10027 NEW ~
##  8 2015-12-31 00:28:24 2015-12-31 05:19:00 Club/Bar/Restaura~        10025 NEW ~
##  9 2015-12-31 00:31:59 2015-12-31 02:34:08 Residential Build~        10021 NEW ~
## 10 2015-12-31 00:35:11 2015-12-31 05:36:35 Residential Build~        10065 NEW ~
## # ... with 32,956 more rows, and 3 more variables: borough <chr>,
## #   latitude <dbl>, longitude <dbl>
```

# Mutate -> make modifications to data sets:


```r
# ---------------------------------------------------------------
# Verb #4: Mutate 
# ---------------------------------------------------------------

# So far we've sorted stuff, and selected stuff. Now let's change stuff! 

# What if we perhaps we wanted to know the time interval between the closed and open dates
# We could use mutate! 

nyc_noise_complaints %>%
  mutate(interval = closed_date - created_date) # creates a new "interval" column and fills it with the values of the closed_date column minus the values of the created_date column.
```

```
## # A tibble: 225,414 x 9
##    created_date        closed_date         location_type    incident_zip city   
##    <dttm>              <dttm>              <chr>                   <dbl> <chr>  
##  1 2015-12-31 00:01:15 2015-12-31 03:48:04 Store/Commercial        10034 NEW YO~
##  2 2015-12-31 00:02:48 2015-12-31 04:36:13 Store/Commercial        10040 NEW YO~
##  3 2015-12-31 00:03:25 2015-12-31 00:40:15 Residential Bui~        10026 NEW YO~
##  4 2015-12-31 00:03:26 2015-12-31 01:53:38 Residential Bui~        11231 BROOKL~
##  5 2015-12-31 00:05:10 2015-12-31 03:49:10 Residential Bui~        10033 NEW YO~
##  6 2015-12-31 00:08:05 2015-12-31 01:59:12 Residential Bui~        10467 BRONX  
##  7 2015-12-31 00:11:40 2015-12-31 06:24:00 Residential Bui~        11230 BROOKL~
##  8 2015-12-31 00:12:13 2015-12-31 00:38:09 Residential Bui~        11215 BROOKL~
##  9 2015-12-31 00:12:37 2015-12-31 05:03:39 Residential Bui~        10463 BRONX  
## 10 2015-12-31 00:14:13 2015-12-31 06:25:40 Store/Commercial        11372 JACKSO~
## # ... with 225,404 more rows, and 4 more variables: borough <chr>,
## #   latitude <dbl>, longitude <dbl>, interval <drtn>
```

```r
## What if we wanted to combine the City and Zip Code for whatever reason? 

nyc_noise_complaints %>% 
  mutate(city_zip = paste(city, incident_zip, sep = ' - '))
```

```
## # A tibble: 225,414 x 9
##    created_date        closed_date         location_type    incident_zip city   
##    <dttm>              <dttm>              <chr>                   <dbl> <chr>  
##  1 2015-12-31 00:01:15 2015-12-31 03:48:04 Store/Commercial        10034 NEW YO~
##  2 2015-12-31 00:02:48 2015-12-31 04:36:13 Store/Commercial        10040 NEW YO~
##  3 2015-12-31 00:03:25 2015-12-31 00:40:15 Residential Bui~        10026 NEW YO~
##  4 2015-12-31 00:03:26 2015-12-31 01:53:38 Residential Bui~        11231 BROOKL~
##  5 2015-12-31 00:05:10 2015-12-31 03:49:10 Residential Bui~        10033 NEW YO~
##  6 2015-12-31 00:08:05 2015-12-31 01:59:12 Residential Bui~        10467 BRONX  
##  7 2015-12-31 00:11:40 2015-12-31 06:24:00 Residential Bui~        11230 BROOKL~
##  8 2015-12-31 00:12:13 2015-12-31 00:38:09 Residential Bui~        11215 BROOKL~
##  9 2015-12-31 00:12:37 2015-12-31 05:03:39 Residential Bui~        10463 BRONX  
## 10 2015-12-31 00:14:13 2015-12-31 06:25:40 Store/Commercial        11372 JACKSO~
## # ... with 225,404 more rows, and 4 more variables: borough <chr>,
## #   latitude <dbl>, longitude <dbl>, city_zip <chr>
```

```r
# We'll come back to mutate more later...
```

# Summarise information about data sets:


```r
# ---------------------------------------------------------------
# Verb #5: Summarize
# ---------------------------------------------------------------

# Mutate kept the same number of rows in the data frame and added a column.
# Sometimes we just want to get an answer, you know? So for that, we use summarize

# For example - remember when we mutated above to get the interval of time between the
# close and open times of each policy call? What if we wanted to know the AVERAGE time of the whole dataset? 

nyc_noise_complaints %>%
  mutate(interval = closed_date - created_date) %>%
  summarize(avg_duration = mean(interval))
```

```
## # A tibble: 1 x 1
##   avg_duration
##   <drtn>      
## 1 NA mins
```

```r
# HUH. We got an NA! I wonder why that is...
?mean
mean(c(1:5))
```

```
## [1] 3
```

```r
mean(c(1, 2, 3, 4, 5))
```

```
## [1] 3
```

```r
mean(c(1, 2, NA, 4, 5), na.rm = TRUE) # gets a mean and ignore NA values
```

```
## [1] 3
```

```r
nyc_noise_complaints %>%
  mutate(interval = closed_date - created_date) %>%
  summarize(avg_duration = mean(interval, na.rm = T))
```

```
## # A tibble: 1 x 1
##   avg_duration  
##   <drtn>        
## 1 -516.6851 mins
```

```r
# HUH. STILL WEIRD. LET'S SEE WHERE THESE NEGATIVES ARE STROLLING IN FROM. 

nyc_noise_complaints %>%
  mutate(interval = closed_date - created_date) %>%
  arrange(interval)
```

```
## # A tibble: 225,414 x 9
##    created_date        closed_date         location_type    incident_zip city   
##    <dttm>              <dttm>              <chr>                   <dbl> <chr>  
##  1 2016-03-12 22:56:09 1900-01-01 00:00:00 Residential Bui~           NA <NA>   
##  2 2016-03-12 22:49:56 1900-01-01 00:00:00 Street/Sidewalk            NA <NA>   
##  3 2016-03-12 18:29:57 1900-01-01 00:00:00 Street/Sidewalk            NA <NA>   
##  4 2016-03-11 23:26:11 2016-03-11 23:28:35 Residential Bui~        11215 BROOKL~
##  5 2016-09-13 22:11:20 2016-09-13 22:13:47 Street/Sidewalk         10031 NEW YO~
##  6 2016-06-10 23:16:06 2016-06-10 23:18:36 Street/Sidewalk         10040 NEW YO~
##  7 2016-07-04 22:26:29 2016-07-04 22:28:59 Street/Sidewalk         10040 NEW YO~
##  8 2016-10-10 13:28:33 2016-10-10 13:31:03 Street/Sidewalk         10001 NEW YO~
##  9 2016-09-24 23:10:36 2016-09-24 23:13:07 Store/Commercial        11372 JACKSO~
## 10 2016-04-19 11:25:47 2016-04-19 11:28:20 Street/Sidewalk         10005 NEW YO~
## # ... with 225,404 more rows, and 4 more variables: borough <chr>,
## #   latitude <dbl>, longitude <dbl>, interval <drtn>
```

```r
# got it, okay, let's filter out those rows! 

nyc_noise_complaints %>%
  mutate(interval = closed_date - created_date) %>%
  filter(interval > 0) %>%
  summarize(avg_duration = mean(interval, na.rm = T))
```

```
## # A tibble: 1 x 1
##   avg_duration
##   <drtn>      
## 1 299.547 mins
```

```r
?summarize

# We could compute multiple things this way...

nyc_noise_complaints %>%
  mutate(interval = closed_date - created_date) %>%
  filter(interval > 0) %>%
  summarize(avg_interval = mean(interval, na.rm = T),
            median_interval = median(interval, na.rm = T))
```

```
## # A tibble: 1 x 2
##   avg_interval median_interval
##   <drtn>       <drtn>         
## 1 299.547 mins 154.0167 mins
```

# Group information in data sets to play around with:


```r
# ---------------------------------------------------------------
# Verb #6: Group By
# ---------------------------------------------------------------

# This is the sneaky little verb that's going to make your life incredibly easy - but is almost useless by itself. 
# This lets you GROUP things together to then perform further actions on it! 

# For example - what if we wanted a count of cases by borough? Adding them up individually could be quite annoying. 
#...so let's group them! 

nyc_noise_complaints %>%
  group_by(borough) %>% 
  summarize(count = n())
```

```
## # A tibble: 6 x 2
##   borough       count
##   <chr>         <int>
## 1 BRONX         47672
## 2 BROOKLYN      68905
## 3 MANHATTAN     64172
## 4 QUEENS        38274
## 5 STATEN ISLAND  5411
## 6 Unspecified     980
```

```r
# n() is just a nice easy function that counts for you! 

# What if we wanted the breakdown of location types ONLY in the city of Brooklyn? 

nyc_noise_complaints %>% 
  filter(city == 'BROOKLYN') %>%
  group_by(location_type) %>%
  summarize(count = n()) %>%
  arrange(desc(count))
```

```
## # A tibble: 6 x 2
##   location_type              count
##   <chr>                      <int>
## 1 Residential Building/House 44677
## 2 Street/Sidewalk            11252
## 3 Store/Commercial            6467
## 4 Club/Bar/Restaurant         5177
## 5 Park/Playground             1044
## 6 House of Worship             292
```

# Notes and bonus exercies:

**Note:**
- sort data frames using arrange()
- select data frame columns using select()
- filter data frame rows using filter()
- add columns using mutate()
- return specific answers using summarise()
- group things together to perform acions on them using group_by()
- get the number of things in the thing coming in from a pipe %>% operator using n()



```r
# How many calls took more than two hours to respond to?
nyc_noise_complaints %>% 
  mutate(interval = closed_date - created_date) %>% 
  filter(interval > 120) %>% 
  summarise(count = n())
```

```
## # A tibble: 1 x 1
##    count
##    <int>
## 1 132733
```

```r
# Which city has the most reports
nyc_noise_complaints %>% 
  group_by(city) %>% 
  summarise(count = n()) %>% 
  arrange(desc(count))
```

```
## # A tibble: 49 x 2
##    city                count
##    <chr>               <int>
##  1 BROOKLYN            68909
##  2 NEW YORK            64112
##  3 BRONX               47673
##  4 STATEN ISLAND        5411
##  5 JAMAICA              4041
##  6 ASTORIA              3456
##  7 CORONA               2395
##  8 RIDGEWOOD            2228
##  9 SOUTH OZONE PARK     1852
## 10 SOUTH RICHMOND HILL  1764
## # ... with 39 more rows
```

```r
# Which borough has the most parties in houses of worship?
nyc_noise_complaints %>% 
  filter(location_type == "House of Worship") %>% 
  group_by(borough) %>%
  summarise(count = n()) %>% 
  arrange(desc(count))
```

```
## # A tibble: 5 x 2
##   borough       count
##   <chr>         <int>
## 1 BROOKLYN        292
## 2 QUEENS          115
## 3 MANHATTAN       113
## 4 BRONX            79
## 5 STATEN ISLAND     3
```

```r
# What is the percentage of police reports in each borough that were from Houses of Worship

nyc_noise_complaints %>% 
  group_by(borough) %>% 
  mutate(total_borough_reports = n()) %>% 
  filter(location_type == "House of Worship") %>% 
  summarise(count = 100 * n() / total_borough_reports) %>% 
  distinct()
```

```
## `summarise()` has grouped output by 'borough'. You can override using the `.groups` argument.
```

```
## # A tibble: 5 x 2
## # Groups:   borough [5]
##   borough        count
##   <chr>          <dbl>
## 1 BRONX         0.166 
## 2 BROOKLYN      0.424 
## 3 MANHATTAN     0.176 
## 4 QUEENS        0.300 
## 5 STATEN ISLAND 0.0554
```
