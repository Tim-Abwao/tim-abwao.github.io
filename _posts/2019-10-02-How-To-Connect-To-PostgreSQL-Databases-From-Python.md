---
tags: sql postgres
last_modified_at: 2021-11-07T20:32:00+03:00
---
[PostgreSQL][1] is a *reliable*, *high-performance* open-source [object-relational database management system][2]. It can hold databases as large as 32TB, with virtually unlimited rows.

![Elaphant](/assets/images/articles/elephant.jpg)

(*Photo by [Zoë Reeve][3] on [Unsplash][4]*)

## Psycopg2 - Python's Vessel into Postgres

[Psycopg][5] is a *robust* Python adaptor for *PostgreSQL*. It enables you to create databases, run [SQL][6] queries, and accomplish pretty much every other task you'd wish to on *postgres* databases; from within Python programs.

*Psycopg "...was designed for heavily multi-threaded applications that create and destroy lots of cursors and make a large number of concurrent INSERTs or UPDATEs.*"[^1] This is good news for any who have concerns about scalability.

Example use-cases:

- Flask or django apps & websites using *Postgres* databases to persist user data.
- Automated analysis & report-generating programs written in Python, sourcing data from and saving it to  *Postgres* databases.

>**TIP:** If you'd like to perform [Object–relational mapping][10], check out [SQLAlchemy][11].

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

Connecting to database *"my_db"*, on a *locally running postgres*  server, as the user *"my_username"*:

```python
from getpass import getpass

import psycopg2

# Establish a connection to the database
conn = psycopg2.connect(
    user="my_username",
    dbname="my_db",
    password=getpass(prompt="User password: "),
    host="localhost"
)
cursor = conn.cursor()

cursor.execute(
    """
    CREATE TABLE clients (
        id              serial PRIMARY KEY,
        name            text NOT NULL,
        email           text NOT NULL,
        total_purchases money NOT NULL,
        date            timestamp NOT NULL
    );
    """
)
cursor.execute(
    "INSERT INTO clients VALUES (%s, %s, %s, %s, %s)",
    ("1234", "ACME Corp.", "info@acme.co", 10000, "01-01-2020")
)

# Persist changes
conn.commit()

# Terminate the connection to the database
cursor.close()
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

[^1]: The Psycopg Team (2021). *"Psycopg 2.9.2 documentation"* <https://www.psycopg.org/docs/>.

[1]: https://www.postgresql.org
[2]: https://database.guide/what-is-an-ordbms
[3]: https://unsplash.com/photos/9hSejnboeTY
[4]: https://unsplash.com/
[5]: https://www.psycopg.org/docs/
[6]: http://www.sqlcourse.com/intro.html
[7]: https://www.psycopg.org/docs/install.html#quick-install
[8]: https://www.psycopg.org/docs/install.html#build-prerequisites
[9]: https://www.psycopg.org/docs/usage.html#
[10]: https://en.wikipedia.org/wiki/Object%E2%80%93relational_mapping "ORM"
[11]: https://www.sqlalchemy.org/
