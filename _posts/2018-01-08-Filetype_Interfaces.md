---
layout: post
title: "Filetype Interfaces"
categories:
  - Notes
tags:
  - ETL
  - Notes
---

Data can come in any number of filetypes, which, while fascinating in its own way, can be a headache for programmers. This is a writeup of a few of the most common filetypes and how to use Python to read them.

*This reference tutorial is based off of the excellent free online book* [Automate the Boring Stuff With Python](https://automatetheboringstuff.com).

# Text

### Flat Files (.txt, or no extension)

Plain text data is one of the easiest to interface with. The [Python Docs](https://docs.python.org/3/tutorial/inputoutput.html) cover how to handle it extensively. 

```python
with open('filename.txt') as f:
	data = f.read()			# Puts all the data in a string
	data = f.readline()		# Puts all the data in a list of strings
```

The readline() function divides data by newlines, but it can be tweaked to separate by other characters (f.readline(sep=',')). 


### Word Documents (.doc, .docx)

Word documents are a little trickier to work with than flat files. They're encoded differently than plain text (because of fonts, styles, and other things) so we need a specific [library](https://python-docx.readthedocs.io/en/latest/) to pull information from them.

```python
import docx
document = doxc.Document('filename.docx')
text = []

for paragraph in document.paragraphs:
	text.append(paragraph.text)

text_string = '\n'.join(text)
```

*If you need to preserve formatting, you'll need to do some additional work. Check [chapter 13](https://automatetheboringstuff.com/chapter13/) of* Automate the Boring Stuff With Python *for a more in-depth tutorial.*

### PDF Documents (.pdf)

PDF's are the bane of data miners. Adobe's special propriety encoding is a nightmare to work with, but luckily there are [tools](https://pythonhosted.org/PyPDF2/) to do so.

```python
import PyPDF2
with open('filename.pdf', 'rb') as f:
	scribe = PyPDF2.PdfFileReader(f)
	page = scribe.getPage(0)
	page.extractText()		# Pulls text out as a single string
```

Don't count on the string being an exact likeness of the PDF's text. The translation is imperfect, with strange formatting errors and outright missing pieces. Still, it's better than transcribing the PDF by hand.

*Readers interested in doing more complex work with PDF's can reference this chapter from* [Automate the Boring Stuff With Python](https://automatetheboringstuff.com/chapter13/).

# Spreadsheets

### Comma Seperated Values (.csv)

Despite the name, CSV files come in many different shapes and sizes. The separting character may be a comma, but it might also be a tab or a pipe \|. Luckily CSV's are ubiquitious enough that plenty of programs can read it in without trouble (Excel, Calc, RStudio). Python has a [built-in library](https://docs.python.org/3/library/csv.html) that operates similarly to the standard file reader:


```python
import csv
with open('filename.csv') as f:
	scribe = csv.reader(csvfile, delimeter=',')
	for row in scribe:
		print(', '.join(row))
```

Programmers looking for a heavyweight analysis tool will be better served with the [Pandas library](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html). The read_csv() function translates the csv file straight into a dataframe.

```python
import pandas
data = pandas.read_csv('filename.csv', sep=',')
```

### Excel Spreadsheets (.xls, .xlsx)

A little more complicated than CSV files, the Excel spreadsheet is also much more common. Interfacing with a spreadsheet opens up new avenues for analysis and automation. Unfortunately, there is no built-in tool for reading Excel spreadsheets. We'll need to use a [library](http://www.python-excel.org/).

```python
import xlrd		# Reading .xls files
import xlwt		# Writing .xls files
import openpyxl		# Reading and writing .xlsx files

# .xls (pre-2010) file
book = xlrd.open_workbook('filename.xls')
sheet = book.sheet_by_index(0)		# Open the first sheet in the workbook
cell = sheet.cell(0, 0)			# Get the top-leftmost cell

# .xlsx (2010-) file
book2 = openpyxl.

```

There is also a [Pandas wrapper](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_excel.html) that uses the previously mentioned libraries to convert Excel files into dataframes.

```python
data = pandas.read_excel('filename.xls', sheet_name=0)
```

# Data Structures

### JSON (.json)

Contrary to their name, JSON's (JavaScript Object Notation) have very little to do with JavaScript. The file contents merely resemble programming objects in Javascript:

```
{
	"name": "Fred",
	"occupation": "Shadowrunner",
	"missionsSurvived": 5,
	"knownAssociates": [
	{
		"name": "Jim",
		"missionsSurvived": 0
	},
	{
		"name": "Kim",
		"missionsSurvived": 127
	}
	]
}
```

There is no special encoding on a JSON file; it's plain text and can be opened with any text editor. Programs reading a JSON file will expect it to follow a strict syntax though. This allows JSON objects to be easily passed between different programs in different programming languages. Python comes with a built-in [JSON library](https://docs.python.org/3/library/json.html) for this reason.

```python
import json

with open('filename.json') as f:
	text = f.read()			# Convert the file to text
	json_obj = json.loads(text)	# Convert the text to a dictionary
	print(json_obj['name'])			
```

### XML (.xml)

XML (eXtensible Markup Language) fulfills the same purpose as a JSON. Namely, it offers a plain text format that can encode programming object structures. Many technologies are phasing out the XML format in favor of JSON due to its verbosity but you're likely to stumble on XML files for years to come.

```
<people>
	<person>
		<name>Fred</name>
		<occupation>Shadowrunner</occupation>
	</person>
	<person>
		<name>Jim</name>
		<favoriteLunch>Salad</favoriteLunch>
	</person>
</people>
```

Python comes with a [built-in library](https://docs.python.org/3/library/xml.etree.elementtree.html) for handling XML files. However, many find the [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) and [xmltodict](https://pypi.python.org/pypi/xmltodict) libraries easier to work with.

```python
import xmltodict
with open('filename.xml') as f:
	text = f.read()
	xml_d = xmltodict.parse(text)
	print(xml_d['people']['person']['name'])
```

### Other Tools

* **NLTK**: A Python library for natural language processing.
* **Regular Expressions**: A complex but incredibly powerful toolkit for getting exactly what you want from data.
* **AWK**: An older tool for organizing unencoded data. Useful for pulling data from wonky custom formats. 