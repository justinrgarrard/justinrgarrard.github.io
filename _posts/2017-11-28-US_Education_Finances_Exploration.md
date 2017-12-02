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

**UPDATE**: This project write-up was updated December 2nd.

The objective of this [mini-project](https://github.com/justinrgarrard/EducationalFinances) was to familiarize myself with Python's tools for interacting with spreadsheets (xlrd, xlwt, openpyxl). To that end, I aggregated U.S. Census data from 1993 to 2015 on educational finances. 

## The Data

[U.S. School Finances](https://www.kaggle.com/noriuk/us-educational-finances): An annual survey that records revenues and expenditures for each school district in the U.S. I made use of the "All Data" tables to generate a pair of easy-to-use CSV files.

[elsec_main.csv] A comma-separated spreadsheet containing revenues and expenditures for all U.S. school districts, 1993-2015.

    STATE,NAME,YRDATA,TOTALREV,TFEDREV,TSTREV,TLOCREV,TOTALEXP,TCURELSC,TCURINST,TCURSSVC,TCUROTH,NONELSEC,TCAPOUT
    Alabama,AUTAUGA CO SCH DIST,2000,48294,3344,34783,10167,49796,42037,26648,12921,2468,752,4761
    Alabama,BALDWIN CO SCH DIST,2000,150579,10578,78199,61802,138009,128009,81035,40483,6491,2792,5378

[elsec_summary.csv] A comma-separated spreadsheet containing state summaries of revenues and expenditures, organized by year.

    STATE,YEAR,TOTAL_REVENUE,FEDERAL_REVENUE,STATE_REVENUE,LOCAL_REVENUE,TOTAL_EXPENDITURE,PROGRAM_CURRENT_EXPENDITURE,INSTRUCTION_EXPENDITURE,SUPPORT_SERVICES_EXPENDITURE,PROGRAM_OTHER_EXPENDITURE,PROGRAM_NON_ELSEC_EXPENDITURE,CAPITAL_OUTLAY_EXPENDITURE
    Alabama,1993,2827391,331409,1729295,766687,2833433,2569466,1564558,794146,210762,26460,204207
    Alaska,1993,1191398,176150,775829,239419,1126398,959013,494917,433788,30308,5983,135791


## The Details

```
.zip -> .xls -> .csv -> SQL -> .csv
```

The numerous .xls spreadsheets are extracted from a .zip archive. From there, they are parsed using Pandas, xlrd, and regular expressions. The first aggregate [elsec_main.csv] is written to a CSV file.

The CSV file is easily imported into an SQLite database, allowing for SQL-style queries. The second aggregate file [elsec_summary.csv] organizes entries by state and year. Users looking to aggregate the data differently should have a fairly easy time modifying the existing code to do so. 
