---
title: "Lab 3 Homework"
author: "Rebecca Kolesar-Price"
date: "1/18/23"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

```r
#view(sleep)
```

## Load the tidyverse

```r
library(tidyverse)
```

## Mammals Sleep
1. For this assignment, we are going to use built-in data on mammal sleep patterns. From which publication are these data taken from? Since the data are built-in you can use the help function in R.

```r
sleep<-(msleep)
```

2. Store these data into a new data frame `sleep`.

```r
sleep <- readr::read_csv("data/mammals_sleep_allison_cicchetti_1976.csv")
```

```
## Rows: 62 Columns: 11
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): species
## dbl (10): body weight in kg, brain weight in g, slow wave ("nondreaming") sl...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
str(sleep)
```

```
## spc_tbl_ [62 × 11] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ species                                                        : chr [1:62] "African elephant" "African giant pouched rat" "Arctic Fox" "Arctic ground squirrel" ...
##  $ body weight in kg                                              : num [1:62] 6654 1 3.38 0.92 2547 ...
##  $ brain weight in g                                              : num [1:62] 5712 6.6 44.5 5.7 4603 ...
##  $ slow wave ("nondreaming") sleep (hrs/day)                      : num [1:62] -999 6.3 -999 -999 2.1 9.1 15.8 5.2 10.9 8.3 ...
##  $ paradoxical ("dreaming") sleep (hrs/day)                       : num [1:62] -999 2 -999 -999 1.8 0.7 3.9 1 3.6 1.4 ...
##  $ total sleep (hrs/day)  (sum of slow wave and paradoxical sleep): num [1:62] 3.3 8.3 12.5 16.5 3.9 9.8 19.7 6.2 14.5 9.7 ...
##  $ maximum life span (years)                                      : num [1:62] 38.6 4.5 14 -999 69 27 19 30.4 28 50 ...
##  $ gestation time (days)                                          : num [1:62] 645 42 60 25 624 180 35 392 63 230 ...
##  $ predation index (1-5)                                          : num [1:62] 3 3 1 5 3 4 1 4 1 1 ...
##  $ sleep exposure index (1-5)                                     : num [1:62] 5 1 1 2 5 4 1 5 2 1 ...
##  $ overall danger index (1-5)                                     : num [1:62] 3 3 1 3 4 4 1 4 1 1 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   species = col_character(),
##   ..   `body weight in kg` = col_double(),
##   ..   `brain weight in g` = col_double(),
##   ..   `slow wave ("nondreaming") sleep (hrs/day)` = col_double(),
##   ..   `paradoxical ("dreaming") sleep (hrs/day)` = col_double(),
##   ..   `total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)` = col_double(),
##   ..   `maximum life span (years)` = col_double(),
##   ..   `gestation time (days)` = col_double(),
##   ..   `predation index (1-5)` = col_double(),
##   ..   `sleep exposure index (1-5)` = col_double(),
##   ..   `overall danger index (1-5)` = col_double()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

3. What are the dimensions of this data frame (variables and observations)? How do you know? Please show the *code* that you used to determine this below.  

```r
dim(sleep)
```

```
## [1] 62 11
```

4. Are there any NAs in the data? How did you determine this? Please show your code.  

```r
anyNA.data.frame(sleep)
```

```
## [1] FALSE
```

```r
is.na.data.frame(sleep)
```

```
##       species body weight in kg brain weight in g
##  [1,]   FALSE             FALSE             FALSE
##  [2,]   FALSE             FALSE             FALSE
##  [3,]   FALSE             FALSE             FALSE
##  [4,]   FALSE             FALSE             FALSE
##  [5,]   FALSE             FALSE             FALSE
##  [6,]   FALSE             FALSE             FALSE
##  [7,]   FALSE             FALSE             FALSE
##  [8,]   FALSE             FALSE             FALSE
##  [9,]   FALSE             FALSE             FALSE
## [10,]   FALSE             FALSE             FALSE
## [11,]   FALSE             FALSE             FALSE
## [12,]   FALSE             FALSE             FALSE
## [13,]   FALSE             FALSE             FALSE
## [14,]   FALSE             FALSE             FALSE
## [15,]   FALSE             FALSE             FALSE
## [16,]   FALSE             FALSE             FALSE
## [17,]   FALSE             FALSE             FALSE
## [18,]   FALSE             FALSE             FALSE
## [19,]   FALSE             FALSE             FALSE
## [20,]   FALSE             FALSE             FALSE
## [21,]   FALSE             FALSE             FALSE
## [22,]   FALSE             FALSE             FALSE
## [23,]   FALSE             FALSE             FALSE
## [24,]   FALSE             FALSE             FALSE
## [25,]   FALSE             FALSE             FALSE
## [26,]   FALSE             FALSE             FALSE
## [27,]   FALSE             FALSE             FALSE
## [28,]   FALSE             FALSE             FALSE
## [29,]   FALSE             FALSE             FALSE
## [30,]   FALSE             FALSE             FALSE
## [31,]   FALSE             FALSE             FALSE
## [32,]   FALSE             FALSE             FALSE
## [33,]   FALSE             FALSE             FALSE
## [34,]   FALSE             FALSE             FALSE
## [35,]   FALSE             FALSE             FALSE
## [36,]   FALSE             FALSE             FALSE
## [37,]   FALSE             FALSE             FALSE
## [38,]   FALSE             FALSE             FALSE
## [39,]   FALSE             FALSE             FALSE
## [40,]   FALSE             FALSE             FALSE
## [41,]   FALSE             FALSE             FALSE
## [42,]   FALSE             FALSE             FALSE
## [43,]   FALSE             FALSE             FALSE
## [44,]   FALSE             FALSE             FALSE
## [45,]   FALSE             FALSE             FALSE
## [46,]   FALSE             FALSE             FALSE
## [47,]   FALSE             FALSE             FALSE
## [48,]   FALSE             FALSE             FALSE
## [49,]   FALSE             FALSE             FALSE
## [50,]   FALSE             FALSE             FALSE
## [51,]   FALSE             FALSE             FALSE
## [52,]   FALSE             FALSE             FALSE
## [53,]   FALSE             FALSE             FALSE
## [54,]   FALSE             FALSE             FALSE
## [55,]   FALSE             FALSE             FALSE
## [56,]   FALSE             FALSE             FALSE
## [57,]   FALSE             FALSE             FALSE
## [58,]   FALSE             FALSE             FALSE
## [59,]   FALSE             FALSE             FALSE
## [60,]   FALSE             FALSE             FALSE
## [61,]   FALSE             FALSE             FALSE
## [62,]   FALSE             FALSE             FALSE
##       slow wave ("nondreaming") sleep (hrs/day)
##  [1,]                                     FALSE
##  [2,]                                     FALSE
##  [3,]                                     FALSE
##  [4,]                                     FALSE
##  [5,]                                     FALSE
##  [6,]                                     FALSE
##  [7,]                                     FALSE
##  [8,]                                     FALSE
##  [9,]                                     FALSE
## [10,]                                     FALSE
## [11,]                                     FALSE
## [12,]                                     FALSE
## [13,]                                     FALSE
## [14,]                                     FALSE
## [15,]                                     FALSE
## [16,]                                     FALSE
## [17,]                                     FALSE
## [18,]                                     FALSE
## [19,]                                     FALSE
## [20,]                                     FALSE
## [21,]                                     FALSE
## [22,]                                     FALSE
## [23,]                                     FALSE
## [24,]                                     FALSE
## [25,]                                     FALSE
## [26,]                                     FALSE
## [27,]                                     FALSE
## [28,]                                     FALSE
## [29,]                                     FALSE
## [30,]                                     FALSE
## [31,]                                     FALSE
## [32,]                                     FALSE
## [33,]                                     FALSE
## [34,]                                     FALSE
## [35,]                                     FALSE
## [36,]                                     FALSE
## [37,]                                     FALSE
## [38,]                                     FALSE
## [39,]                                     FALSE
## [40,]                                     FALSE
## [41,]                                     FALSE
## [42,]                                     FALSE
## [43,]                                     FALSE
## [44,]                                     FALSE
## [45,]                                     FALSE
## [46,]                                     FALSE
## [47,]                                     FALSE
## [48,]                                     FALSE
## [49,]                                     FALSE
## [50,]                                     FALSE
## [51,]                                     FALSE
## [52,]                                     FALSE
## [53,]                                     FALSE
## [54,]                                     FALSE
## [55,]                                     FALSE
## [56,]                                     FALSE
## [57,]                                     FALSE
## [58,]                                     FALSE
## [59,]                                     FALSE
## [60,]                                     FALSE
## [61,]                                     FALSE
## [62,]                                     FALSE
##       paradoxical ("dreaming") sleep (hrs/day)
##  [1,]                                    FALSE
##  [2,]                                    FALSE
##  [3,]                                    FALSE
##  [4,]                                    FALSE
##  [5,]                                    FALSE
##  [6,]                                    FALSE
##  [7,]                                    FALSE
##  [8,]                                    FALSE
##  [9,]                                    FALSE
## [10,]                                    FALSE
## [11,]                                    FALSE
## [12,]                                    FALSE
## [13,]                                    FALSE
## [14,]                                    FALSE
## [15,]                                    FALSE
## [16,]                                    FALSE
## [17,]                                    FALSE
## [18,]                                    FALSE
## [19,]                                    FALSE
## [20,]                                    FALSE
## [21,]                                    FALSE
## [22,]                                    FALSE
## [23,]                                    FALSE
## [24,]                                    FALSE
## [25,]                                    FALSE
## [26,]                                    FALSE
## [27,]                                    FALSE
## [28,]                                    FALSE
## [29,]                                    FALSE
## [30,]                                    FALSE
## [31,]                                    FALSE
## [32,]                                    FALSE
## [33,]                                    FALSE
## [34,]                                    FALSE
## [35,]                                    FALSE
## [36,]                                    FALSE
## [37,]                                    FALSE
## [38,]                                    FALSE
## [39,]                                    FALSE
## [40,]                                    FALSE
## [41,]                                    FALSE
## [42,]                                    FALSE
## [43,]                                    FALSE
## [44,]                                    FALSE
## [45,]                                    FALSE
## [46,]                                    FALSE
## [47,]                                    FALSE
## [48,]                                    FALSE
## [49,]                                    FALSE
## [50,]                                    FALSE
## [51,]                                    FALSE
## [52,]                                    FALSE
## [53,]                                    FALSE
## [54,]                                    FALSE
## [55,]                                    FALSE
## [56,]                                    FALSE
## [57,]                                    FALSE
## [58,]                                    FALSE
## [59,]                                    FALSE
## [60,]                                    FALSE
## [61,]                                    FALSE
## [62,]                                    FALSE
##       total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)
##  [1,]                                                           FALSE
##  [2,]                                                           FALSE
##  [3,]                                                           FALSE
##  [4,]                                                           FALSE
##  [5,]                                                           FALSE
##  [6,]                                                           FALSE
##  [7,]                                                           FALSE
##  [8,]                                                           FALSE
##  [9,]                                                           FALSE
## [10,]                                                           FALSE
## [11,]                                                           FALSE
## [12,]                                                           FALSE
## [13,]                                                           FALSE
## [14,]                                                           FALSE
## [15,]                                                           FALSE
## [16,]                                                           FALSE
## [17,]                                                           FALSE
## [18,]                                                           FALSE
## [19,]                                                           FALSE
## [20,]                                                           FALSE
## [21,]                                                           FALSE
## [22,]                                                           FALSE
## [23,]                                                           FALSE
## [24,]                                                           FALSE
## [25,]                                                           FALSE
## [26,]                                                           FALSE
## [27,]                                                           FALSE
## [28,]                                                           FALSE
## [29,]                                                           FALSE
## [30,]                                                           FALSE
## [31,]                                                           FALSE
## [32,]                                                           FALSE
## [33,]                                                           FALSE
## [34,]                                                           FALSE
## [35,]                                                           FALSE
## [36,]                                                           FALSE
## [37,]                                                           FALSE
## [38,]                                                           FALSE
## [39,]                                                           FALSE
## [40,]                                                           FALSE
## [41,]                                                           FALSE
## [42,]                                                           FALSE
## [43,]                                                           FALSE
## [44,]                                                           FALSE
## [45,]                                                           FALSE
## [46,]                                                           FALSE
## [47,]                                                           FALSE
## [48,]                                                           FALSE
## [49,]                                                           FALSE
## [50,]                                                           FALSE
## [51,]                                                           FALSE
## [52,]                                                           FALSE
## [53,]                                                           FALSE
## [54,]                                                           FALSE
## [55,]                                                           FALSE
## [56,]                                                           FALSE
## [57,]                                                           FALSE
## [58,]                                                           FALSE
## [59,]                                                           FALSE
## [60,]                                                           FALSE
## [61,]                                                           FALSE
## [62,]                                                           FALSE
##       maximum life span (years) gestation time (days) predation index (1-5)
##  [1,]                     FALSE                 FALSE                 FALSE
##  [2,]                     FALSE                 FALSE                 FALSE
##  [3,]                     FALSE                 FALSE                 FALSE
##  [4,]                     FALSE                 FALSE                 FALSE
##  [5,]                     FALSE                 FALSE                 FALSE
##  [6,]                     FALSE                 FALSE                 FALSE
##  [7,]                     FALSE                 FALSE                 FALSE
##  [8,]                     FALSE                 FALSE                 FALSE
##  [9,]                     FALSE                 FALSE                 FALSE
## [10,]                     FALSE                 FALSE                 FALSE
## [11,]                     FALSE                 FALSE                 FALSE
## [12,]                     FALSE                 FALSE                 FALSE
## [13,]                     FALSE                 FALSE                 FALSE
## [14,]                     FALSE                 FALSE                 FALSE
## [15,]                     FALSE                 FALSE                 FALSE
## [16,]                     FALSE                 FALSE                 FALSE
## [17,]                     FALSE                 FALSE                 FALSE
## [18,]                     FALSE                 FALSE                 FALSE
## [19,]                     FALSE                 FALSE                 FALSE
## [20,]                     FALSE                 FALSE                 FALSE
## [21,]                     FALSE                 FALSE                 FALSE
## [22,]                     FALSE                 FALSE                 FALSE
## [23,]                     FALSE                 FALSE                 FALSE
## [24,]                     FALSE                 FALSE                 FALSE
## [25,]                     FALSE                 FALSE                 FALSE
## [26,]                     FALSE                 FALSE                 FALSE
## [27,]                     FALSE                 FALSE                 FALSE
## [28,]                     FALSE                 FALSE                 FALSE
## [29,]                     FALSE                 FALSE                 FALSE
## [30,]                     FALSE                 FALSE                 FALSE
## [31,]                     FALSE                 FALSE                 FALSE
## [32,]                     FALSE                 FALSE                 FALSE
## [33,]                     FALSE                 FALSE                 FALSE
## [34,]                     FALSE                 FALSE                 FALSE
## [35,]                     FALSE                 FALSE                 FALSE
## [36,]                     FALSE                 FALSE                 FALSE
## [37,]                     FALSE                 FALSE                 FALSE
## [38,]                     FALSE                 FALSE                 FALSE
## [39,]                     FALSE                 FALSE                 FALSE
## [40,]                     FALSE                 FALSE                 FALSE
## [41,]                     FALSE                 FALSE                 FALSE
## [42,]                     FALSE                 FALSE                 FALSE
## [43,]                     FALSE                 FALSE                 FALSE
## [44,]                     FALSE                 FALSE                 FALSE
## [45,]                     FALSE                 FALSE                 FALSE
## [46,]                     FALSE                 FALSE                 FALSE
## [47,]                     FALSE                 FALSE                 FALSE
## [48,]                     FALSE                 FALSE                 FALSE
## [49,]                     FALSE                 FALSE                 FALSE
## [50,]                     FALSE                 FALSE                 FALSE
## [51,]                     FALSE                 FALSE                 FALSE
## [52,]                     FALSE                 FALSE                 FALSE
## [53,]                     FALSE                 FALSE                 FALSE
## [54,]                     FALSE                 FALSE                 FALSE
## [55,]                     FALSE                 FALSE                 FALSE
## [56,]                     FALSE                 FALSE                 FALSE
## [57,]                     FALSE                 FALSE                 FALSE
## [58,]                     FALSE                 FALSE                 FALSE
## [59,]                     FALSE                 FALSE                 FALSE
## [60,]                     FALSE                 FALSE                 FALSE
## [61,]                     FALSE                 FALSE                 FALSE
## [62,]                     FALSE                 FALSE                 FALSE
##       sleep exposure index (1-5) overall danger index (1-5)
##  [1,]                      FALSE                      FALSE
##  [2,]                      FALSE                      FALSE
##  [3,]                      FALSE                      FALSE
##  [4,]                      FALSE                      FALSE
##  [5,]                      FALSE                      FALSE
##  [6,]                      FALSE                      FALSE
##  [7,]                      FALSE                      FALSE
##  [8,]                      FALSE                      FALSE
##  [9,]                      FALSE                      FALSE
## [10,]                      FALSE                      FALSE
## [11,]                      FALSE                      FALSE
## [12,]                      FALSE                      FALSE
## [13,]                      FALSE                      FALSE
## [14,]                      FALSE                      FALSE
## [15,]                      FALSE                      FALSE
## [16,]                      FALSE                      FALSE
## [17,]                      FALSE                      FALSE
## [18,]                      FALSE                      FALSE
## [19,]                      FALSE                      FALSE
## [20,]                      FALSE                      FALSE
## [21,]                      FALSE                      FALSE
## [22,]                      FALSE                      FALSE
## [23,]                      FALSE                      FALSE
## [24,]                      FALSE                      FALSE
## [25,]                      FALSE                      FALSE
## [26,]                      FALSE                      FALSE
## [27,]                      FALSE                      FALSE
## [28,]                      FALSE                      FALSE
## [29,]                      FALSE                      FALSE
## [30,]                      FALSE                      FALSE
## [31,]                      FALSE                      FALSE
## [32,]                      FALSE                      FALSE
## [33,]                      FALSE                      FALSE
## [34,]                      FALSE                      FALSE
## [35,]                      FALSE                      FALSE
## [36,]                      FALSE                      FALSE
## [37,]                      FALSE                      FALSE
## [38,]                      FALSE                      FALSE
## [39,]                      FALSE                      FALSE
## [40,]                      FALSE                      FALSE
## [41,]                      FALSE                      FALSE
## [42,]                      FALSE                      FALSE
## [43,]                      FALSE                      FALSE
## [44,]                      FALSE                      FALSE
## [45,]                      FALSE                      FALSE
## [46,]                      FALSE                      FALSE
## [47,]                      FALSE                      FALSE
## [48,]                      FALSE                      FALSE
## [49,]                      FALSE                      FALSE
## [50,]                      FALSE                      FALSE
## [51,]                      FALSE                      FALSE
## [52,]                      FALSE                      FALSE
## [53,]                      FALSE                      FALSE
## [54,]                      FALSE                      FALSE
## [55,]                      FALSE                      FALSE
## [56,]                      FALSE                      FALSE
## [57,]                      FALSE                      FALSE
## [58,]                      FALSE                      FALSE
## [59,]                      FALSE                      FALSE
## [60,]                      FALSE                      FALSE
## [61,]                      FALSE                      FALSE
## [62,]                      FALSE                      FALSE
```

5. Show a list of the column names is this data frame.

```r
names(sleep)
```

```
##  [1] "species"                                                        
##  [2] "body weight in kg"                                              
##  [3] "brain weight in g"                                              
##  [4] "slow wave (\"nondreaming\") sleep (hrs/day)"                    
##  [5] "paradoxical (\"dreaming\") sleep (hrs/day)"                     
##  [6] "total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)"
##  [7] "maximum life span (years)"                                      
##  [8] "gestation time (days)"                                          
##  [9] "predation index (1-5)"                                          
## [10] "sleep exposure index (1-5)"                                     
## [11] "overall danger index (1-5)"
```

6. How many herbivores are represented in the data?  

```r
table(sleep$vore)
```

```
## Warning: Unknown or uninitialised column: `vore`.
```

```
## < table of extent 0 >
```
There are 32 herbivores


7. We are interested in two groups; small and large mammals. Let's define small as less than or equal to 1kg body weight and large as greater than or equal to 200kg body weight. Make two new dataframes (large and small) based on these parameters.



```r
large_mammals<-filter(msleep,bodywt<=200)
large_mammals
```

```
## # A tibble: 76 × 11
##    name  genus vore  order conse…¹ sleep…² sleep…³ sleep…⁴ awake  brainwt bodywt
##    <chr> <chr> <chr> <chr> <chr>     <dbl>   <dbl>   <dbl> <dbl>    <dbl>  <dbl>
##  1 Chee… Acin… carni Carn… lc         12.1    NA    NA      11.9 NA       50    
##  2 Owl … Aotus omni  Prim… <NA>       17       1.8  NA       7    0.0155   0.48 
##  3 Moun… Aplo… herbi Rode… nt         14.4     2.4  NA       9.6 NA        1.35 
##  4 Grea… Blar… omni  Sori… lc         14.9     2.3   0.133   9.1  0.00029  0.019
##  5 Thre… Brad… herbi Pilo… <NA>       14.4     2.2   0.767   9.6 NA        3.85 
##  6 Nort… Call… carni Carn… vu          8.7     1.4   0.383  15.3 NA       20.5  
##  7 Vesp… Calo… <NA>  Rode… <NA>        7      NA    NA      17   NA        0.045
##  8 Dog   Canis carni Carn… domest…    10.1     2.9   0.333  13.9  0.07    14    
##  9 Roe … Capr… herbi Arti… lc          3      NA    NA      21    0.0982  14.8  
## 10 Goat  Capri herbi Arti… lc          5.3     0.6  NA      18.7  0.115   33.5  
## # … with 66 more rows, and abbreviated variable names ¹​conservation,
## #   ²​sleep_total, ³​sleep_rem, ⁴​sleep_cycle
```


```r
small_mammals<- filter(msleep,bodywt<=1)
```

8. What is the mean weight for both the small and large mammals?

```r
sw<-(small_mammals$bodywt)
```

```r
lw<-(large_mammals$bodywt)
```

```r
mean(sw)
```

```
## [1] 0.2596667
```


```r
mean(lw)
```

```
## [1] 20.52396
```

9. Using a similar approach as above, do large or small animals sleep longer on average?  

```r
ss<-(small_mammals$sleep_total)
```

```r
mean(ss)
```

```
## [1] 12.65833
```

```r
sl<-(large_mammals$sleep_total)
```


```r
mean(sl)
```

```
## [1] 11.09079
```

10. Which animal is the sleepiest among the entire dataframe?

```r
max(sleep$sleep_total)
```

```
## Warning: Unknown or uninitialised column: `sleep_total`.
```

```
## Warning in max(sleep$sleep_total): no non-missing arguments to max; returning
## -Inf
```

```
## [1] -Inf
```


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
