---
layout: post
title: "U.S. Education Data: Unification Project"
categories:
  - Project
tags:
  - Python
  - Pandas
---

## Overview

I spent some time earlier in the year [working with datasets](https://justinrgarrard.github.io/project/2018/03/03/US_Education_Data.html) related to U.S. education. I found that the data wasn't always easy to work with. Records were separated by year in CSV files, with the headers changing as surveys evolved.

This project is my attempt to organize education data into a more convenient shape. I take raw CSV files across multiple years and topics and combine them into aggregates. The result is a single spreadsheet that's much simpler to work with. 


## Contents

[Data Pipeline Repository](https://github.com/justinrgarrard/USEduData)

> The code that processes input data from the U.S. Census Bureau and National Center for Education Statistics. This is where the cleaning and aggregating takes place.   


[Kaggle Repository](https://www.kaggle.com/noriuk/us-education-datasets-unification-project)

> The input and output files are a bit too large to host on GitHub, so I've hosted them on Kaggle. 


## Reflections

For this project, I tried to improve my software engineering practices. I wanted to make it easy to come back to in the future.

* Decoupling between data processing steps
* Logging in each step
* A sanity check that's generated each time the pipeline is run

Hopefully these steps will lower the learning curve for whenever I have time to expand the code base.

