---
title: "Exploring the BRFSS data"
output: 
  html_document: 
    fig_height: 4
    highlight: pygments
    theme: spacelab
---

## Setup

### Load packages

```{r load-packages, message = FALSE}
library(ggplot2)
library(dplyr)
```

### Load data

Make sure your data and R Markdown files are in the same directory. When loaded
your data file will be called `brfss2013`. Delete this note when before you submit 
your work. 

```{r load-data}
load("brfss2013.RData")
```



* * *

## Part 1: Data


* * *

## Part 2: Research questions

**Research question 1: Are sleep duration and general health of a person associated in any way? **

This question will delve into differentiation of sleep patterns by general health level and help us understand if there is any particular trend which is obvious.

**Research question 2: Is there any association of respondent's sex with him or her being diagnosed with a heart attack?**

The above question will help us understand if the proportion of people being diagnosed with a heart attack vary by gender.

**Research question 3: Does marital status has any association with sex of the respondent? **


* * *

## Part 3: Exploratory data analysis

Let us now look into analyzing the research questions. We will be analyzing data only for the interview year 2013 as we do not have enough observations for 2014.


**Research question 1: Are sleep duration and general health of a person associated in any way? **

```{r Q1}
# Subsetting foe interview year 2013
subset <- brfss2013[brfss2013$iyear == 2013,]

# Removing the observations where either of the two variables being studied are missing
subset1 <- subset[!is.na(subset$sleptim1) & !is.na(subset$genhlth),]

# Generating a box plot visualization
boxplot(sleptim1 ~ genhlth, data = subset1, xlab = "General Health Level", ylab = "# of hours slept")

# Creating a table for summary statistics
subset1 %>% group_by(genhlth) %>% summarise(mean_sleep = mean(sleptim1))

```

From the box plot above, we can clearly observe that the people with poor general health level have a lower average value of sleep time when compared to other categories.
When we look at the summary statistics, we see that as the general health level deteriorates, a declining trend in sleep time is observed. We should be not infer any kind of causality here as this is not an experimental study.


**Research question 2: Is there any association of respondent's sex with him or her being diagnosed with a heart attack?**

```{r Q2}
# Removing the observations where either of the two variables being studied are missing
subset1 <- subset[!is.na(subset$cvdinfr4) & !is.na(subset$sex),]

# Creating a table for summary statistics
HA_by_sex <- table(subset1$sex,subset1$cvdinfr4)
HA_by_sex[1,] <- HA_by_sex[1,]/nrow(subset1[subset1$sex=="Male",]) 
HA_by_sex[2,] <- HA_by_sex[2,]/nrow(subset1[subset1$sex=="Female",])
HA_by_sex

# Creating a bar plot to visualize the results
barplot(HA_by_sex, 
        main = "Proportion of Heart Attack diagnosis cases by gender",
        xlab = "Diagnosis result", col = c("blue", "green"), 
        legend.text = rownames(HA_by_sex), beside = TRUE, 
        args.legend =  list(x= "center"))

```

We can see that a larger proportion of males (8.03%) have been diagnosed with heart attack as compared to the proportion of females (4.58%). There is also some difference observed based on gender in cases where the diagnosis was negative.


**Research question 3: Does marital status has any association with sex of the respondent? **

```{r Q3}
# Removing the observations where either of the two variables being studied are missing
subset1 <- subset[!is.na(subset$marital) & !is.na(subset$sex),]

# Creating a table for summary statistics
MS_by_sex <- table(subset1$sex,subset1$marital)
MS_by_sex[1,] <- MS_by_sex[1,]/nrow(subset1[subset1$sex=="Male",]) 
MS_by_sex[2,] <- MS_by_sex[2,]/nrow(subset1[subset1$sex=="Female",])
MS_by_sex

# Creating a bar plot to visualize the results
 barplot(MS_by_sex, 
        main = "Proportion of males and females by marital status",
        xlab = "Marital Status", col = c("blue", "green"), 
        legend.text = rownames(MS_by_sex), beside = TRUE, 
        args.legend =  list(x= "center"), cex.names = 0.7)

```

By looking at the bar plot, we can observe the variation of people having different marital status distributed based on gender.

For example, only 6.4% of males are widowed compared to 18.4% of females. the difference between proportion of single (never married) males and females is greater than 5%.
