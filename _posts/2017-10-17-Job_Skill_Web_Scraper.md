---
layout: post
title: "Job Skill Webscraper"
categories:
  - Project
---

## Overview

![Visual of Web Scraper](/assets/images/data_analyst_keywords.png)

The [Job Skill Webscraper](https://github.com/justinrgarrard/JobSkillAssessor) is designed to traverse Indeed.com for a specific job title (i.e. Software Engineer) and report on the most frequently requested skills. It collects job postings to store as text, allowing for processing and visualization.

## Data Wrangling

Job posting write-ups are harvested from the links posted on Indeed.com using the Request and BeautifulSoup libraries. Extracted text is collected into a CSV file (with each entry representing a single job posting).

```
def get_job_links(target):
    """
    Scans through the target website for links to job postings.

    :param target: Website URL.
    :return: A list of url suffixes.
    """
    page = urllib.request.urlopen(target)
    soup = BeautifulSoup(page, "lxml")

    all_links = soup.find_all("a")
    links = [link.get('href') for link in all_links]
    job_links = []
    # Pick a few common headers and roll with it
    for link in links:
        if link and ('pagead' in link or 'rc/' in link or 'company/' in link):
            job_links.append(link)
    return job_links
```

1. The script takes in a website URL for Indeed.com (target).
```
https://www.indeed.com/jobs?q=data+scientist&start=0
```

2. The Request library pretends to be a web browser and asks for the web page (page).
```
\<http.client.HTTPResponse object at 0x7f9ca4150f60>
```

3. The BeautifulSoup library reads the web page and organizes it (soup).
```
\<!DOCTYPE html>
\<html lang="en">
\<head>
...
(A bunch of html/css/javascript)
...
```

4. Using BeautifulSoup, we find all of the "a" elements. Those are where web addresses are usually stored (all_links).
```
\<a
  \target="_blank"
  \id="sja1"
  \data-tn-element="jobTitle"
  \class="jobtitle turnstileLink"
  \href="https://www.indeed.com/pagead/long_complicated_alphanumeric_link_name"
  \title="Business Data Analyst"
  \rel="noopener nofollow">
  \Business <b>Data</b> <b>Analyst</b>
\</a>
```

5. We look at all the "a" elements for the "href" attribute. That's the chunk that holds the actual web address.
```
\href="https://www.indeed.com/pagead/long_complicated_alphanumeric_link_name"
```

6. We make sure we're only getting links to job posting, and not to random advertisements or other pages. Luckily Indeed.com follows a consistant pattern with their links. Most have 'pagead', 'rc/' or 'company/' in them.


## Functionallity

Collecting the data is the most time-consuming part of the assessor, but once gathered, it still needs to be processed. 

```
Ref#:P1082

Ph.D. or M.S. in a quantitative field such as Computer Science, Statistics, or Mathematics
Minimum 2 years of professional industry experience in data science
Expertise in machine learning and statistical modeling
Passion to answer Product/Engineering questions with data
Strong ability to code in Python
We get excited about candidates who
Have full stack experience in data collection, aggregation, analysis, visualization, productionization, and monitoring of data science products
Are proficient in small data modeling work: Python, R, Julia, Octave
Are proficient in big data modeling work: Hadoop, Pig, Scala, Spark
Can fish for data: SQL, Pandas, MongoDB
Deploy data science solutions: Java, Python, C++
Communicate concisely and persuasively with engineers and product managers
```

Stop words (such as 'the' or 'and') need to be filtered out, terms should be counted once per posting, capitilization is standardized, and troubleshome characters must be stripped away with the help of regular expressions. What remains can be piped into a Python Counter object. Because some terms are two words long ('Computer Science', 'Microsoft Office') two different Counters are used. 

Even with these precautions, the most common terms will have little bearing on technical skills. Phrases like 'Communication' and 'Human Resources' invariably outnumber 'SQL' or 'Python'. I added in a keyword file to address this problem. The program will pay special attention to terms listed in the keyword file, reporting them distinct from the general results.
