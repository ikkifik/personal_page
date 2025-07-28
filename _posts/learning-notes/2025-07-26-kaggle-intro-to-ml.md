---
layout: posts
title: "Kaggle: Intro to Machine Learning"
date: 2025-07-26
category: Learning-notes
---

- Steps of capturing patterns from data called **fitting** or **training**. The data used to **fit**/train the model called the training data.

- Then after the model has been fit, we apply it to new data to **predict** 

- In decision tree, the last bottom point where the prediction placed called a **leaf**

- Mean Absolute Error(MAE) counts from 0 to infinity, it means this evaluation metrics cannot be used as a standalone evaluation metrics without context. It needs domain knowledge or business context for the score have a meaning. The stakeholders must know the expected value scale based on the business they have.

- MAE more suitable used for comparing different machine learning models on the same dataset, to find the better model by looking at the lowest score between models.

- MAE can also be used for comparing values of training data and testing/validation data during evaluation, to estimate the underfitting and overfitting, visually using linear graph.