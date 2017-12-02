---
layout: category
title: Toolbox
category: toolbox
---

This section covers various tools I've found useful in the past.

### Numpy/Pandas

The data analyst's standard kit. Numpy is a Python library that allows for C-style arrays. It's fast, powerful, and has a bunch of clever features for statistical summaries.

Pandas builds on top of Numpy (and many other libraries). It offers Dataframes, multi-dimensional Numpy arrays that mimic tables. There are also functions for importing and exporting Dataframes. 

```
'''
An example of parsing an XLS spreadsheet into a CSV file with Pandas.
'''

import pandas as pd

book = pd.ExcelFile(filename)
data = book.parse(0)
data.to_csv(output_filename)
```


### SQLite3/bleach

SQLite3 is a Python library that makes lightweight SQL work easy. I'm fond of its ability to create in-memory databases for quick-and-dirty work. SQLite3 pairs well with Bleach, a library for cleaning inputs to avoid SQL injection.

```
'''
Creates an in-memory database and a table called misc.
Inserts cleaned data.
'''

import sqlite3
import bleach

con = sqlite3.connect(':memory:')
cur = con.cursor()
data = ['stuff', 6, 'things']

cur.execute("DROP TABLE if EXISTS misc")

q = \
	'''
	CREATE TABLE misc(
	garbage TEXT,
	numbers INT,
	junk TEXT);
	'''
cur.execute(q)

cur.execute("INSERT INTO misc(garbage, number, junk), "
			"VALUES(?, ?, ?);",
			(bleach.clean(data[0]),
			 bleach.clean(data[1]),
			 bleach.clean(data[2])))

con.commit()

```


### argparse

The Software Engineer's best friend. Makes Python scripting easy by offering a simple set of functions for parsing input arguments. It automatically generates a usage statement to boot.

```
def parse_args():
    """
    Parses input arguments.
    :return: An argparse object.
    """
    parser = argparse.ArgumentParser(
        description="A script to scrape job postings.")
    parser.add_argument('--job_title', default="data scientist", nargs="?",
                        const='1', help="The job title to search for.")
    parser.add_argument('--limit', default="100", nargs="?", const='1',
                        help="The number of pages to scan.")
    parser.add_argument('--output_filename', default="output.csv", nargs="?",
                        const='1', help="The filename used for output.")
    arguments = parser.parse_args()
    return arguments

...

args = parse_args()
job = args.job_title.replace(' ', '+')
pages = int(args.limit)
```


### Jupyter Notebook

A different type of environment for programming in Python. I find it especially useful for prototyping, as code is separated into blocks. Users can run individual chunks of the code without having to run an entire program (ala PyCharm). 


### Requests/BeautifulSoup

Requests is a library that simplifies HTTP requests like POST and GET. It's significantly better than trying to handwrite API calls and forcefeed them to a terminal. It can also be used to open full-fledged web pages.

BeautifulSoup handles the XML files that often come out of Requests. It can access specific elements or search through categories of elements. 


### matplotlib/ggplot2

Two libraries that help with visualizing data. They can be used to produce many different types of graphs. I personally prefer ggplot2 (an R library), but Python and MATLAB devotees may find matplotlib more to taste.


### xlrd/openpyxl

These libraries are actually used by Pandas for accessing spreadsheets. If you need to do something very specific, it might be a good idea to use them instead. Openpyxl works with .xlsx files (Excel 2010+) while xlrd is meant for .xls files (earlier Excel versions).


### NLTK

A natural language processing (NLP) library with substantial content. It can tokenize sentences, download text corpora, recognize stopwords, and do a hundred other things. I've used it in the past to create personalized Naive Bayes classifiers.


### fuzzywuzzy

A simple but effective Python library for fuzzy string matching (i.e. 'rectangel' to 'rectangle'). 


### scikit-learn

More of a toolbox than a single tool, the scikit-learn library has dozens of machine learning algorithms built in. Programmers familiar with Classifiers and Regressors should find plenty to keep occupied.


### XGBoost

A third-party Boosting algorithm for machine learning. It's become fairly popular on Kaggle, but it can be a bit of a pain to work with. Unlike scikit-learn, XGBoost doesn't play nicely with Pandas. 


### Scapy

A packet-manipulation library that's useful for automating low-level network things. I used it extensively back when I was building an automated testing suite for a network switch. Others have found it useful for Black Hat work.


### Hadoop

A powerful distributed infrastructure that lets programmers take advantage of multiple computers to run a single program, without all the hassle of coding it up in C (looking at you MPI). Hadoop is associated with an entire ecosystem of other tech relating to the storage and query of "Big Data".

I'd recommend using a virtual machine copy for tinkering. I've managed to install Hadoop locally on two separate occasions, but both were arduous ordeals. 
