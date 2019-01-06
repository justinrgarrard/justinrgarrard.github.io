---
layout: post
title: "Goodreads Genre Classifier"
categories:
  - Project
tags:
  - Python
  - scikit-learn
  - NLP
---

## Overview

The [Goodreads Genre Classifier](https://github.com/justinrgarrard/GenreClassifier) is a Python program designed to predict a book's genre. It feeds curated data collected from the Goodreads API into a machine learning algorithm.

## Data Wrangling

Labelled data is pulled from a manually compiled list of users (goodreads_booklists.csv). Each entry follows the same pattern of [goodreads_list_name, user_id, genre_class].

```
fantasy,666892,1
```

This information is used to make an API call. Goodreads sends back an XML response that can be parsed for relevant features (isbn, title, author, etc.) and placed into an SQL database for later use.

The full process, then, looks something like this:

1. Manually create a list of Goodreads Lists for each genre.

2. Pull data using the Goodreads API (Requests library).

3. Parse the data (xmltodict library).

4. Scrub the data for SQL safety (bleach library).

5. Enter the data into a SQL database (sqlite3 library).

This project involved less data cleaning than others, but required more work upfront to curate.

## Functionality

Once the data is compiled, it can be used to train a classifier. There are two main components involved:

* The type of classifier (SVM, AdaBoost)
* The features used (Author, Title, Publication Year, etc.)

Presently, the program uses an SVM with the author's name and the book's title. The text processing is handled by two sub-classifiers, both Naive Bayes.


That being said, it's evident that the program could use work. I'm curious whether it would make a difference if I gave the classifier more information. For instance, if it was fed probability distributions for the author and title classifiers, or if I could get the title classifier to use bigrams.

## Reflections

This was a good practice project. It covered data acquisition (via API), organization (SQL), and application (Classifiers). I think that I need a little more training in machine learning before this can be made into something genuinely useful.
