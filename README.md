# ANA-515-WEEK-4

---
title: "Hw2 for ANA 515"
author: "Pin-Chieh Huang"
date: "2024-06-10"
output:
 
  word_document: word_document
  html_document: html_document
---

Describe Data:

The database I am using is from United Airlines how much they spent on each department every year based on wide and narrow body aircraft. The data is stored as an Excel file. As we know most of data is about the money and number,so the data type is binary. In order to have perfect number, we need to  remove n/a row and convert the scientific number. In the report, we will see only summary and clean data from our file. 

```{r section 2~3, include = FALSE}
#install.packages("tidyverse")
#install.packages("readxl")
#install.packages("dplyr")
library(tidyverse)
library(readxl)
library(dplyr)
library(knitr)

united <- read_xls("United Airlines Aircraft Operating Statistics- Actuals.xls")
united
united1 <-united[-1,-1] # remove the first row and first column because of n/a value
colnames(united1) <- united1[1,] # to see the first row which is years
united2 <- united1[-1,] # remove the first now because we want to bring the first row (year) as head 
united2 <- na.omit(united2) #remove the rows with n/a

```



We have data about `r nrow(united2)` factories such as how much they spent on pilot, HR, aircrafts  and so on . The distribution of this is shown below: The data is about 2014 and 2015 how much united airlines spent on the each department. the `1column(united2)`is the data of 2014 and the `2column(united2)`is the data of 2015


```{r section4, include=FALSE}
united2 <- subset(united1,select = c("year","2014","2015")) #subset 2014 and 2015 columns 
options(scipen = 999) #  to turn off scientific notation

united2 <- na.omit(united2) #remove the rows with n/a
print(kable(united2)) # the total costs in 2014 and 2015 from united differetn departments 
united2
```
```{r section5, include=FALSE}
united3 <- subset(united1,select = c("year","2013","2014","2015")) #subset 2013, 2014 and 2015 columns 
options(scipen = 999) #  to turn off scientific notation

united3 <- na.omit(united3) #remove the rows with n/a
print(kable(united3))
united3
```

```{r  comment=NA}
united3 <- round(united3[,-1], digits=2) # to round the number to digital 2.  excludes column 1 because it is name. 
summary(united3)
```
