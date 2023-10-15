# Crime_Analysis
![image](./images/Crime.image.png)

## Introduction
This Dataset contains all of the recorded crime data in the city of Los Angeles between the years of 2020 to the Present Day(2023). The dataset contains everything from the time the crime was reported, the type of crime committed, as well as the longitude and latitude which the crime was committed. 

## Problem Statement
The analysis of crime data containing information on victims' gender presents an opportunity to gain insights into the demographics of crime victims. The primary objective is to investigate and understand patterns and disparities related to gender in reported crimes, potentially revealing areas for targeted intervention and policy development.

## Tools Used
- R programming

## Dataset
The dataset was downloaded from [here](https://www.kaggle.com/datasets/nathaniellybrand/los-angeles-crime-dataset-2020-present). The dataset was made available by SavorSauce.

## Analysis
Step 1: Install package tidyverse and load the library. Tidyverse package enables cleaning tools and creation of plots.
```  
install.packages("tidyverse")
library(tidyverse)
```
Step 2: Upload the dataset in R studio.
``` 
Crime_data <- read.csv("C:/Users/bastr/Downloads/Crime_Data.csv")
```
Step 3: Cleaning
```
str(Crime_data)
head(Crime_data)
Crime_data <- Crime_data %>%
  mutate_if(is.numeric, ~ifelse(is.na(.), 0, .))
```
Add age_group column
```
library(dplyr)
age_groups <- c("Under 18", "18-29", "30-39", "40-49", "50-59", "60 and over")
age_breaks <- c(0, 18, 30, 40, 50, 60, Inf)
Crime_data <- Crime_data %>%
  mutate(AgeGroup = cut(Vict.Age, breaks = age_breaks, labels = age_groups, include.lowest = TRUE))
head(Crime_data)
```
Step 4: Create plots
Victims by sex
```
library(ggplot2)
ggplot(Crime_data, aes(x = factor(Vict.Sex), fill = Vict.Sex)) +
  geom_bar() +
  labs(title = "Bar Chart of Vict.Sex",
       x = "Victime Sex",
       y = "DR_NO") +
  theme_minimal()
```
Victims by Age
```
ggplot(Crime_data, aes(x = Vict.Age)) +
    geom_histogram(binwidth = 5, fill = "lightblue", color = "black") +
    labs(title = "Histogram of Victim Ages",
         x = "Victim Age",
         y = "Frequency") +
    theme_minimal()
```

## Conclusion
Our analysis of the crime data reveals some significant patterns and insights regarding the victims of reported crimes. Firstly, it is evident that male individuals are the most frequently targeted victims across various crime categories. This suggests that males may face a higher risk of victimization compared to other gender identities in Los Angeles.

Additionally, when examining the age distribution of victims, an interesting trend emerges. The histogram of victim ages clearly illustrates that there is a lower occurrence of reported crimes for individuals in the age range of 80-120. This may indicate a lower death rate or a reduced likelihood of being involved in criminal incidents for individuals in this age group.

These findings have important implications for understanding the demographics of crime victims and can be used to inform crime prevention strategies and social support systems to better protect and assist vulnerable populations. It's important to note that further in-depth analysis and research may be required to explore the underlying causes and consequences of these patterns, but this initial insight can serve as a valuable starting point for such investigations.




