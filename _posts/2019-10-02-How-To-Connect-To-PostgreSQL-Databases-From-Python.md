---
author: Abwao
layout: post
last_modified_at: 2020-05-24T21:20:00+03:00
---
[PostgreSQL](https://www.postgresql.org) is a **fast** and **reliable** open-source [object-relational database management system](https://database.guide/what-is-an-ordbms).
It can hold databases as large as 32TB, with virtually unlimited rows.

![Elaphant](/assets/images/articles/elephant.jpg)<br>
<sub>*Photo by <a href="https://unsplash.com/@zoeeee_?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Zoë Reeve</a> on <a href="https://unsplash.com/">Unsplash</a>*</sub>

## Psycopg2 - Python's Vessel into Postgres

[Psycopg](http://initd.org/psycopg/docs) is a **robust** Python adaptor for PostgreSQL. It enables you to create databases, run [SQL](http://www.sqlcourse.com/intro.html) queries, and accomplish pretty much every other task you'd wish to with your postgres database(s); from within Python programs.

The Psycopg official website states that "_It was designed for heavily multi-threaded applications that create and destroy lots of cursors and make a large number of concurrent INSERTs or UPDATEs._" This is good news for any who are concerned about scalability.

Example use-cases include:

- Storing users' account/transaction/etc data to Postgres databases from flask or django websites & blogs.
- Extracting data from Postgres databases for automated data analysis and report-generating apps written in Python.

## Installation

The following are required:

- A C compiler
- Python header files (**python-dev** or **python3-dev**)
- **libpq** header files
- The **pg_config** program

In general, if you already have *Postgres* and Python installed, then

```bash
$ sudo apt-get install python3-dev libpq-dev  
$ pip install psycopg2
```

should do the trick.

To find out more on resolving dependencies and installing from source, please visit the Psycopg [installation page](https://www.psycopg.org/docs/install.html).

## Basic Usage

In oder to connect to a database, say perhaps one named _database1_, on a _locally running_ Postgres server, as the user _user1_; you could try:

```python
import psycopg2 as ps

# Connecting to the database
conn = ps.connect("dbname=database1 user=user1 password=user1password host=localhost")

# Opening a cursor to perform database operations
cur = conn.cursor()

# Executing an SQL query
cur.execute("SELECT * FROM table1;")

# Assigning obtained data to the variable 'data'
data = cur.fetchall()

#Creating a table
cur.execute("""
            CREATE TABLE clients (
                    Name text,
                    Email text,
                    Total_Purchases money,
                    Date timestamp
                );
            """)

# Adding a record
cur.execute("INSERT INTO clients VALUES (%s, %s, %s, %s,)",
            ("ACME Corp.", "info@acme.co", 10000, "01-01-2020"))

# Saving the changes to the database
conn.commit()

# Closing the connection to the database
cur.close()
conn.close()
```

## Next Steps

Now that you're familiar with some of psycopg's  features, please consider visiting the [Basic module usage](https://www.psycopg.org/docs/usage.html#) page in the official docs. 

Psycopg's developers have done an excellent job of explaining how it works, and how to use it. Here are some of the topics covered:

- Passing parameters to SQL queries
- Adapting Python values to SQL types
- Accessing PostgreSQL large objects
- Server side cursors
- Thread and process safety
- Transactions control.

