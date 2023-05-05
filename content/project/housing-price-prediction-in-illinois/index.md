---
title: Housing Price Prediction in Illinois
date: 2021-12-01T04:00:48.563Z
summary: >-
  This project involves working with a dataset from the Cook County Assessor's
  Office in Illinois, which contains over 500,000 records describing houses sold
  in the area in recent years. The dataset is split into training and test
  sets. 


  In Part 1, Exploratory Data Analysis (EDA) ais performed. In Part 2, the focus is on advanced prediction with machine learning. The criterion for evaluation is L2 loss, and the baseline model is ridge regression.
draft: false
featured: false
tags:
  - Data Science
links:
  - url: https://github.com/frankling2020/UMSI-Projects/blob/main/ece4710j/Project_part1.ipynb
    name: Part 1
    icon_pack: fas
    icon: link
  - name: Part 2
    url: https://github.com/frankling2020/UMSI-Projects/blob/main/ece4710j/Project_part2.ipynb
    icon_pack: fas
    icon: link
image:
  filename: featured.jpg
  focal_point: Smart
  preview_only: false
---
## Dataset

The dataset comes from the Cook County Assessor’s Office (CCAO) in Illinois, a government institution that determines property taxes across most of Chicago’s metropolitan area and its nearby suburbs. In the United States, all property owners are required to pay property taxes, which are then used to fund public services including education, road maintenance, and sanitation. These property tax assessments are based on property values estimated using statistical models that consider multiple factors, such as real estate value and construction cost.

The CCAO dataset consists of over 500 thousand records describing houses sold in Cook County in recent years (new records are still coming in every week!). The data set we will be working with has 61 features in total. An explanation of each variable can be found in the included `codebook.txt` file. Some of the columns have been filtered out to ensure this assignment doesn’t become overly long when dealing with data cleaning and formatting.

The data are split into training and test sets with 204792 and 68264 observations, respectively.



## [](https://frankling2020.github.io/2021/12/01/housing-price/#Part-1-Explortary-Data-Analysis-EDA "Part 1: Explortary Data Analysis (EDA)")Part 1: Explortary Data Analysis (EDA)

* Abnormal Values: remove outliers, fill with default values
* Feature Engineering: log transformation, one-hot encoding, keyword extraction
* Modeling: linear regression
* Notice: implement with pipeline and visualization



## [](https://frankling2020.github.io/2021/12/01/housing-price/#Part-2-Advanced-Prediction-with-Machine-Learning "Part 2: Advanced Prediction with Machine Learning")Part 2: Advanced Prediction with Machine Learning

* Criterion: L2 loss
* Baseline: ridge regression
* Main Model: xgboost + random forest
* Ablation study: xgboost, xgboost + ridge regression