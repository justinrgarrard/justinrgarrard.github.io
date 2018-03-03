---
layout: category
title: Data Science Primer
category: DataSciencePrimer
---

Data Science, speaking broadly, is the practice of turning data into useful information. It's the process of distilling actionable insights from mind-bogglingly large piles of observations, such as predicting cancer rates based on the medical histories of 100,000 people. This reference page outlines my understanding of data science and the tools commonly associated with it.

### [ETL](/category/ETLPrimer.html) (Extract-Transform-Load)

A prerequisite to doing any kind of data science is having clean, useful data to work with. ETL is about organizing data sources into a cohesive shape. 

### Exploratory Analysis

Every dataset has a "feel" to it based on its size, quality, and content. Exploratory Analysis assesses datasets in quantitative and qualitative terms. It finds relationships between variables, identifies potential problem areas, and offers potential uses.

### Predictive Modeling

The bread-and-butter of data science. A predictive model is a complex machine that's designed to answer a question. 

* **Classifiers**: A model that predicts what category something falls in. The Toxic Comment Classifier I built for a Kaggle competition is an example of this. The question being asked is, "Given this comment's text, is it toxic, obscene, insulting, threatening, and/or identity hate?" Classifiers produce discrete outputs (i.e. yes or no).

* **Regressors**: A model that predicts a value based on its inputs. The Housing Price Regressor I build on Kaggle is an example of this. The question being asked is "Given information like the size of a house and the year it was built, how much should the house be sold for?" Regressors produce continuous output (i.e. $0 to $500,000).

### Machine Learning

Predictive models are generally built using machine learning algorithms.

* **Features**: A feature is a specific quality that's used to train a machine learning algorithm. It can be something like, "size of a house in square feet" or "color of the house". Feature engineering is one of the most difficult and creative aspects of data science.

* **Labels**: The agreed upon "right answer" for a piece of data. If the question is "How much should this house sell for?" the label might be "$100,000".