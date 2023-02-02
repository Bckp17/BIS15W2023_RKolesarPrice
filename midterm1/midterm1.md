---
title: "Midterm 1"
author: "Rebecca Kolesar-price"
date: "1/31/23"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above.  

After the first 50 minutes, please upload your code (5 points). During the second 50 minutes, you may get help from each other- but no copy/paste. Upload the last version at the end of this time, but be sure to indicate it as final. If you finish early, you are free to leave.

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean! Use the tidyverse and pipes unless otherwise indicated. This exam is worth a total of 35 points. 

Please load the following libraries.

```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
## ✔ ggplot2 3.4.0      ✔ purrr   1.0.0 
## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
## ✔ tidyr   1.2.1      ✔ stringr 1.5.0 
## ✔ readr   2.1.3      ✔ forcats 0.5.2 
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
## 
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

In the midterm 1 folder there is a second folder called `data`. Inside the `data` folder, there is a .csv file called `ecs21351-sup-0003-SupplementS1.csv`. These data are from Soykan, C. U., J. Sauer, J. G. Schuetz, G. S. LeBaron, K. Dale, and G. M. Langham. 2016. Population trends for North American winter birds based on hierarchical models. Ecosphere 7(5):e01351. 10.1002/ecs2.1351.  

Please load these data as a new object called `ecosphere`. In this step, I am providing the code to load the data, clean the variable names, and remove a footer that the authors used as part of the original publication.

```r
ecosphere <- read_csv("data/ecs21351-sup-0003-SupplementS1.csv", skip=2) %>% 
  clean_names() %>%
  slice(1:(n() - 18)) # this removes the footer
```

Problem 1. (1 point) Let's start with some data exploration. What are the variable names?

```r
variable.names(ecosphere)
```

```
##  [1] "order"                       "family"                     
##  [3] "common_name"                 "scientific_name"            
##  [5] "diet"                        "life_expectancy"            
##  [7] "habitat"                     "urban_affiliate"            
##  [9] "migratory_strategy"          "log10_mass"                 
## [11] "mean_eggs_per_clutch"        "mean_age_at_sexual_maturity"
## [13] "population_size"             "winter_range_area"          
## [15] "range_in_cbc"                "strata"                     
## [17] "circles"                     "feeder_bird"                
## [19] "median_trend"                "lower_95_percent_ci"        
## [21] "upper_95_percent_ci"
```

Problem 2. (1 point) Use the function of your choice to summarize the data.

```r
glimpse(ecosphere)
```

```
## Rows: 551
## Columns: 21
## $ order                       <chr> "Anseriformes", "Anseriformes", "Anserifor…
## $ family                      <chr> "Anatidae", "Anatidae", "Anatidae", "Anati…
## $ common_name                 <chr> "American Black Duck", "American Wigeon", …
## $ scientific_name             <chr> "Anas rubripes", "Anas americana", "Buceph…
## $ diet                        <chr> "Vegetation", "Vegetation", "Invertebrates…
## $ life_expectancy             <chr> "Long", "Middle", "Middle", "Long", "Middl…
## $ habitat                     <chr> "Wetland", "Wetland", "Wetland", "Wetland"…
## $ urban_affiliate             <chr> "No", "No", "No", "No", "No", "No", "No", …
## $ migratory_strategy          <chr> "Short", "Short", "Moderate", "Moderate", …
## $ log10_mass                  <dbl> 3.09, 2.88, 2.96, 3.11, 3.02, 2.88, 2.56, …
## $ mean_eggs_per_clutch        <dbl> 9.0, 7.5, 10.5, 3.5, 9.5, 13.5, 10.0, 8.5,…
## $ mean_age_at_sexual_maturity <dbl> 1.0, 1.0, 3.0, 2.5, 2.0, 1.0, 0.6, 2.0, 1.…
## $ population_size             <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ winter_range_area           <dbl> 3212473, 7145842, 1812841, 360134, 854350,…
## $ range_in_cbc                <dbl> 99.1, 61.7, 69.8, 53.7, 5.3, 0.5, 17.9, 72…
## $ strata                      <dbl> 82, 124, 37, 19, 36, 5, 26, 134, 145, 103,…
## $ circles                     <dbl> 1453, 1951, 502, 247, 470, 97, 479, 2189, …
## $ feeder_bird                 <chr> "No", "No", "No", "No", "No", "No", "No", …
## $ median_trend                <dbl> 1.014, 0.996, 1.039, 0.998, 1.004, 1.196, …
## $ lower_95_percent_ci         <dbl> 0.971, 0.964, 1.016, 0.956, 0.975, 1.152, …
## $ upper_95_percent_ci         <dbl> 1.055, 1.009, 1.104, 1.041, 1.036, 1.243, …
```

Problem 3. (2 points) How many distinct orders of birds are represented in the data?

```r
ecosphere %>% 
  count(order)
```

```
## # A tibble: 19 × 2
##    order                 n
##    <chr>             <int>
##  1 Anseriformes         44
##  2 Apodiformes          15
##  3 Caprimulgiformes      5
##  4 Charadriiformes      81
##  5 Ciconiiformes        29
##  6 Columbiformes        11
##  7 Coraciiformes         3
##  8 Cuculiformes          3
##  9 Falconiformes        31
## 10 Galliformes          21
## 11 Gaviiformes           4
## 12 Gruiformes           12
## 13 Passeriformes       237
## 14 Piciformes           22
## 15 Podicipediformes      6
## 16 Procellariiformes     4
## 17 Psittaciformes        6
## 18 Strigiformes         16
## 19 Trogoniformes         1
```

Problem 4. (2 points) Which habitat has the highest diversity (number of species) in the data?

```r
#Woodland has the highest diversity with 177 species

ecosphere %>% 
  group_by(habitat) %>% 
  summarise(max_diversity=sum(n_distinct(scientific_name))) %>% 
  arrange(desc(max_diversity))
```

```
## # A tibble: 7 × 2
##   habitat   max_diversity
##   <chr>             <int>
## 1 Woodland            177
## 2 Wetland             153
## 3 Shrubland            82
## 4 Various              45
## 5 Ocean                44
## 6 Grassland            36
## 7 <NA>                 14
```


Run the code below to learn about the `slice` function. Look specifically at the examples (at the bottom) for `slice_max()` and `slice_min()`. If you are still unsure, try looking up examples online (https://rpubs.com/techanswers88/dplyr-slice). Use this new function to answer question 5 below.

```r
?slice_max
```

Problem 5. (4 points) Using the `slice_max()` or `slice_min()` function described above which species has the largest and smallest winter range?

```r
ecosphere %>% 
  slice_max(winter_range_area) %>% 
  select(common_name,habitat, winter_range_area)
```

```
## # A tibble: 1 × 3
##   common_name      habitat winter_range_area
##   <chr>            <chr>               <dbl>
## 1 Sooty Shearwater Ocean           185968946
```


```r
ecosphere %>% 
  slice_min(winter_range_area) %>% 
  select(common_name,habitat, winter_range_area)
```

```
## # A tibble: 1 × 3
##   common_name habitat   winter_range_area
##   <chr>       <chr>                 <dbl>
## 1 Skylark     Grassland                11
```

Problem 6. (2 points) The family Anatidae includes ducks, geese, and swans. Make a new object `ducks` that only includes species in the family Anatidae. Restrict this new dataframe to include all variables except order and family.

```r
ducks<- filter(ecosphere, family=="Anatidae") %>% 
  select(-"order",-"family")
```

Problem 7. (2 points) We might assume that all ducks live in wetland habitat. Is this true for the ducks in these data? If there are exceptions, list the species below.

```r
ducks %>% 
  filter(habitat!="Wetland")
```

```
## # A tibble: 1 × 19
##   common…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶ mean_…⁷ mean_…⁸
##   <chr>    <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>   <dbl>   <dbl>
## 1 Common … Somate… Inve… Middle  Ocean   No      Short      3.31       5     2.5
## # … with 9 more variables: population_size <dbl>, winter_range_area <dbl>,
## #   range_in_cbc <dbl>, strata <dbl>, circles <dbl>, feeder_bird <chr>,
## #   median_trend <dbl>, lower_95_percent_ci <dbl>, upper_95_percent_ci <dbl>,
## #   and abbreviated variable names ¹​common_name, ²​scientific_name,
## #   ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy, ⁶​log10_mass,
## #   ⁷​mean_eggs_per_clutch, ⁸​mean_age_at_sexual_maturity
```

Problem 8. (4 points) In ducks, how is mean body mass associated with migratory strategy? Do the ducks that migrate long distances have high or low average body mass?

```r
ducks%>% 
  group_by(migratory_strategy) %>% 
  summarise(body_mass=mean(log10_mass))
```

```
## # A tibble: 5 × 2
##   migratory_strategy body_mass
##   <chr>                  <dbl>
## 1 Long                    2.87
## 2 Moderate                3.11
## 3 Resident                4.03
## 4 Short                   2.98
## 5 Withdrawal              2.92
```


Problem 9. (2 points) Accipitridae is the family that includes eagles, hawks, kites, and osprey. First, make a new object `eagles` that only includes species in the family Accipitridae. Next, restrict these data to only include the variables common_name, scientific_name, and population_size.

```r
eagles<- filter(ecosphere, family=="Accipitridae") %>% 
  select(common_name, scientific_name, population_size)
eagles
```

```
## # A tibble: 20 × 3
##    common_name         scientific_name          population_size
##    <chr>               <chr>                              <dbl>
##  1 Bald Eagle          Haliaeetus leucocephalus              NA
##  2 Broad-winged Hawk   Buteo platypterus                1700000
##  3 Cooper's Hawk       Accipiter cooperii                700000
##  4 Ferruginous Hawk    Buteo regalis                      80000
##  5 Golden Eagle        Aquila chrysaetos                 130000
##  6 Gray Hawk           Buteo nitidus                         NA
##  7 Harris's Hawk       Parabuteo unicinctus               50000
##  8 Hook-billed Kite    Chondrohierax uncinatus               NA
##  9 Northern Goshawk    Accipiter gentilis                200000
## 10 Northern Harrier    Circus cyaneus                    700000
## 11 Red-shouldered Hawk Buteo lineatus                   1100000
## 12 Red-tailed Hawk     Buteo jamaicensis                2000000
## 13 Rough-legged Hawk   Buteo lagopus                     300000
## 14 Sharp-shinned Hawk  Accipiter striatus                500000
## 15 Short-tailed Hawk   Buteo brachyurus                      NA
## 16 Snail Kite          Rostrhamus sociabilis                 NA
## 17 Swainson's Hawk     Buteo swainsoni                   540000
## 18 White-tailed Hawk   Buteo albicaudatus                    NA
## 19 White-tailed Kite   Elanus leucurus                       NA
## 20 Zone-tailed Hawk    Buteo albonotatus                     NA
```

Problem 10. (4 points) In the eagles data, any species with a population size less than 250,000 individuals is threatened. Make a new column `conservation_status` that shows whether or not a species is threatened.

```r
eagles %>% 
  mutate(conservation_status=population_size<250000) %>% 
  filter(!is.na(population_size)) %>% 
  select(common_name, conservation_status)
```

```
## # A tibble: 12 × 2
##    common_name         conservation_status
##    <chr>               <lgl>              
##  1 Broad-winged Hawk   FALSE              
##  2 Cooper's Hawk       FALSE              
##  3 Ferruginous Hawk    TRUE               
##  4 Golden Eagle        TRUE               
##  5 Harris's Hawk       TRUE               
##  6 Northern Goshawk    TRUE               
##  7 Northern Harrier    FALSE              
##  8 Red-shouldered Hawk FALSE              
##  9 Red-tailed Hawk     FALSE              
## 10 Rough-legged Hawk   FALSE              
## 11 Sharp-shinned Hawk  FALSE              
## 12 Swainson's Hawk     FALSE
```

Problem 11. (2 points) Consider the results from questions 9 and 10. Are there any species for which their threatened status needs further study? How do you know?

```r
#There is multiple catagories that include NAs, the species that would require more research would be the one below that appear as NA.
eagles %>% 
  mutate(conservation_status=population_size<250000) %>% 
  select(common_name, conservation_status)
```

```
## # A tibble: 20 × 2
##    common_name         conservation_status
##    <chr>               <lgl>              
##  1 Bald Eagle          NA                 
##  2 Broad-winged Hawk   FALSE              
##  3 Cooper's Hawk       FALSE              
##  4 Ferruginous Hawk    TRUE               
##  5 Golden Eagle        TRUE               
##  6 Gray Hawk           NA                 
##  7 Harris's Hawk       TRUE               
##  8 Hook-billed Kite    NA                 
##  9 Northern Goshawk    TRUE               
## 10 Northern Harrier    FALSE              
## 11 Red-shouldered Hawk FALSE              
## 12 Red-tailed Hawk     FALSE              
## 13 Rough-legged Hawk   FALSE              
## 14 Sharp-shinned Hawk  FALSE              
## 15 Short-tailed Hawk   NA                 
## 16 Snail Kite          NA                 
## 17 Swainson's Hawk     FALSE              
## 18 White-tailed Hawk   NA                 
## 19 White-tailed Kite   NA                 
## 20 Zone-tailed Hawk    NA
```

Problem 12. (4 points) Use the `ecosphere` data to perform one exploratory analysis of your choice. The analysis must have a minimum of three lines and two functions. You must also clearly state the question you are attempting to answer.

```r
#which birds lay at least 2 eggs per clutch above sexual maturity of 4
ecosphere %>% 
  group_by(mean_age_at_sexual_maturity) %>% 
  filter(mean_age_at_sexual_maturity>4) %>% 
  filter(mean_eggs_per_clutch>=2) %>% 
  select(common_name,mean_age_at_sexual_maturity,mean_eggs_per_clutch) %>% 
  arrange(desc(mean_age_at_sexual_maturity))
```

```
## # A tibble: 15 × 3
## # Groups:   mean_age_at_sexual_maturity [5]
##    common_name              mean_age_at_sexual_maturity mean_eggs_per_clutch
##    <chr>                                          <dbl>                <dbl>
##  1 Turkey Vulture                                  10.5                  2  
##  2 Black Vulture                                    7.5                  2  
##  3 Trumpeter Swan                                   5.5                  4.5
##  4 Glaucous-winged Gull                             5.5                  3  
##  5 Golden Eagle                                     5.5                  2.5
##  6 Brown Jay                                        5                    4  
##  7 Black Oystercatcher                              4.5                  2.5
##  8 Great Black-backed Gull                          4.5                  2.5
##  9 Lesser Black-backed Gull                         4.5                  3  
## 10 Western Gull                                     4.5                  3  
## 11 Yellow-footed Gull                               4.5                  3  
## 12 Gull-billed Tern                                 4.5                  2  
## 13 Bald Eagle                                       4.5                  2  
## 14 Sandhill Crane                                   4.5                  2  
## 15 Whooping Crane                                   4.5                  2
```


Please provide the names of the students you have worked with with during the exam:

```r
#Ananda leia
```

Please be 100% sure your exam is saved, knitted, and pushed to your github repository. No need to submit a link on canvas, we will find your exam in your repository.
