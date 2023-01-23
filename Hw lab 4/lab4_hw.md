---
title: "Lab 4 Homework"
author: "Rebecca Kolesar-Price"
date: "1/19/23"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
```

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  


**1. Load the data into a new object called `homerange`.** .

```r
homerange<-readr::read_csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Rows: 569 Columns: 24
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (16): taxon, common.name, class, order, family, genus, species, primarym...
## dbl  (8): mean.mass.g, log10.mass, mean.hra.m2, log10.hra, dimension, preyma...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```



**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**  

```r
dim(homerange)
```

```
## [1] 569  24
```

```r
names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```

```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild        dimension        preymass         log10.preymass   
##  Length:569         Min.   :2.000   Min.   :     0.67   Min.   :-0.1739  
##  Class :character   1st Qu.:2.000   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Median :2.000   Median :    53.75   Median : 1.7304  
##                     Mean   :2.218   Mean   :  3989.88   Mean   : 2.0188  
##                     3rd Qu.:2.000   3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                     Max.   :3.000   Max.   :130233.20   Max.   : 5.1147  
##                                     NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```

```r
variable.names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```

**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  

```r
homerange$taxon<-as.factor(homerange$taxon)
homerange$taxon
```

```
##   [1] lake fishes   river fishes  river fishes  river fishes  river fishes 
##   [6] river fishes  marine fishes marine fishes marine fishes marine fishes
##  [11] marine fishes marine fishes marine fishes lake fishes   lake fishes  
##  [16] lake fishes   river fishes  river fishes  lake fishes   lake fishes  
##  [21] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [26] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [31] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [36] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [41] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [46] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [51] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [56] marine fishes marine fishes marine fishes marine fishes lake fishes  
##  [61] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [66] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [71] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [76] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [81] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [86] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [91] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [96] marine fishes river fishes  river fishes  river fishes  river fishes 
## [101] lake fishes   river fishes  river fishes  river fishes  marine fishes
## [106] marine fishes marine fishes marine fishes marine fishes lake fishes  
## [111] marine fishes marine fishes marine fishes birds         birds        
## [116] birds         birds         birds         birds         birds        
## [121] birds         birds         birds         birds         birds        
## [126] birds         birds         birds         birds         birds        
## [131] birds         birds         birds         birds         birds        
## [136] birds         birds         birds         birds         birds        
## [141] birds         birds         birds         birds         birds        
## [146] birds         birds         birds         birds         birds        
## [151] birds         birds         birds         birds         birds        
## [156] birds         birds         birds         birds         birds        
## [161] birds         birds         birds         birds         birds        
## [166] birds         birds         birds         birds         birds        
## [171] birds         birds         birds         birds         birds        
## [176] birds         birds         birds         birds         birds        
## [181] birds         birds         birds         birds         birds        
## [186] birds         birds         birds         birds         birds        
## [191] birds         birds         birds         birds         birds        
## [196] birds         birds         birds         birds         birds        
## [201] birds         birds         birds         birds         birds        
## [206] birds         birds         birds         birds         birds        
## [211] birds         birds         birds         birds         birds        
## [216] birds         birds         birds         birds         birds        
## [221] birds         birds         birds         birds         birds        
## [226] birds         birds         birds         birds         birds        
## [231] birds         birds         birds         birds         birds        
## [236] birds         birds         birds         birds         birds        
## [241] birds         birds         birds         birds         birds        
## [246] birds         birds         birds         birds         birds        
## [251] birds         birds         birds         mammals       mammals      
## [256] mammals       mammals       mammals       mammals       mammals      
## [261] mammals       mammals       mammals       mammals       mammals      
## [266] mammals       mammals       mammals       mammals       mammals      
## [271] mammals       mammals       mammals       mammals       mammals      
## [276] mammals       mammals       mammals       mammals       mammals      
## [281] mammals       mammals       mammals       mammals       mammals      
## [286] mammals       mammals       mammals       mammals       mammals      
## [291] mammals       mammals       mammals       mammals       mammals      
## [296] mammals       mammals       mammals       mammals       mammals      
## [301] mammals       mammals       mammals       mammals       mammals      
## [306] mammals       mammals       mammals       mammals       mammals      
## [311] mammals       mammals       mammals       mammals       mammals      
## [316] mammals       mammals       mammals       mammals       mammals      
## [321] mammals       mammals       mammals       mammals       mammals      
## [326] mammals       mammals       mammals       mammals       mammals      
## [331] mammals       mammals       mammals       mammals       mammals      
## [336] mammals       mammals       mammals       mammals       mammals      
## [341] mammals       mammals       mammals       mammals       mammals      
## [346] mammals       mammals       mammals       mammals       mammals      
## [351] mammals       mammals       mammals       mammals       mammals      
## [356] mammals       mammals       mammals       mammals       mammals      
## [361] mammals       mammals       mammals       mammals       mammals      
## [366] mammals       mammals       mammals       mammals       mammals      
## [371] mammals       mammals       mammals       mammals       mammals      
## [376] mammals       mammals       mammals       mammals       mammals      
## [381] mammals       mammals       mammals       mammals       mammals      
## [386] mammals       mammals       mammals       mammals       mammals      
## [391] mammals       mammals       mammals       mammals       mammals      
## [396] mammals       mammals       mammals       mammals       mammals      
## [401] mammals       mammals       mammals       mammals       mammals      
## [406] mammals       mammals       mammals       mammals       mammals      
## [411] mammals       mammals       mammals       mammals       mammals      
## [416] mammals       mammals       mammals       mammals       mammals      
## [421] mammals       mammals       mammals       mammals       mammals      
## [426] mammals       mammals       mammals       mammals       mammals      
## [431] mammals       mammals       mammals       mammals       mammals      
## [436] mammals       mammals       mammals       mammals       mammals      
## [441] mammals       mammals       mammals       mammals       mammals      
## [446] mammals       mammals       mammals       mammals       mammals      
## [451] mammals       mammals       mammals       mammals       mammals      
## [456] mammals       mammals       mammals       mammals       mammals      
## [461] mammals       mammals       mammals       mammals       mammals      
## [466] mammals       mammals       mammals       mammals       mammals      
## [471] mammals       mammals       mammals       mammals       mammals      
## [476] mammals       mammals       mammals       mammals       mammals      
## [481] mammals       mammals       mammals       mammals       mammals      
## [486] mammals       mammals       mammals       mammals       mammals      
## [491] mammals       lizards       snakes        snakes        snakes       
## [496] snakes        snakes        snakes        snakes        snakes       
## [501] snakes        snakes        snakes        snakes        snakes       
## [506] snakes        snakes        snakes        snakes        snakes       
## [511] snakes        snakes        snakes        snakes        snakes       
## [516] snakes        snakes        lizards       lizards       lizards      
## [521] lizards       lizards       lizards       lizards       lizards      
## [526] lizards       snakes        lizards       snakes        snakes       
## [531] snakes        snakes        snakes        snakes        snakes       
## [536] snakes        snakes        snakes        snakes        snakes       
## [541] snakes        snakes        snakes        turtles       turtles      
## [546] turtles       turtles       turtles       turtles       turtles      
## [551] turtles       turtles       turtles       turtles       turtles      
## [556] turtles       tortoises     tortoises     tortoises     tortoises    
## [561] tortoises     tortoises     tortoises     tortoises     tortoises    
## [566] tortoises     tortoises     tortoises     turtles      
## 9 Levels: birds lake fishes lizards mammals marine fishes ... turtles
```

```r
homerange$order<-as.factor(homerange$order)
homerange$order
```

```
##   [1] anguilliformes        cypriniformes         cypriniformes        
##   [4] cypriniformes         cypriniformes         esociformes          
##   [7] gadiformes            gadiformes            perciformes          
##  [10] perciformes           perciformes           perciformes          
##  [13] perciformes           perciformes           perciformes          
##  [16] perciformes           perciformes           perciformes          
##  [19] perciformes           perciformes           perciformes          
##  [22] perciformes           perciformes           perciformes          
##  [25] perciformes           perciformes           perciformes          
##  [28] perciformes           perciformes           perciformes          
##  [31] perciformes           perciformes           perciformes          
##  [34] perciformes           perciformes           perciformes          
##  [37] perciformes           perciformes           perciformes          
##  [40] perciformes           perciformes           perciformes          
##  [43] perciformes           perciformes           perciformes          
##  [46] perciformes           perciformes           perciformes          
##  [49] perciformes           perciformes           perciformes          
##  [52] perciformes           perciformes           perciformes          
##  [55] perciformes           perciformes           perciformes          
##  [58] perciformes           perciformes           perciformes          
##  [61] perciformes           perciformes           perciformes          
##  [64] perciformes           perciformes           perciformes          
##  [67] perciformes           perciformes           perciformes          
##  [70] perciformes           perciformes           perciformes          
##  [73] perciformes           perciformes           perciformes          
##  [76] perciformes           perciformes           perciformes          
##  [79] perciformes           perciformes           perciformes          
##  [82] perciformes           perciformes           perciformes          
##  [85] perciformes           perciformes           perciformes          
##  [88] perciformes           perciformes           perciformes          
##  [91] perciformes           perciformes           perciformes          
##  [94] perciformes           perciformes           perciformes          
##  [97] salmoniformes         salmoniformes         salmoniformes        
## [100] salmoniformes         salmoniformes         scorpaeniformes      
## [103] scorpaeniformes       scorpaeniformes       scorpaeniformes      
## [106] scorpaeniformes       scorpaeniformes       scorpaeniformes      
## [109] scorpaeniformes       siluriformes          syngnathiformes      
## [112] syngnathiformes       tetraodontiformes\xa0 accipitriformes      
## [115] accipitriformes       accipitriformes       accipitriformes      
## [118] accipitriformes       accipitriformes       anseriformes         
## [121] apterygiformes        caprimulgiformes      charadriiformes      
## [124] columbidormes         columbiformes         columbiformes        
## [127] coraciiformes         coraciiformes         cuculiformes         
## [130] cuculiformes          cuculiformes          cuculiformes         
## [133] falconiformes         falconiformes         falconiformes        
## [136] falconiformes         falconiformes         falconiformes        
## [139] falconiformes         falconiformes         falconiformes        
## [142] falconiformes         falconiformes         falconiformes        
## [145] falconiformes         falconiformes         falconiformes        
## [148] falconiformes         falconiformes         galliformes          
## [151] galliformes           galliformes           galliformes          
## [154] galliformes           galliformes           galliformes          
## [157] galliformes           gruiformes            gruiformes           
## [160] gruiformes            passeriformes         passeriformes        
## [163] passeriformes         passeriformes         passeriformes        
## [166] passeriformes         passeriformes         passeriformes        
## [169] passeriformes         passeriformes         passeriformes        
## [172] passeriformes         passeriformes         passeriformes        
## [175] passeriformes         passeriformes         passeriformes        
## [178] passeriformes         passeriformes         passeriformes        
## [181] passeriformes         passeriformes         passeriformes        
## [184] passeriformes         passeriformes         passeriformes        
## [187] passeriformes         passeriformes         passeriformes        
## [190] passeriformes         passeriformes         passeriformes        
## [193] passeriformes         passeriformes         passeriformes        
## [196] passeriformes         passeriformes         passeriformes        
## [199] passeriformes         passeriformes         passeriformes        
## [202] passeriformes         passeriformes         passeriformes        
## [205] passeriformes         passeriformes         passeriformes        
## [208] passeriformes         passeriformes         passeriformes        
## [211] passeriformes         passeriformes         passeriformes        
## [214] passeriformes         passeriformes         passeriformes        
## [217] passeriformes         passeriformes         passeriformes        
## [220] passeriformes         passeriformes         passeriformes        
## [223] passeriformes         passeriformes         passeriformes        
## [226] passeriformes         passeriformes         passeriformes        
## [229] passeriformes         passeriformes         pelecaniformes       
## [232] pelecaniformes        piciformes            piciformes           
## [235] piciformes            piciformes            piciformes           
## [238] piciformes            piciformes            psittaciformes       
## [241] rheiformes            rheiformes            strigiformes         
## [244] strigiformes          strigiformes          strigiformes         
## [247] strigiformes          strigiformes          strigiformes         
## [250] strigiformes          strigiformes          struthioniformes     
## [253] tinamiformes          afrosoricida          afrosoricida         
## [256] artiodactyla          artiodactyla          artiodactyla         
## [259] artiodactyla          artiodactyla          artiodactyla         
## [262] artiodactyla          artiodactyla          artiodactyla         
## [265] artiodactyla          artiodactyla          artiodactyla         
## [268] artiodactyla          artiodactyla          artiodactyla         
## [271] artiodactyla          artiodactyla          artiodactyla         
## [274] artiodactyla          artiodactyla          artiodactyla         
## [277] artiodactyla          artiodactyla          artiodactyla         
## [280] artiodactyla          artiodactyla          artiodactyla         
## [283] artiodactyla          artiodactyla          artiodactyla         
## [286] artiodactyla          artiodactyla          artiodactyla         
## [289] artiodactyla          artiodactyla          artiodactyla         
## [292] artiodactyla          artiodactyla          artiodactyla         
## [295] carnivora             carnivora             carnivora            
## [298] carnivora             carnivora             carnivora            
## [301] carnivora             carnivora             carnivora            
## [304] carnivora             carnivora             carnivora            
## [307] carnivora             carnivora             carnivora            
## [310] carnivora             carnivora             carnivora            
## [313] carnivora             carnivora             carnivora            
## [316] carnivora             carnivora             carnivora            
## [319] carnivora             carnivora             carnivora            
## [322] carnivora             carnivora             carnivora            
## [325] carnivora             carnivora             carnivora            
## [328] carnivora             carnivora             carnivora            
## [331] carnivora             carnivora             carnivora            
## [334] carnivora             carnivora             carnivora            
## [337] carnivora             carnivora             carnivora            
## [340] carnivora             carnivora             carnivora            
## [343] carnivora             carnivora             carnivora            
## [346] carnivora             carnivora             carnivora            
## [349] carnivora             carnivora             dasyuromorpha        
## [352] dasyuromorpha         dasyuromorpha         dasyuromorpia        
## [355] didelphimorphia       didelphimorphia       diprodontia          
## [358] diprodontia           diprodontia           diprodontia          
## [361] diprodontia           diprodontia           diprodontia          
## [364] diprodontia           diprodontia           diprodontia          
## [367] diprodontia           diprodontia           diprotodontia        
## [370] diprotodontia         diprotodontia         diprotodontia        
## [373] diprotodontia         diprotodontia         diprotodontia        
## [376] erinaceomorpha        erinaceomorpha        lagomorpha           
## [379] lagomorpha            lagomorpha            lagomorpha           
## [382] lagomorpha            lagomorpha            lagomorpha           
## [385] lagomorpha            lagomorpha            lagomorpha           
## [388] lagomorpha            lagomorpha            lagomorpha           
## [391] lagomorpha            macroscelidea         macroscelidea        
## [394] macroscelidea         monotrematae          peramelemorphia      
## [397] peramelemorphia       perissodactyla        perissodactyla       
## [400] perissodactyla        pilosa                proboscidea          
## [403] proboscidea           roden                 rodentia             
## [406] rodentia              rodentia              rodentia             
## [409] rodentia              rodentia              rodentia             
## [412] rodentia              rodentia              rodentia             
## [415] rodentia              rodentia              rodentia             
## [418] rodentia              rodentia              rodentia             
## [421] rodentia              rodentia              rodentia             
## [424] rodentia              rodentia              rodentia             
## [427] rodentia              rodentia              rodentia             
## [430] rodentia              rodentia              rodentia             
## [433] rodentia              rodentia              rodentia             
## [436] rodentia              rodentia              rodentia             
## [439] rodentia              rodentia              rodentia             
## [442] rodentia              rodentia              rodentia             
## [445] rodentia              rodentia              rodentia             
## [448] rodentia              rodentia              rodentia             
## [451] rodentia              rodentia              rodentia             
## [454] rodentia              rodentia              rodentia             
## [457] rodentia              rodentia              rodentia             
## [460] rodentia              rodentia              rodentia             
## [463] rodentia              rodentia              rodentia             
## [466] rodentia              rodentia              rodentia             
## [469] rodentia              rodentia              rodentia             
## [472] rodentia              rodentia              rodentia             
## [475] rodentia              rodentia              rodentia             
## [478] rodentia              rodentia              rodentia             
## [481] rodentia              soricomorpha          soricomorpha         
## [484] soricomorpha          soricomorpha          soricomorpha         
## [487] soricomorpha          soricomorpha          soricomorpha         
## [490] soricomorpha          soricomorpha          squamata             
## [493] squamata              squamata              squamata             
## [496] squamata              squamata              squamata             
## [499] squamata              squamata              squamata             
## [502] squamata              squamata              squamata             
## [505] squamata              squamata              squamata             
## [508] squamata              squamata              squamata             
## [511] squamata              squamata              squamata             
## [514] squamata              squamata              squamata             
## [517] squamata              squamata              squamata             
## [520] squamata              squamata              squamata             
## [523] squamata              squamata              squamata             
## [526] squamata              squamata              squamata             
## [529] squamata              squamata              squamata             
## [532] squamata              squamata              squamata             
## [535] squamata              squamata              squamata             
## [538] squamata              squamata              squamata             
## [541] squamata              squamata              squamata             
## [544] testudines            testudines            testudines           
## [547] testudines            testudines            testudines           
## [550] testudines            testudines            testudines           
## [553] testudines            testudines            testudines           
## [556] testudines            testudines            testudines           
## [559] testudines            testudines            testudines           
## [562] testudines            testudines            testudines           
## [565] testudines            testudines            testudines           
## [568] testudines            testudines           
## 51 Levels: accipitriformes afrosoricida anguilliformes ... tetraodontiformes\xa0
```


**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**  

```r
taxa<- select(homerange, "taxon", "common.name", "class","order","family","genus","species")
```

**5. The variable `taxon` identifies the large, common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**  

```r
table(homerange$taxon)
```

```
## 
##         birds   lake fishes       lizards       mammals marine fishes 
##           140             9            11           238            90 
##  river fishes        snakes     tortoises       turtles 
##            14            41            12            14
```

**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.**  

```r
table(homerange$trophic.guild)
```

```
## 
## carnivore herbivore 
##       342       227
```

**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  

```r
carnivore<-filter(homerange, trophic.guild=="carnivore")
```

```r
herbivore<-filter(homerange, trophic.guild=="herbivores")
```

```r
anyNA.data.frame(herbivore)
```

```
## [1] FALSE
```


**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  

```r
anyNA.data.frame(homerange)
```

```
## [1] TRUE
```

```r
mean(homerange$mean.hra.m2)
```

```
## [1] 21456509
```

```r
variable.names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```

**9. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer? What is its common name?**  

```r
deer<- filter(homerange, family=="deer", species=="deer", genus=="deer",log10.mass=="deer")
```

**10. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!** **Snake is found in taxon column**    

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
