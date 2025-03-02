---
layout: post
title: "RegEx Codethrough"
date: 2025-03-01
categories: [data, regex, analytics]
---
## Introduction

This code through will explore additional use cases of regular expressions
within R by using the Amazon Fine Food Reviews dataset from Kaggle.

You can find the direct link here: [Kaggle Dataset](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews/data)

For a brief description of this dataset - it contains reviews of fine foods
from Amazon. The dataset contains information on product/user information,
ratings, and reviews. 

## Learning Objectives

Our goal for this CodeThrough is to filter the reviews to answer a couple of 
business questions and also clean the datasets. 

```{r include = FALSE}

# SET GLOBAL KNITR OPTIONS

knitr::opts_chunk$set(echo = TRUE, 
                      message = FALSE, 
                      warning = FALSE, 
                      fig.width = 10, 
                      fig.height = 8)



# LOAD PACKAGES

library(tidyverse)
library(stringr)
library(readr)

```

*Step 1: Load Amazon Review Dataset*
```{r}
# As mentioned, please refer to the Kaggle link I provded above to download
# the dataset. It is quite a big file, so it may take some time!

# Define file path
dataset_path <- "/Users/kalanicook/Downloads/amazon_kaggle/Reviews.csv"

# Load the dataset in R
reviews <- read_csv(dataset_path)

# View the first few rows
head(reviews)
```
<br>

*Step 2: Filter Reviews with RegEx*

For our first scenario, we want to filter the reviews that mention key terms 
such as "Refund" or "Money". This could give us an idea of customer complaints.

<br>

```{r}
refund_reviews <- reviews %>%
  filter(str_detect(Text, "(?i)refund|money back|return"))

head(refund_reviews$Text, 5)
```
<br>

Logic:
By using str_detect(), the function works to search through our Reviews.csv
file and return reviews that match the requested pattern. 

(?i) - is used to make the search case insenstive. 

<br>

Following this, let's do the opposite and filter for reviews that are positive.

<br>

```{r}
positive_reviews <- reviews %>%
  filter(str_detect(Text, "(?i)awesome|love|amazing"))

head(positive_reviews$Text, 5)
```
