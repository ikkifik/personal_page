---
layout: posts
title: "Kaggle: Intermediate Machine Learning"
date: 2025-07-26
category: Learning-notes
---
- Ordinal encoding -> a categorical variable approach which uses ordinal variables (ordering number) for reinterpreting categorical values into numbers (e.g. `"Never" (0) < "Rarely" (1) < "Most days" (2) < "Every day" (3).`)

- One-hot encoding -> adding new columns for each corresponding category and put the value 

`True` when the corresponding rows originally have value same with the new columns. It called nominal variables, unlike the ordinal encoding, one-hot encoding doesn't assume category order (i.e. without intrinsic ranking). However, this approach isn't suitable for large number of category values (i.e. kinda difficult if the values more than 15, imagine having 15 new columns each containing 0 or 1 value as category row representations).

- Categorical variables ≠ class (target) features

- Solving the missing value problem using imputer, there are several ways, by using: median and mean for specific numerical data; or the "most frequent" and constant for both numerical and strings (object) data.

- Using imputation is more preferable way instead of dropping columns (or probably rows, self-opinion) which can make the model losing the potential of important features.