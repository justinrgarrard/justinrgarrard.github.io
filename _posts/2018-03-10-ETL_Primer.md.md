---
layout: post
title: "ETL Primer"
categories:
  - Project
tags:
  - Python
---

ETL (Extract, Transform, and Load) is the practice of preparing data for use. It's something of a prerequisite for Data Science, and pops up in a good number of other contexts. This page is intended to serve as a helpful reference for programmers that don't engineer data pipelines on a daily basis. It covers simple, small-scale use cases.

### Extract

Extraction is the process of pulling data together from various digital sources. It covers a broad range of technologies.

* [File Extraction](../etlprimer/2018/01/08/Filetype_interfaces.html) (.txt, .csv, .xls, etc.)
* [Database Queries](../etlprimer/2018/01/11/Database_queries.html)
* API Requests
* Web Scraping

### Transform

Transformation encompasses techniques for modifying data to suit one's purposes. It's focus is ensuring that the data is easy to use.

* Cleaning (outlier removal, handling NaN's)
* Organizing (renaming columns, ensuring consistency)
* Reshaping (isolating data, joining data, transposing, melting)

### Load

Loading is about wrapping the finished data in a neat package. It's the simplest of the three.

* Exporting data (database, files, reports)
* Location (access, size, referential integrity)
* Documentation (where did it come from, what did you do to it, what is it now)

