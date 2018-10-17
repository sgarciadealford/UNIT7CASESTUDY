---
title: "Unit 7"
author: "Solange GarciadeAlford"
date: "October 10, 2018"
output: 
  html_document:
    keep_md: true 
---



## Introduction

```r
brdata <- read.csv("C:/Users/solan/documents/breweries.csv")
bedata <- read.csv("C:/Users/solan/documents/beers.csv")
```
## Questions of Interest

```r
## Q1 - How many brewries are present in each state?

str(brdata)
```

```
## 'data.frame':	558 obs. of  4 variables:
##  $ Brew_ID: int  1 2 3 4 5 6 7 8 9 10 ...
##  $ Name   : Factor w/ 551 levels "10 Barrel Brewing Company",..: 355 12 266 319 201 136 227 477 59 491 ...
##  $ City   : Factor w/ 384 levels "Abingdon","Abita Springs",..: 228 200 122 299 300 62 91 48 152 136 ...
##  $ State  : Factor w/ 51 levels " AK"," AL"," AR",..: 24 18 20 5 5 41 6 23 23 23 ...
```

```r
str(bedata)
```

```
## 'data.frame':	2410 obs. of  7 variables:
##  $ Name      : Factor w/ 2305 levels "#001 Golden Amber Lager",..: 1638 577 1705 1842 1819 268 1160 758 1093 486 ...
##  $ Beer_ID   : int  1436 2265 2264 2263 2262 2261 2260 2259 2258 2131 ...
##  $ ABV       : num  0.05 0.066 0.071 0.09 0.075 0.077 0.045 0.065 0.055 0.086 ...
##  $ IBU       : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ Brewery_id: int  409 178 178 178 178 178 178 178 178 178 ...
##  $ Style     : Factor w/ 100 levels "","Abbey Single Ale",..: 19 18 16 12 16 80 18 22 18 12 ...
##  $ Ounces    : num  12 12 12 12 12 12 12 12 12 12 ...
```

```r
options(repos="https://cran.rstudio.com" )

install.packages("tidyverse")
```

```
## Installing package into 'C:/Users/solan/Documents/R/win-library/3.5'
## (as 'lib' is unspecified)
```

```
## package 'tidyverse' successfully unpacked and MD5 sums checked
## 
## The downloaded binary packages are in
## 	C:\Users\solan\AppData\Local\Temp\Rtmpy0MZl4\downloaded_packages
```

```r
library(plyr)

count(brdata, c("State"))
```

```
##    State freq
## 1     AK    7
## 2     AL    3
## 3     AR    2
## 4     AZ   11
## 5     CA   39
## 6     CO   47
## 7     CT    8
## 8     DC    1
## 9     DE    2
## 10    FL   15
## 11    GA    7
## 12    HI    4
## 13    IA    5
## 14    ID    5
## 15    IL   18
## 16    IN   22
## 17    KS    3
## 18    KY    4
## 19    LA    5
## 20    MA   23
## 21    MD    7
## 22    ME    9
## 23    MI   32
## 24    MN   12
## 25    MO    9
## 26    MS    2
## 27    MT    9
## 28    NC   19
## 29    ND    1
## 30    NE    5
## 31    NH    3
## 32    NJ    3
## 33    NM    4
## 34    NV    2
## 35    NY   16
## 36    OH   15
## 37    OK    6
## 38    OR   29
## 39    PA   25
## 40    RI    5
## 41    SC    4
## 42    SD    1
## 43    TN    3
## 44    TX   28
## 45    UT    4
## 46    VA   16
## 47    VT   10
## 48    WA   23
## 49    WI   20
## 50    WV    1
## 51    WY    4
```

```r
## Q2 - Merge beer data with the breweries data. Print the first 6 observations and the last six observations to check the merged file.

##chaning the name of the column in the satesize data frame for merging files
names(brdata)[1] <- "Brewery_id"
str(brdata)
```

```
## 'data.frame':	558 obs. of  4 variables:
##  $ Brewery_id: int  1 2 3 4 5 6 7 8 9 10 ...
##  $ Name      : Factor w/ 551 levels "10 Barrel Brewing Company",..: 355 12 266 319 201 136 227 477 59 491 ...
##  $ City      : Factor w/ 384 levels "Abingdon","Abita Springs",..: 228 200 122 299 300 62 91 48 152 136 ...
##  $ State     : Factor w/ 51 levels " AK"," AL"," AR",..: 24 18 20 5 5 41 6 23 23 23 ...
```

```r
##merging files
mdata <- merge(brdata, bedata , by = "Brewery_id")
str(mdata)
```

```
## 'data.frame':	2410 obs. of  10 variables:
##  $ Brewery_id: int  1 1 1 1 1 1 2 2 2 2 ...
##  $ Name.x    : Factor w/ 551 levels "10 Barrel Brewing Company",..: 355 355 355 355 355 355 12 12 12 12 ...
##  $ City      : Factor w/ 384 levels "Abingdon","Abita Springs",..: 228 228 228 228 228 228 200 200 200 200 ...
##  $ State     : Factor w/ 51 levels " AK"," AL"," AR",..: 24 24 24 24 24 24 18 18 18 18 ...
##  $ Name.y    : Factor w/ 2305 levels "#001 Golden Amber Lager",..: 1640 1926 1525 802 1258 2185 71 458 1218 43 ...
##  $ Beer_ID   : int  2689 2688 2687 2692 2691 2690 2683 2686 2685 2684 ...
##  $ ABV       : num  0.06 0.06 0.056 0.045 0.049 0.048 0.042 0.08 0.125 0.077 ...
##  $ IBU       : int  38 25 47 50 26 19 42 68 80 25 ...
##  $ Style     : Factor w/ 100 levels "","Abbey Single Ale",..: 83 22 57 16 77 48 18 12 46 77 ...
##  $ Ounces    : num  16 16 16 16 16 16 16 16 16 16 ...
```

```r
head(mdata)
```

```
##   Brewery_id             Name.x        City State        Name.y Beer_ID
## 1          1 NorthGate Brewing  Minneapolis    MN       Pumpion    2689
## 2          1 NorthGate Brewing  Minneapolis    MN    Stronghold    2688
## 3          1 NorthGate Brewing  Minneapolis    MN   Parapet ESB    2687
## 4          1 NorthGate Brewing  Minneapolis    MN  Get Together    2692
## 5          1 NorthGate Brewing  Minneapolis    MN Maggie's Leap    2691
## 6          1 NorthGate Brewing  Minneapolis    MN    Wall's End    2690
##     ABV IBU                               Style Ounces
## 1 0.060  38                         Pumpkin Ale     16
## 2 0.060  25                     American Porter     16
## 3 0.056  47 Extra Special / Strong Bitter (ESB)     16
## 4 0.045  50                        American IPA     16
## 5 0.049  26                  Milk / Sweet Stout     16
## 6 0.048  19                   English Brown Ale     16
```

```r
tail(mdata)
```

```
##      Brewery_id                        Name.x          City State
## 2405        556         Ukiah Brewing Company         Ukiah    CA
## 2406        557       Butternuts Beer and Ale Garrattsville    NY
## 2407        557       Butternuts Beer and Ale Garrattsville    NY
## 2408        557       Butternuts Beer and Ale Garrattsville    NY
## 2409        557       Butternuts Beer and Ale Garrattsville    NY
## 2410        558 Sleeping Lady Brewing Company     Anchorage    AK
##                         Name.y Beer_ID   ABV IBU                   Style
## 2405             Pilsner Ukiah      98 0.055  NA         German Pilsener
## 2406         Porkslap Pale Ale      49 0.043  NA American Pale Ale (APA)
## 2407           Snapperhead IPA      51 0.068  NA            American IPA
## 2408         Moo Thunder Stout      50 0.049  NA      Milk / Sweet Stout
## 2409  Heinnieweisse Weissebier      52 0.049  NA              Hefeweizen
## 2410 Urban Wilderness Pale Ale      30 0.049  NA        English Pale Ale
##      Ounces
## 2405     12
## 2406     12
## 2407     12
## 2408     12
## 2409     12
## 2410     12
```

```r
##Q3 - Report the number of NA's in each column.
count(mdata$Brewery_id == "NA")
```

```
##       x freq
## 1 FALSE 2410
```

```r
count(mdata$Name.x == "NA")
```

```
##       x freq
## 1 FALSE 2410
```

```r
count(mdata$City == "NA")
```

```
##       x freq
## 1 FALSE 2410
```

```r
count(mdata$State == "NA")
```

```
##       x freq
## 1 FALSE 2410
```

```r
count(mdata$Name.y == "NA")
```

```
##       x freq
## 1 FALSE 2410
```

```r
count(mdata$Beer_ID == "NA")
```

```
##       x freq
## 1 FALSE 2410
```

```r
count(mdata$ABV == "NA")
```

```
##       x freq
## 1 FALSE 2348
## 2    NA   62
```

```r
count(mdata$IBU == "NA")
```

```
##       x freq
## 1 FALSE 1405
## 2    NA 1005
```

```r
count(mdata$Style == "NA")
```

```
##       x freq
## 1 FALSE 2410
```

```r
count(mdata$Ounces == "NA")
```

```
##       x freq
## 1 FALSE 2410
```

```r
##Q4 - Compute the median alcohol content and international bitterness unit for each state. 

install.packages("stats")
```

```
## Installing package into 'C:/Users/solan/Documents/R/win-library/3.5'
## (as 'lib' is unspecified)
```

```
## Warning: package 'stats' is not available (for R version 3.5.1)
```

```
## Warning: package 'stats' is a base package, and should not be updated
```

```r
library(stats)

median.ABV <- data.frame(aggregate(ABV ~ State, data = mdata, median))
median.IBU <- data.frame(aggregate(IBU ~ State, data = mdata, median))
median.ABV
```

```
##    State    ABV
## 1     AK 0.0560
## 2     AL 0.0600
## 3     AR 0.0520
## 4     AZ 0.0550
## 5     CA 0.0580
## 6     CO 0.0605
## 7     CT 0.0600
## 8     DC 0.0625
## 9     DE 0.0550
## 10    FL 0.0570
## 11    GA 0.0550
## 12    HI 0.0540
## 13    IA 0.0555
## 14    ID 0.0565
## 15    IL 0.0580
## 16    IN 0.0580
## 17    KS 0.0500
## 18    KY 0.0625
## 19    LA 0.0520
## 20    MA 0.0540
## 21    MD 0.0580
## 22    ME 0.0510
## 23    MI 0.0620
## 24    MN 0.0560
## 25    MO 0.0520
## 26    MS 0.0580
## 27    MT 0.0550
## 28    NC 0.0570
## 29    ND 0.0500
## 30    NE 0.0560
## 31    NH 0.0550
## 32    NJ 0.0460
## 33    NM 0.0620
## 34    NV 0.0600
## 35    NY 0.0550
## 36    OH 0.0580
## 37    OK 0.0600
## 38    OR 0.0560
## 39    PA 0.0570
## 40    RI 0.0550
## 41    SC 0.0550
## 42    SD 0.0600
## 43    TN 0.0570
## 44    TX 0.0550
## 45    UT 0.0400
## 46    VA 0.0565
## 47    VT 0.0550
## 48    WA 0.0555
## 49    WI 0.0520
## 50    WV 0.0620
## 51    WY 0.0500
```

```r
median.IBU
```

```
##    State  IBU
## 1     AK 46.0
## 2     AL 43.0
## 3     AR 39.0
## 4     AZ 20.5
## 5     CA 42.0
## 6     CO 40.0
## 7     CT 29.0
## 8     DC 47.5
## 9     DE 52.0
## 10    FL 55.0
## 11    GA 55.0
## 12    HI 22.5
## 13    IA 26.0
## 14    ID 39.0
## 15    IL 30.0
## 16    IN 33.0
## 17    KS 20.0
## 18    KY 31.5
## 19    LA 31.5
## 20    MA 35.0
## 21    MD 29.0
## 22    ME 61.0
## 23    MI 35.0
## 24    MN 44.5
## 25    MO 24.0
## 26    MS 45.0
## 27    MT 40.0
## 28    NC 33.5
## 29    ND 32.0
## 30    NE 35.0
## 31    NH 48.5
## 32    NJ 34.5
## 33    NM 51.0
## 34    NV 41.0
## 35    NY 47.0
## 36    OH 40.0
## 37    OK 35.0
## 38    OR 40.0
## 39    PA 30.0
## 40    RI 24.0
## 41    SC 30.0
## 42    TN 37.0
## 43    TX 33.0
## 44    UT 34.0
## 45    VA 42.0
## 46    VT 30.0
## 47    WA 38.0
## 48    WI 19.0
## 49    WV 57.5
## 50    WY 21.0
```

```r
##     Plot a bar chart to compare.
install.packages("ggplot2")
```

```
## Installing package into 'C:/Users/solan/Documents/R/win-library/3.5'
## (as 'lib' is unspecified)
```

```
## package 'ggplot2' successfully unpacked and MD5 sums checked
## 
## The downloaded binary packages are in
## 	C:\Users\solan\AppData\Local\Temp\Rtmpy0MZl4\downloaded_packages
```

```r
library(ggplot2)

medians.st <- merge(median.ABV, median.IBU , by = "State")
str(medians.st)
```

```
## 'data.frame':	50 obs. of  3 variables:
##  $ State: Factor w/ 51 levels " AK"," AL"," AR",..: 1 2 3 4 5 6 7 8 9 10 ...
##  $ ABV  : num  0.056 0.06 0.052 0.055 0.058 0.0605 0.06 0.0625 0.055 0.057 ...
##  $ IBU  : num  46 43 39 20.5 42 40 29 47.5 52 55 ...
```

```r
ggplot(data=medians.st, aes(x=State, y=IBU )) +   
geom_bar(aes(fill = IBU), position = "dodge", stat="identity") +
labs(title = "         Median International Bitterness Unit by State") +
labs(caption = "(Based on data from study case)") +
theme(axis.text.x = element_text(color="#993333", 
                           size=7, angle=90),
        axis.text.y = element_text(face="bold", color="#993333", 
                           size=10, angle=90))
```

![](UNIT7CASESTUDY_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```r
ggplot(data=medians.st, aes(x=State, y=ABV )) +   
geom_bar(aes(fill = ABV), position = "dodge", stat="identity") +
labs(title = "         Median Alcohol Content by State") +
labs(caption = "(Based on data from study case)") +
theme(axis.text.x = element_text(color="#993333", 
                           size=7, angle=90),
        axis.text.y = element_text(face="bold", color="#993333", 
                           size=10, angle=90))
```

![](UNIT7CASESTUDY_files/figure-html/unnamed-chunk-2-2.png)<!-- -->

```r
## Q5 -- Which state has the maximum alcoholic (ABV) beer? Which state has the most bitter (IBU) beer?

a <- max(medians.st$ABV)
b <- max(medians.st$IBU)
a
```

```
## [1] 0.0625
```

```r
b
```

```
## [1] 61
```

```r
c.df <- data.frame(which(medians.st$ABV == a))
c.df
```

```
##   which.medians.st.ABV....a.
## 1                          8
## 2                         18
```

```r
c.df1 <- c.df[1,1]
c.df2 <- c.df[2,1]
c.df1
```

```
## [1] 8
```

```r
c.df2
```

```
## [1] 18
```

```r
st.medABV1 <- medians.st[8,]
st.medABV2 <- medians.st[18,]
st.medABV1
```

```
##   State    ABV  IBU
## 8    DC 0.0625 47.5
```

```r
st.medABV2
```

```
##    State    ABV  IBU
## 18    KY 0.0625 31.5
```

```r
## Kentucky and Washington, D.C, have the highest median maximum alcoholic (ABV) beers.

ci.df <- data.frame(which(medians.st$IBU == b))
ci.df
```

```
##   which.medians.st.IBU....b.
## 1                         22
```

```r
ci.df1 <- c.df[1,1]
ci.df1
```

```
## [1] 8
```

```r
st.medIBU <- medians.st[22,]
st.medIBU
```

```
##    State   ABV IBU
## 22    ME 0.051  61
```

```r
## Maine is the state with the highest median IBU beer


## Q6  - Summary statistics for the ABV variable.

summary(mdata$ABV)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
## 0.00100 0.05000 0.05600 0.05977 0.06700 0.12800      62
```

```r
## Q7 - There is an apparent relationship between the bitterness of the beer and its alcoholic content? 
## Draw a scatter plot.

## Graphing packages found at:
##http://www.sthda.com/english/wiki/ggplot2-scatterplot-easy-scatter-plot-using-ggplot2-and-r-statistical-software

install.packages("devtools")
```

```
## Installing package into 'C:/Users/solan/Documents/R/win-library/3.5'
## (as 'lib' is unspecified)
```

```
## package 'devtools' successfully unpacked and MD5 sums checked
## 
## The downloaded binary packages are in
## 	C:\Users\solan\AppData\Local\Temp\Rtmpy0MZl4\downloaded_packages
```

```r
library(devtools)
install_github("easyGgplot2", "kassambara")
```

```
## Warning: Username parameter is deprecated. Please use kassambara/
## easyGgplot2
```

```
## Skipping install of 'easyGgplot2' from a github remote, the SHA1 (cb017c1c) has not changed since last install.
##   Use `force = TRUE` to force installation
```

```r
library(easyGgplot2)


ggplot2.scatterplot(data=mdata, xName='ABV', yName='IBU', mapping=aes(size = qsec), addRegLine=TRUE, regLineColor="red", mainTitle='                                        AVB versus IBU', xtitle="Alcohol by Volume of Beer", ytitle="International Bitterness Units", shape=23, size=2, fill="navy")
```

```
## Warning: Removed 1005 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 1005 rows containing missing values (geom_point).
```

![](UNIT7CASESTUDY_files/figure-html/unnamed-chunk-2-3.png)<!-- -->

## Including Plots





Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
