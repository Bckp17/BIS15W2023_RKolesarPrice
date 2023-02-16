---
title: "Lab 10 Homework"
author: "Rebecca Kolesar-Price"
date: "2/15/23"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above. For any included plots, make sure they are clearly labeled. You are free to use any plot type that you feel best communicates the results of your analysis.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(here)
library(naniar)
```

## Desert Ecology
For this assignment, we are going to use a modified data set on [desert ecology](http://esapubs.org/archive/ecol/E090/118/). The data are from: S. K. Morgan Ernest, Thomas J. Valone, and James H. Brown. 2009. Long-term monitoring and experimental manipulation of a Chihuahuan Desert ecosystem near Portal, Arizona, USA. Ecology 90:1708.

```r
deserts <- read_csv(here("lab10", "data", "surveys_complete.csv"))
```

```
## Rows: 34786 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (6): species_id, sex, genus, species, taxa, plot_type
## dbl (7): record_id, month, day, year, plot_id, hindfoot_length, weight
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

1. Use the function(s) of your choice to get an idea of its structure, including how NA's are treated. Are the data tidy?  

```r
naniar::all_na(deserts)
```

```
## [1] FALSE
```

```r
deserts %>% 
  summarize(number_nas = sum(is.na(weight)))
```

```
## # A tibble: 1 × 1
##   number_nas
##        <int>
## 1       2503
```

2. How many genera and species are represented in the data? What are the total number of observations? Which species is most/ least frequently sampled in the study?

```r
deserts %>% 
  select(genus,species) %>% 
  summarise(n_genera=n_distinct(genus),
            n_species=n_distinct(species),
            n=n())
```

```
## # A tibble: 1 × 3
##   n_genera n_species     n
##      <int>     <int> <int>
## 1       26        40 34786
```

3. What is the proportion of taxa included in this study? Show a table and plot that reflects this count.

```r
deserts %>% 
  count(taxa) %>% 
  ggplot(aes(x=taxa, y=log10(n))) + geom_col()
```

![](lab10_hw_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

4. For the taxa included in the study, use the fill option to show the proportion of individuals sampled by `plot_type.`

```r
deserts %>% 
  ggplot(aes(x=taxa, fill=taxa))+
  geom_bar()+
  scale_y_log10()+
  theme(plot.title = element_text(size = rel(2), hjust = 0.5))
```

![](lab10_hw_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

5. What is the range of weight for each species included in the study? Remove any observations of weight that are NA so they do not show up in the plot.

```r
deserts %>% 
  filter(weight!="NA") %>% 
   ggplot(aes(x=species, y=weight, fill=species)) +
  geom_col()+
  coord_flip()+
  scale_y_log10()
```

![](lab10_hw_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

6. Add another layer to your answer from #4 using `geom_point` to get an idea of how many measurements were taken for each species.

```r
deserts %>% 
  filter(weight!="NA") %>% 
   ggplot(aes(x=species, y=weight, fill=species)) +
  geom_col()+ 
  geom_point(alpha=0.3, color="tomato", position = "jitter")+
  coord_flip()+
  scale_y_log10()
```

![](lab10_hw_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

7. [Dipodomys merriami](https://en.wikipedia.org/wiki/Merriam's_kangaroo_rat) is the most frequently sampled animal in the study. How have the number of observations of this species changed over the years included in the study?

```r
deserts %>% 
  filter(species_id=="DM") %>% 
  group_by(year) %>% 
  summarize(n_samples=n()) %>% 
  ggplot(aes(x=as.factor(year), y=n_samples, fill=as.factor(year))) + 
  geom_col()+
  theme(axis.text.x = element_text(angle = 90, hjust = 0.5))+
  labs(title = "Dipodomys merriami",
       x = NULL,
       y= "n")
```

![](lab10_hw_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

8. What is the relationship between `weight` and `hindfoot` length? Consider whether or not over plotting is an issue.

```r
deserts %>% 
  ggplot(aes(x=weight, y=hindfoot_length, fill=hindfoot_length))+
  geom_line(na.rm=T, size=.5)+
  theme(plot.title = element_text(size = rel(1), hjust = 0.5))+
  labs(title = " Weight VS Hindfoot length",
       x = "Weight",
       y = "Hindfoot length")
```

```
## Warning: Using `size` aesthetic for lines was deprecated in ggplot2 3.4.0.
## ℹ Please use `linewidth` instead.
```

![](lab10_hw_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

9. Which two species have, on average, the highest weight? Once you have identified them, make a new column that is a ratio of `weight` to `hindfoot_length`. Make a plot that shows the range of this new ratio and fill by sex.

```r
deserts %>% 
  filter(species_id=="NL" | species_id=="DS") %>% 
  filter(weight!="NA" & hindfoot_length!="NA" & sex!="NA") %>% 
  mutate(ratio=weight/hindfoot_length) %>% 
  select(species_id, sex, weight, hindfoot_length, ratio) %>% 
  ggplot(aes(x=species_id, y=ratio, fill=sex)) + geom_boxplot()+
  labs(title = "Weight/ Hindfoot Length Range",
       x = "Species ID",
       y = "Weight/Hindfoot Length") 
```

![](lab10_hw_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

10. Make one plot of your choice! Make sure to include at least two of the aesthetics options you have learned.

```r
deserts %>% 
  ggplot(aes(x=sex, y=plot_id, fill=sex))+
  geom_col()+
  coord_flip()+ theme(plot.title =  element_text(size = rel(1), hjust = 0.5))+
  labs(title = "Sex vs Plot ID",
       x = "SEX",
       y= "PLOT ID")
```

![](lab10_hw_files/figure-html/unnamed-chunk-12-1.png)<!-- -->

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 
