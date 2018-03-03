---
layout: post
title: "Ames Housing Price Regressor"
categories:
  - Project
tags:
  - Python
  - regression
  - machine learning
  - numpy
  - pandas
---

## Overview

One of the practice competitions for Kaggle, using the Ames Housing Dataset. The Housing Price Regressor attempts to guess the price of a house using machine learning principles. 

## The Data

[Ames Housing Dataset](http://www.amstat.org/publications/jse/v19n3/decock.pdf): A fairly large data set with 79 variables relating to houses, including elements such as lot size, number of bathrooms, and year of construction. 

## The Highlights

* A customizable Python script that allows users to pick from AdaBoost, GradientBoost, XGB, and hybrid regressor options.

* Techniques for data formatting such as one-hot encoding for categorical values and logarithmic normalization.

* Handmade code for generating Root-Mean-Squared-Error (RMSE) and tuning regressor parameters (n estimators, learning rate).

## The Details

The full code can be found [here](https://github.com/justinrgarrard/KaggleHousePricer). Improvement is still needed to achieve an acceptable level of 'accuracy', but the foundations are in place.