---
layout: post
title: "U.S. Education Finances"
categories:
  - Kaggle
tags:
  - Kaggle
  - Python
---

## Overview

The objective of this [mini-project](https://github.com/justinrgarrard/EducationalFinances) was to familiarize myself with Python's tools for interacting with spreadsheets (xlrd, xlwt, openpyxl). To that end, I aggregated U.S. Census data from 2002 to 2015 on educational finances. 

## The Data

[U.S. School Finances](https://www.kaggle.com/noriuk/us-educational-finances): An annual survey that records revenues and expenditures for each school district in the U.S. I made use of the surveys from 2002 onwards, as the corresponding spreadsheets were neatly organized by state. I might attempt a more comprehensive aggregation in the future.


## The Details

The core of this project is a Python script that navigates spreadsheets and harvests the relevant data. The process involved a smattering of regular expressions but wasn't otherwise complex. I was impressed with how easy it is to access sheets and cells using xlrd and openpyxl. Moreover, the fact that both tools are integrated into Pandas was an unexpected surprise. 
