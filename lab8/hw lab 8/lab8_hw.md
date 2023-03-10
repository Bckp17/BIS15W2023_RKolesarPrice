---
title: "Lab 8 Homework"
author: "Rebecca Kolesar-Price"
date: "2/9/23"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(here)
```

## Install `here`
The package `here` is a nice option for keeping directories clear when loading files. I will demonstrate below and let you decide if it is something you want to use.  

```r
#install.packages("here")
```

## Data
For this homework, we will use a data set compiled by the Office of Environment and Heritage in New South Whales, Australia. It contains the enterococci counts in water samples obtained from Sydney beaches as part of the Beachwatch Water Quality Program. Enterococci are bacteria common in the intestines of mammals; they are rarely present in clean water. So, enterococci values are a measurement of pollution. `cfu` stands for colony forming units and measures the number of viable bacteria in a sample [cfu](https://en.wikipedia.org/wiki/Colony-forming_unit).   

This homework loosely follows the tutorial of [R Ladies Sydney](https://rladiessydney.org/). If you get stuck, check it out!  

1. Start by loading the data `sydneybeaches`. Do some exploratory analysis to get an idea of the data structure.

```r
sydney_beaches<-read.csv(here("hw lab 8", "data2", "sydneybeaches.csv"))
glimpse(sydney_beaches)
```

```
## Rows: 3,690
## Columns: 8
## $ BeachId                 <dbl> 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, 25…
## $ Region                  <chr> "Sydney City Ocean Beaches", "Sydney City Ocea…
## $ Council                 <chr> "Randwick Council", "Randwick Council", "Randw…
## $ Site                    <chr> "Clovelly Beach", "Clovelly Beach", "Clovelly …
## $ Longitude               <dbl> 151.2675, 151.2675, 151.2675, 151.2675, 151.26…
## $ Latitude                <dbl> -33.91449, -33.91449, -33.91449, -33.91449, -3…
## $ Date                    <chr> "02/01/2013", "06/01/2013", "12/01/2013", "18/…
## $ Enterococci..cfu.100ml. <int> 19, 3, 2, 13, 8, 7, 11, 97, 3, 0, 6, 0, 1, 8, …
```

```r
anyNA(sydney_beaches)
```

```
## [1] TRUE
```

If you want to try `here`, first notice the output when you load the `here` library. It gives you information on the current working directory. You can then use it to easily and intuitively load files.

```r
library(here)
```

The quotes show the folder structure from the root directory.

```r
sydneybeaches <-read_csv(here("lab8", "data", "sydneybeaches.csv")) %>% janitor::clean_names()
```

```
## Rows: 3690 Columns: 8
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (4): Region, Council, Site, Date
## dbl (4): BeachId, Longitude, Latitude, Enterococci (cfu/100ml)
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

2. Are these data "tidy" per the definitions of the tidyverse? How do you know? Are they in wide or long format?


3. We are only interested in the variables site, date, and enterococci_cfu_100ml. Make a new object focused on these variables only. Name the object `sydneybeaches_long`

```r
sydneybeachs_long<-
  sydneybeaches %>% 
  select("site","date","enterococci_cfu_100ml")
sydneybeachs_long
```

```
## # A tibble: 3,690 × 3
##    site           date       enterococci_cfu_100ml
##    <chr>          <chr>                      <dbl>
##  1 Clovelly Beach 02/01/2013                    19
##  2 Clovelly Beach 06/01/2013                     3
##  3 Clovelly Beach 12/01/2013                     2
##  4 Clovelly Beach 18/01/2013                    13
##  5 Clovelly Beach 30/01/2013                     8
##  6 Clovelly Beach 05/02/2013                     7
##  7 Clovelly Beach 11/02/2013                    11
##  8 Clovelly Beach 23/02/2013                    97
##  9 Clovelly Beach 07/03/2013                     3
## 10 Clovelly Beach 25/03/2013                     0
## # … with 3,680 more rows
```


4. Pivot the data such that the dates are column names and each beach only appears once. Name the object `sydneybeaches_wide`

```r
sydneybeaches_wide<- sydneybeachs_long %>% 
  pivot_wider(names_from = "site",
              values_from = "enterococci_cfu_100ml")
sydneybeaches_wide
```

```
## # A tibble: 344 × 12
##    date  Clove…¹ Cooge…² Gordo…³ Littl…⁴ Malab…⁵ Marou…⁶ South…⁷ South…⁸ Bondi…⁹
##    <chr>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
##  1 02/0…      19      15      NA       9       2       1       1      12       3
##  2 06/0…       3       4      NA       3       4       1       0       2       1
##  3 12/0…       2      17      NA      72     390      20      33     110       2
##  4 18/0…      13      18      NA       1      15       2       2      13       1
##  5 30/0…       8      22      NA      44      13      11      13     100       6
##  6 05/0…       7       2      NA       7      13       0       0     630       5
##  7 11/0…      11     110      NA     150     140       4      30      79     600
##  8 23/0…      97     630      NA     330     390      60      92     570      67
##  9 07/0…       3      11      NA      31       6       1      13      69       1
## 10 25/0…       0      82       4     420      28      33      17      37       0
## # … with 334 more rows, 2 more variables: `Bronte Beach` <dbl>,
## #   `Tamarama Beach` <dbl>, and abbreviated variable names ¹​`Clovelly Beach`,
## #   ²​`Coogee Beach`, ³​`Gordons Bay (East)`, ⁴​`Little Bay Beach`,
## #   ⁵​`Malabar Beach`, ⁶​`Maroubra Beach`, ⁷​`South Maroubra Beach`,
## #   ⁸​`South Maroubra Rockpool`, ⁹​`Bondi Beach`
```


5. Pivot the data back so that the dates are data and not column names.

```r
sydneybeaches_wide %>% 
 pivot_longer(-date,
               names_to="site",
               values_to="enterococci_cfu_100ml"
               )
```

```
## # A tibble: 3,784 × 3
##    date       site                    enterococci_cfu_100ml
##    <chr>      <chr>                                   <dbl>
##  1 02/01/2013 Clovelly Beach                             19
##  2 02/01/2013 Coogee Beach                               15
##  3 02/01/2013 Gordons Bay (East)                         NA
##  4 02/01/2013 Little Bay Beach                            9
##  5 02/01/2013 Malabar Beach                               2
##  6 02/01/2013 Maroubra Beach                              1
##  7 02/01/2013 South Maroubra Beach                        1
##  8 02/01/2013 South Maroubra Rockpool                    12
##  9 02/01/2013 Bondi Beach                                 3
## 10 02/01/2013 Bronte Beach                                4
## # … with 3,774 more rows
```


6. We haven't dealt much with dates yet, but separate the date into columns day, month, and year. Do this on the `sydneybeaches_long` data.


```r
sydneybeaches_long_date<-sydneybeachs_long%>%
  separate(date,into = c("day","month","year"),sep="/")
sydneybeaches_long_date
```

```
## # A tibble: 3,690 × 5
##    site           day   month year  enterococci_cfu_100ml
##    <chr>          <chr> <chr> <chr>                 <dbl>
##  1 Clovelly Beach 02    01    2013                     19
##  2 Clovelly Beach 06    01    2013                      3
##  3 Clovelly Beach 12    01    2013                      2
##  4 Clovelly Beach 18    01    2013                     13
##  5 Clovelly Beach 30    01    2013                      8
##  6 Clovelly Beach 05    02    2013                      7
##  7 Clovelly Beach 11    02    2013                     11
##  8 Clovelly Beach 23    02    2013                     97
##  9 Clovelly Beach 07    03    2013                      3
## 10 Clovelly Beach 25    03    2013                      0
## # … with 3,680 more rows
```

7. What is the average `enterococci_cfu_100ml` by year for each beach. Think about which data you will use- long or wide.

```r
sydeny_beaches_mean <- sydneybeaches_long_date  %>% 
  group_by(site, year) %>% 
  summarize(mean_enterococci_cfu_100ml=mean(enterococci_cfu_100ml, na.rm=T))
```

```
## `summarise()` has grouped output by 'site'. You can override using the
## `.groups` argument.
```

```r
sydeny_beaches_mean
```

```
## # A tibble: 66 × 3
## # Groups:   site [11]
##    site         year  mean_enterococci_cfu_100ml
##    <chr>        <chr>                      <dbl>
##  1 Bondi Beach  2013                        32.2
##  2 Bondi Beach  2014                        11.1
##  3 Bondi Beach  2015                        14.3
##  4 Bondi Beach  2016                        19.4
##  5 Bondi Beach  2017                        13.2
##  6 Bondi Beach  2018                        22.9
##  7 Bronte Beach 2013                        26.8
##  8 Bronte Beach 2014                        17.5
##  9 Bronte Beach 2015                        23.6
## 10 Bronte Beach 2016                        61.3
## # … with 56 more rows
```


8. Make the output from question 7 easier to read by pivoting it to wide format.

```r
sydneybeaches_mean_wide<-sydeny_beaches_mean%>%
  pivot_wider(names_from = "year",
              values_from = "mean_enterococci_cfu_100ml")
sydneybeaches_mean_wide
```

```
## # A tibble: 11 × 7
## # Groups:   site [11]
##    site                    `2013` `2014` `2015` `2016` `2017` `2018`
##    <chr>                    <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>
##  1 Bondi Beach              32.2   11.1   14.3    19.4  13.2   22.9 
##  2 Bronte Beach             26.8   17.5   23.6    61.3  16.8   43.4 
##  3 Clovelly Beach            9.28  13.8    8.82   11.3   7.93  10.6 
##  4 Coogee Beach             39.7   52.6   40.3    59.5  20.7   21.6 
##  5 Gordons Bay (East)       24.8   16.7   36.2    39.0  13.7   17.6 
##  6 Little Bay Beach        122.    19.5   25.5    31.2  18.2   59.1 
##  7 Malabar Beach           101.    54.5   66.9    91.0  49.8   38.0 
##  8 Maroubra Beach           47.1    9.23  14.5    26.6  11.6    9.21
##  9 South Maroubra Beach     39.3   14.9    8.25   10.7   8.26  12.5 
## 10 South Maroubra Rockpool  96.4   40.6   47.3    59.3  46.9  112.  
## 11 Tamarama Beach           29.7   39.6   57.0    50.3  20.4   15.5
```


9. What was the most polluted beach in 2018?

```r
sydeny_beaches_mean %>% 
  select("site","mean_enterococci_cfu_100ml") %>% 
  slice_max(mean_enterococci_cfu_100ml, n=1) %>% 
  arrange(desc(mean_enterococci_cfu_100ml))
```

```
## # A tibble: 11 × 2
## # Groups:   site [11]
##    site                    mean_enterococci_cfu_100ml
##    <chr>                                        <dbl>
##  1 Little Bay Beach                             122. 
##  2 South Maroubra Rockpool                      112. 
##  3 Malabar Beach                                101. 
##  4 Bronte Beach                                  61.3
##  5 Coogee Beach                                  59.5
##  6 Tamarama Beach                                57.0
##  7 Maroubra Beach                                47.1
##  8 South Maroubra Beach                          39.3
##  9 Gordons Bay (East)                            39.0
## 10 Bondi Beach                                   32.2
## 11 Clovelly Beach                                13.8
```


10. Please complete the class project survey at: [BIS 15L Group Project](https://forms.gle/H2j69Z3ZtbLH3efW6)


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
