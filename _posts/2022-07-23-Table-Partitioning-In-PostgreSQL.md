In database lingo, partitioning refers to the splitting of a table into smaller physical units. It helps speed up queries by reducing the amount of data to sift through, and enabling action on chunks rather than individual rows.

![Sliced bread](/assets/images/articles/sql-table-partitioning/bread.jpg)

*(Photo by [Young Shih][bread-img-source] on [Unsplash][unsplash])*

Partitioning is typically applied when the volume of data involved is considerably large. A common tactic is to place frequently used partitions in high-speed [SSD][ssd]s, while relegating stale data to cheaper (and hence slower) storage media.

## Types of Partitions

*PostgreSQL* implements 3 partitioning mechanisms:

### I. Range partitioning

Defines partitions using *ranges of values* from key column(s); with the lower bound being inclusive, and the upper exclusive. e.g.

```sql
CREATE TABLE covid_data (
    day         date NOT NULL,
    country     varchar(70) NOT NULL,
    confirmed   bigint NOT NULL,
    deaths      integer NOT NULL
)
PARTITION BY RANGE (confirmed);   -- use no. of confirmed cases as partition key

CREATE TABLE covid_data_confirmed_upto_1e4 PARTITION OF covid_data
    FOR VALUES FROM (0) TO (10000);
CREATE TABLE covid_data_confirmed_1e4_to_1e5 PARTITION OF covid_data
    FOR VALUES FROM (10000) TO (100000);
...
```

### II. List partitioning

Defines partitions by explicitly *listing the values to appear* in each one. e.g.

```sql
CREATE TABLE covid_data (
    day         date NOT NULL,
    country     varchar(70) NOT NULL,
    confirmed   bigint NOT NULL,
    deaths      integer NOT NULL
)
PARTITION BY LIST (left(upper(country), 1));  -- Partition by country 1st letter

CREATE TABLE covid_data_countries_a_to_d PARTITION OF covid_data
    FOR VALUES IN ('A', 'B', 'C', 'D');
CREATE TABLE covid_data_countries_e_to_h PARTITION OF covid_data
    FOR VALUES IN ('E', 'F', 'G', 'H');
...
```

### III. Hash partitioning

Defines partitions using the *remainder* from applying a *hash function* to the partition key and dividing by a *specified modulus*. e.g.

```sql
CREATE TABLE covid_data (
    day         date NOT NULL,
    country     varchar(70) NOT NULL,
    confirmed   bigint NOT NULL,
    deaths      integer NOT NULL
)
PARTITION BY HASH (confirmed);

CREATE TABLE covid_data_confirmed_rem0 PARTITION OF covid_data
    FOR VALUES WITH (MODULUS 10, REMAINDER 0);  -- where hashed val ends in 0
CREATE TABLE covid_data_confirmed_rem1 PARTITION OF covid_data
    FOR VALUES WITH (MODULUS 10, REMAINDER 1);  -- where hashed val ends in 1
...
```

## Example

Let's carry out a simple experiment to gauge the practicality of partitioning. We'll execute the following transaction as a script ([create_tables.sql][table_script]), and load [sample data][sample]:

```sql
BEGIN;
CREATE TABLE covid_data (
    day         date NOT NULL,
    country     varchar(70) NOT NULL,
    confirmed   integer NOT NULL,  -- int OK since all sample values < 2,147,483,647
    deaths      integer NOT NULL
);
CREATE TABLE covid_data_partitioned (
    day         date NOT NULL,
    country     varchar(70) NOT NULL,
    confirmed   integer NOT NULL,
    deaths      integer NOT NULL
)
PARTITION BY RANGE (day);

CREATE TABLE covid_data_2020q1 PARTITION OF covid_data_partitioned
    FOR VALUES FROM ('2020-1-1') TO ('2020-4-1');
CREATE TABLE covid_data_2020q2 PARTITION OF covid_data_partitioned
    FOR VALUES FROM ('2020-4-1') TO ('2020-7-1');
CREATE TABLE covid_data_2020q3 PARTITION OF covid_data_partitioned
    FOR VALUES FROM ('2020-7-1') TO ('2020-10-1');
CREATE TABLE covid_data_2020q4 PARTITION OF covid_data_partitioned
    FOR VALUES FROM ('2020-10-1') TO ('2021-1-1');
CREATE TABLE covid_data_2021q1 PARTITION OF covid_data_partitioned
    FOR VALUES FROM ('2021-1-1') TO ('2021-4-1');
CREATE TABLE covid_data_2021q2 PARTITION OF covid_data_partitioned
    FOR VALUES FROM ('2021-4-1') TO ('2021-7-1');
CREATE TABLE covid_data_2021q3 PARTITION OF covid_data_partitioned
    FOR VALUES FROM ('2021-7-1') TO ('2021-10-1');
CREATE TABLE covid_data_2021q4 PARTITION OF covid_data_partitioned
    FOR VALUES FROM ('2021-10-1') TO ('2022-1-1');
CREATE TABLE covid_data_2022q1 PARTITION OF covid_data_partitioned
    FOR VALUES FROM ('2022-1-1') TO ('2022-4-1');
CREATE TABLE covid_data_2022q2 PARTITION OF covid_data_partitioned
    FOR VALUES FROM ('2022-4-1') TO ('2022-7-1');
CREATE TABLE covid_data_2022q3 PARTITION OF covid_data_partitioned
    FOR VALUES FROM ('2022-7-1') TO ('2022-10-1');
CREATE TABLE covid_data_2022q4 PARTITION OF covid_data_partitioned
    FOR VALUES FROM ('2022-10-1') TO ('2023-1-1');
COMMIT;
```

### 1. Creating a database and loading the data

```bash
$ createdb covid19_data
$ psql covid19_data 
psql (14.4)
Type "help" for help.

covid19_data=> \i create_tables.sql 
BEGIN
CREATE TABLE
CREATE TABLE
CREATE TABLE
CREATE TABLE
CREATE TABLE
CREATE TABLE
CREATE TABLE
CREATE TABLE
CREATE TABLE
CREATE TABLE
CREATE TABLE
CREATE TABLE
CREATE TABLE
CREATE TABLE
COMMIT
covid19_data=> \copy covid_data FROM time-series-data.csv WITH (FORMAT CSV, HEADER);
COPY 181687
covid19_data=> \copy covid_data_partitioned FROM time-series-data.csv WITH (FORMAT CSV, HEADER);
COPY 181687
```

### 2. Evaluating performance

Though results varied across runs, the partitioned table generally took more time planning, but executed the test query much faster:

```sql
covid19_data=> EXPLAIN ANALYZE SELECT * FROM covid_data_partitioned WHERE day BETWEEN '2020-12-24' AND '2020-12-02';
                                     QUERY PLAN                                     
------------------------------------------------------------------------------------
 Result  (cost=0.00..0.00 rows=0 width=0) (actual time=0.001..0.001 rows=0 loops=1)
   One-Time Filter: false
 Planning Time: 0.062 ms
 Execution Time: 0.008 ms
(4 rows)

covid19_data=> EXPLAIN ANALYZE SELECT * FROM covid_data WHERE day BETWEEN '2020-12-24' AND '2020-12-02';
                                                QUERY PLAN                                                
----------------------------------------------------------------------------------------------------------
 Seq Scan on covid_data  (cost=0.00..3922.30 rows=908 width=21) (actual time=9.159..9.159 rows=0 loops=1)
   Filter: ((day >= '2020-12-24'::date) AND (day <= '2020-12-02'::date))
   Rows Removed by Filter: 181687
 Planning Time: 0.052 ms
 Execution Time: 9.184 ms
(5 rows)
```

Had the data been massive, sequential scans would have taken significantly longer, and the planning overhead in the partitioned table would have really paid off. Reminds me of a story about cutting a tree.

## Further Reading

- [Table partitioning][postgres-pt] in *PostgreSQL* docs.
- Database [partitioning][partition-wiki] and [indexing][idx-wiki] on *Wikipedia*.

[bread-img-source]: https://unsplash.com/@yangchihshih
[unsplash]: https://unsplash.com/
[ssd]: https://en.wikipedia.org/wiki/Solid-state_drive
[table_script]: https://github.com/Tim-Abwao/blog-projects/blob/main/sql-table-partition/create_tables.sql
[sample]: https://raw.githubusercontent.com/Tim-Abwao/blog-projects/main/sql-table-partition/time-series-data.csv
[postgres-pt]: https://www.postgresql.org/docs/14/ddl-partitioning.html
[partition-wiki]: https://en.wikipedia.org/wiki/Partition_(database)
[idx-wiki]: https://en.wikipedia.org/wiki/Database_index
