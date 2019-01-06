---
layout: post
title: "Database Queries"
categories:
  - Notes
tags:
  - ETL
  - Notes
---

At a certain point, it stops being feasible to store data in a file format. You'll know you're at this point when your text editor crashes from the strain of trying to open a 2 GB CSV or when Excel flat out tells you that it can't load every row.

The solution to unwieldy data is databases. They offer a way to organize, store, and access information on a scale beyond files. This page gives a quick overview of how to read data from various databases using Python.

*Databases are a really big topic, one that entire careers are based on. This writeup is just a cursory overview for programmers that need to grab something. It doesn't cover insertion, deletion, subqueries, first-normal form, or anything beyond basic queries. Those looking for a more in-depth tutorial should check out a more substantial intro like Udacity's free [Relational Databases](https://www.udacity.com/course/intro-to-relational-databases--ud197) course.*

# SQL and SQL Accessories

The most common form of database is a SQL (Structured Query Language) database. They're time-tested, having had decades to work out the bugs and formalize the rules.

A SQL database consists of tables which hold related information. They look an awful lot like your average everyday spreadsheet. Each category is strongly typed (text, number, etc.) though the typing system depends on the particular flavor of SQL being used.

```
# This is a table we'll call 'people'

name, age, occupation
Kim, 26, Psychologist
John, 50, IT Guy
```

### The Query

A query is just a command to access specific data. SQL queries are written up in their own fairly intuitive language. 

```
SELECT name FROM people;

> Kim, John
```

If we wanted to write that in a Python program, we'd do it like so:

```python
import sqlite3	# A lightweight SQL flavor
database = sqlite3.connect('db')	# Connect to or create the 'db' database
cursor = database.cursor()		# Our interface to the database

query = '''
	SELECT name FROM people;
	'''

cursor.execute(query)
database.commit()			# Tell the database to do run the query

output = cursor.fetchall()		# Grab the output
for row in output:			# Print the results
	print(row)

database.close()	# Always good practice to close your connection
```

**The library and syntax used to interface with a database depends on the database type.** This code will work for SQLite databases, but not for PostgreSQL, MySQL, or MS SQL Server databases. Luckily, many of the database libraries for Python adhere to the same general structure. Here's an example of a MySQL query:

```python
import MySQLdb	# A lightweight SQL flavor
database = MySQLdb.connect(host="localhost",
				user="root",
				passwd="root",
				db="db")	
cursor = database.cursor()		# Our interface to the database

query = '''
	SELECT name FROM people;
	'''

cursor.execute(query)

output = cursor.fetchall()		# Grab the output
for row in output:			# Print the results
	print(row)

database.close()		
```

There are a few minor changes (the connector takes more information, the "commit()" statement is gone), but the general structure is identical to SQLite. 

### SQL Flavors

A quick listing of some of the most common types of SQL.

* **SQLite**: Simple, lightweight SQL implementation. Let's you create temporary databases in memory. Types are very basic (text, number). Library: [sqlite3](https://docs.python.org/3/library/sqlite3.html)
* **PostgreSQL**: Fairly common open-source SQL implemenation. Library: [psycopg2](https://wiki.postgresql.org/wiki/Psycopg2_Tutorial)
* **MySQL**: Extremely common SQL implemenation, often used in Linux tech stacks. Library: [MySQLdb](https://mysqlclient.readthedocs.io/)
* **MS SQL Server**: Extremely common SQL implemenation, generally used in Windows tech stacks. Library: [pyodbc](https://github.com/mkleehammer/pyodbc/wiki)

# NoSQL

NoSQL databases fulfill the same general needs of SQL databases, but with enough differences in implemenation that they can't be considered SQL.  

*The exact differences between a NoSQL and a SQL database vary tremendously. The only consistent feature NoSQL databases have in common is that they are "not SQL".*

### MongoDB

Library: [pymongo](http://api.mongodb.com/python/current/tutorial.html)

MongoDB data is represented by JSON-style documents.

```
# We'll call this the 'mg' Collection (which is MongoDB's table)
{
	"author": "Mike",
	"text": "My first blog post!",
	"tags": ["mongodb", "python", "pymongo"],
}
```

Queries aren't quite as pretty as SQL (in my opinion), though they are perfectly understandable with a little practice. Make sure MongoDB is installed and running on your machine ('$mongod' in the terminal).

```python
import pymongo
client = pymongo.MongoClient()
client = MongoClient('localhost', 8080)

database = client['db']		# Connect to the 'db' database
collection = database['mg']		# Connect to the 'mg' Collection

output = posts.find({'author':'Mike'})	# Run the query
for item in output:
	print(item)

```

### Cassandra

Library: [datastax](https://datastax.github.io/python-driver/)

Cassandra is a NoSQL database flavor whose usage closely resembles SQL. Cassandra uses its own faux SQL language called CQL (Cassandra Query Language).

```python
from cassandra.cluster import Cluster
database = Cluster(port=8080)	# Connect to or create a Cluster (~ a database)
session = cluster.connect('people')	# Connect to a Node (~ a table)

output = session.execute('SELECT name FROM people')	#Very similar to a SQL query
for row in output:
	print(row)
```

