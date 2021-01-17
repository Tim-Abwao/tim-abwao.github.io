---
last_modified_at: 2020-09-04T17:58:00+03:00
---
[PostgreSQL][1] is a *reliable*, *high-performance* open-source [object-relational database management system][2]. It can hold databases as large as 32TB, with virtually unlimited rows.

![Elaphant](/assets/images/articles/elephant.jpg)

(*Photo by [Zoë Reeve][3] on [Unsplash][4]*)

## Psycopg2 - Python's Vessel into Postgres

[Psycopg][5] is a *robust* Python adaptor for *PostgreSQL*. It enables you to create databases, run [SQL][6] queries, and accomplish pretty much every other task you'd wish to on *postgres* databases; from within Python programs.

*Psycopg's* authors assert that it "_...was designed for heavily multi-threaded applications that create and destroy lots of cursors and make a large number of concurrent INSERTs or UPDATEs._" This is good news for any who have concerns about scalability.

Example use-cases:

- Flask or django apps & websites using *Postgres* databases to persist user data.
- Automated analysis & report-generating programs written in Python, sourcing data from and saving it to  *Postgres* databases.

## Installation

You can install a [pre-compiled binary version][7] with:

```bash
pip install psycopg2-binary
```

The following are necessary when installing the [source distribution][8]:

- A C compiler
- Python header files (*python-dev* or *python3-dev*)
- *libpq* header files
- The *pg_config* program

In general, if you already have *Postgres* and Python installed, then

```bash
sudo apt-get install python3-dev libpq-dev  
pip install psycopg2
```

should do the trick. If this fails, please refer to the [installation page][8].

## Basic Usage

Connecting to database  _database1_, on a _locally running_ Postgres server, as the user _user1_:

```python
import psycopg2 as ps

conn = ps.connect("dbname=database1 user=user1 password=user1password host=localhost")
cur = conn.cursor()

cur.execute("""
    CREATE TABLE clients (
        id serial PRIMARY KEY,
        Name text,
        Email text,
        Total_Purchases money,
        Date timestamp
    );"""
)
cur.execute("INSERT INTO clients VALUES (%s, %s, %s, %s, %s)",
            ("1234", "ACME Corp.", "info@acme.co", 10000, "01-01-2020"))

conn.commit()
cur.close()
conn.close()
```

## Next Steps

Please consider visiting [Basic module usage][9] to learn more on:

- Passing parameters to SQL queries
- Adapting Python values to SQL types
- Accessing *PostgreSQL* large objects
- Server side cursors
- Thread and process safety
- Transaction control.

[1]: https://www.postgresql.org
[2]: https://database.guide/what-is-an-ordbms
[3]: https://unsplash.com/photos/9hSejnboeTY
[4]: https://unsplash.com/
[5]: https://www.psycopg.org/docs/
[6]: http://www.sqlcourse.com/intro.html
[7]: https://www.psycopg.org/docs/install.html#quick-install
[8]: https://www.psycopg.org/docs/install.html#build-prerequisites
[9]: https://www.psycopg.org/docs/usage.html#
