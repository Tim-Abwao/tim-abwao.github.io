---
author: Abwao
layout: post
last_modified_at: 2020-03-17T00:00:00+03:00
---
[PostgreSQL](https://www.postgresql.org) is a **fast** and **reliable** [object-relational database management system](https://database.guide/what-is-an-ordbms). It can hold databases as large as 32TB, with virtually unlimited rows. This makes it an ideal choice for many companies needing to store and access huge volumes of data. What is more, it's **open source**(free).

## Psycopg2 - Python's Vessel into Postgres
[Psycopg](http://initd.org/psycopg/docs) is a **robust** Python adaptor for PostgreSQL. It enables Python programs to connect to PostgreSQL servers, create databases, and run various [SQL](http://www.sqlcourse.com/intro.html) queries and operations. 

The Psycopg official website states that "_It (Psycopg) was designed for heavily multi-threaded applications that create and destroy lots of cursors and make a large number of concurrent INSERTs or UPDATEs._"

Example use-cases include:
- Storing users' account/transaction/etc info to Postgres databases from flask/django websites & blogs.
- Extracting data from Postgres databases for automated, Python-based data analysis and report-generating apps, among others.

## Getting Started
Please see [Installation](https://www.psycopg.org/docs/install.html) for the various ways to install Psycopg2. 

Generally, if you already have PostgreSQL and Python installed, then
``` bash

$ pip install psycopg2

```
should do the trick.

Afterwards, head on to the [Basic Module Usage](https://www.psycopg.org/docs/usage.html) page for an introduction on how to use it. For instance, to connect to a database named _database1_ on a locally running Postgres server as the user _user1_, and obtain data; try the following:

{% highlight python %}

>>> import psycopg2
>>> conn=ps.connect("dbname=database1 user=user1 password=user1password host=localhost ")

# Open a cursor to perform database operations
>>> cur = conn.cursor()

# Execute a command: query data from table1 in the database 
>>> cur.execute("SELECT * FROM table1;")

# Save the data to a variable called 'data'
>>> data=cur.fetchall()

{% endhighlight %} 

You can explore these and more features of Psycopg2 using [this jupyter notebook](https://github.com/Tim-Abwao/Psycopg2-Basics/blob/master/PostgreSQL%20Basics%20with%20Psycopg2.ipynb).