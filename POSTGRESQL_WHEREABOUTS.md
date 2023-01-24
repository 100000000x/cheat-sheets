# PostgreSQL Whereabouts

## Questions to ask
1. What server name am I connecting to?
2. What database name am I connecting to?
3. What table name am I connecting to?
4. What database program do I use?
5. What programming language do I use to connect to the database program?
6. What adapter do I use to connect to the database program?

## PostgreSQL database.ini
```console
[postgresql]
host=string
dbname=string
user=string
password=string
port=integer
```
## PostgreSQL config / connect
```python3
import ConfigParser
import psycopg
import config

def config(filename='database.ini', section='postgresql'):

parser = ConfigParser()
parser.read(filename)

db = {}
  if parser.has_section(section):
  params = parser.items(section)
  for param in params:
  db[param[0]] = param[1]
  else:
  raise Exception('Section {0} not found in the {1} file'.format(section, filename))

  return db

  def connect():

  conn = None

  try:
  params = config()

  print('Connecting to the PostgreSQL database...')
  conn = psycopg.connect(**params)

  cur = conn.cursor()
  print('PostgreSQL database version:')

  #cur.execute("SQL COMMAND %s", (VAR1))
  #conn.commit()

  #cur.execute("SQL COMMAND %s", (VAR1))
  #row = cur.fetchone()

  cur.execute('SELECT version()')
  db_version = cur.fetchone()
  print(db_version)

  cur.close()

  except (Exception, psycopg.DatabaseError) as error:
  print(error)

  finally:
  if conn is not None:
  conn.close()
  print('Database connection closed.')
  ```
## PostgreSQL and pgAdmin4 setup Ubuntu
```console
sudo apt update && sudo apt upgrade
sudo apt install postgresql postgresql-contrib
sudo apt install curl
sudo curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add
sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
sudo apt install pgadmin4
sudo ufw allow http
sudo ufw allow https
http://localhost:5050/browser/
```
## PostgreSQL / PQSL commands
```
pg_lsclusters
time psql < gemeinden.sql
systemctl status postgresql
ps -ef | grep postgres
sudo -i
su - postgres
sudo -i -u postgres
psql
pg_ctl
pg_dump
pg_dumpall
pg_restore
pg_basebackup
pg_createcluster
show search_path
systemctl stop postgresql
systemctl start postgresql
systemctl restart postgresql
psql -p 5433
sudo -u postgres createuser --interactive
sudo adduser postgres
sudo -i -u postgres
psql -d postgres
psql -U postgres -d postgres
psql -h host -U postgres -d postgres -f inputfile
\?
\h
\c databasename
\h alter role
\h table
\l
\l+
\i
\z
\pset tuples_only=on fieldsep=';'
\echo
\set name Franz # '':
\timing
\watch
\copy tablename to 'filename'
\copy tablename from PRGOGRAM 'command'
\di
\dn
\du
\df
\dv
\dt
\df+ function_name
\dt+
\d+ table_name
\x
\password
\q
show all;
show search_path;
set search_path to schema;
```
## SQL Commands
```sql
Delete Duplicates
DELETE FROM
    basket a
        USING basket b
WHERE
    a.id < b.id
    AND a.fruit = b.fruit;

Create a new role with a username and password:
CREATE ROLE username NOINHERIT LOGIN PASSWORD password;

Change role for the current session to the new_role:
SET ROLE new_role;

Allow role_1 to set its role as role_2:
GRANT role_2 TO role_1;

Create a new database:
CREATE DATABASE [IF NOT EXISTS] db_name;

Delete a database permanently:
DROP DATABASE [IF EXISTS] db_name;

Create a new table or a temporary table:
CREATE [TEMP] TABLE [IF NOT EXISTS] table_name(
   pk SERIAL PRIMARY KEY,
   c1 type(size) NOT NULL,
   c2 type(size) NULL,
   ...
);

Add a new column to a table:
ALTER TABLE table_name ADD COLUMN new_column_name TYPE;

Drop a column in a table:
ALTER TABLE table_name DROP COLUMN column_name;

Rename a column:
ALTER TABLE table_name RENAME column_name TO new_column_name;

Set or remove a default value for a column:
ALTER TABLE table_name ALTER COLUMN [SET DEFAULT value | DROP DEFAULT]

Add a primary key to a table:
ALTER TABLE table_name ADD PRIMARY KEY (column,...);

Remove the primary key from a table:
ALTER TABLE table_name
DROP CONSTRAINT primary_key_constraint_name;

Rename a table:
ALTER TABLE table_name RENAME TO new_table_name;

Drop a table and its dependent objects:
DROP TABLE [IF EXISTS] table_name CASCADE;

Create a view:
CREATE OR REPLACE view_name AS
query;

Create a recursive view:
CREATE RECURSIVE VIEW view_name(column_list) AS
SELECT column_list;

Create a materialized view:
CREATE MATERIALIZED VIEW view_name
AS
query
WITH [NO] DATA;

Refresh a materialized view:
REFRESH MATERIALIZED VIEW CONCURRENTLY view_name;

Drop a view:
DROP VIEW [ IF EXISTS ] view_name;

Drop a materialized view:
DROP MATERIALIZED VIEW view_name;

Rename a view:
ALTER VIEW view_name RENAME TO new_name;

Creating an index with the specified name on a table:
CREATE [UNIQUE] INDEX index_name
ON table (column,...)

Removing a specified index from a table:
DROP INDEX index_name;
Querying data from tables

Query all data from a table:
SELECT * FROM table_name;

Query data from specified columns of all rows in a table:
SELECT column_list
FROM table;

Query data and select only unique rows:
SELECT DISTINCT (column)
FROM table;

Query data from a table with a filter:
SELECT *
FROM table
WHERE condition;

Assign an alias to a column in the result set:
SELECT column_1 AS new_column_1, ...
FROM table;

Query data using the LIKE operator:
SELECT * FROM table_name
WHERE column LIKE '%value%'

Query data using the BETWEEN operator:
SELECT * FROM table_name
WHERE column BETWEEN low AND high;

Query data using the IN operator:
SELECT * FROM table_name
WHERE column IN (value1, value2,...);

Constrain the returned rows with the LIMIT clause:
SELECT * FROM table_name
LIMIT limit OFFSET offset
ORDER BY column_name;

Inner join:
SELECT *
FROM table1
INNER JOIN table2 ON conditions

Left join:
SELECT *
FROM table1
LEFT JOIN table2 ON conditions

Full outer join:
SELECT *
FROM table1
FULL OUTER JOIN table2 ON conditions

Cross join:
SELECT *
FROM table1
CROSS JOIN table2;

Natural join:
SELECT *
FROM table1
NATURAL JOIN table2;

Return the number of rows of a table:
SELECT COUNT (*)
FROM table_name;

Sort rows in ascending or descending order:
SELECT select_list
FROM table
ORDER BY column ASC [DESC], column2 ASC [DESC],...;

Group rows using GROUP BY clause:
SELECT *
FROM table
GROUP BY column_1, column_2, ...;

Filter groups using the HAVING clause:
SELECT *
FROM table
GROUP BY column_1
HAVING condition;

Combine the result set of two or more queries with UNION operator:
SELECT * FROM table1
UNION
SELECT * FROM table2;

Minus a result set using EXCEPT operator:
SELECT * FROM table1
EXCEPT
SELECT * FROM table2;

Get intersection of the result sets of two queries:
SELECT * FROM table1
INTERSECT
SELECT * FROM table2;

Insert a new row into a table:
INSERT INTO table(column1,column2,...)
VALUES(value_1,value_2,...);

Insert multiple rows into a table:
INSERT INTO table_name(column1,column2,...)
VALUES(value_1,value_2,...),
      (value_1,value_2,...),
      (value_1,value_2,...)...

Update data for all rows:
UPDATE table_name
SET column_1 = value_1,
    ...;

Update data for a set of rows specified by a condition in the WHERE clause:
UPDATE table
SET column_1 = value_1,
    ...
WHERE condition;

Delete all rows of a table:
DELETE FROM table_name;

Delete specific rows based on a condition
DELETE FROM table_name
WHERE condition;

Show the query plan for a query:
EXPLAIN query;
Show and execute the query plan for a query:
```
## SQL - Pandas equivalents

```sql
Select * from df
PANDAS EQUIVALENT IS
df

Select owner from df
PANDAS EQUIVALENT IS
df[['owner']]
df.iloc[ : ,2]
df.loc[ : ,['owner']]

Select * from df limit 2
PANDAS EQUIVALENT IS
df.head(2)

Select distinct product_name from df
PANDAS EQUIVALENT IS
df.product_name.unique()

Select * from df where product_name = "pen"
PANDAS EQUIVALENT IS
df[df['product_name'] == 'pen']
df.loc[df['product_name']== 'pen']
df.query('product_name == "pen"')
df[df.apply(lambda x: x['product_name'] == 'pen', axis=1)]

Select * from df where product_name = "pen" and price = 2
PANDAS EQUIVALENT IS
df[(df['product_name'] == 'pen') & (df['price']==2)]
df.loc[(df['product_name']== 'pen') & (df['price'] == 2)]
df.query('product_name == "pen" and price ==2')
df[df.apply(lambda x: x['product_name'] == 'pen' and x['price'] == 2, axis=1)]

Select owner, product name from df where product_name = "pen"
PANDAS EQUIVALENT IS
df[df['product_name'] == 'pen'][['owner','product_name']]
df.loc[df['product_name']== 'pen', ['owner','product_name']]

Select * from df where product_name like "pen%"
PANDAS EQUIVALENT IS
df[df['product_name'].str.startswith('pen')]
df[df['product_name'].str.contains('pen')]

Select * from df where product_name like "%pen"
PANDAS EQUIVALENT IS
df[df['product_name'].str.endswith('pen')]
df[df['product_name'].str.contains('pen')]

Select * from df where product_name in ('pen','pencil')
PANDAS EQUIVALENT IS
df[df['product_name'].isin(['pen','pencil'])]

Select * from df where product_name not in ('pen','pencil')
PANDAS EQUIVALENT IS
df[~df['product_name'].isin(['pen','pencil'])]

Select count(product_name) from df
PANDAS EQUIVALENT IS
df['product_name'].count()

Select sum(price) from df
PANDAS EQUIVALENT IS
df['product_name'].sum()

Select min(price) from df
PANDAS EQUIVALENT IS
df['product_name'].min()

Select max(price) from df
PANDAS EQUIVALENT IS
df['product_name'].max()

Select count(price), count(distinct price), sum(price), min(price), max(price) from df
PANDAS EQUIVALENT IS
df.agg({'price': ['count','nunique','sum','min', 'max']})

Select owner, sum(price) from df group by sum(price)
PANDAS EQUIVALENT IS
df.groupby('owner').agg({'price':'sum'}).reset_index()

Select owner, product_name, sum(price) from df group by owner, product_name
PANDAS EQUIVALENT IS
df.groupby(['owner','product_name']).agg({'price':'sum'}).reset_index()
view raw

Select owner, sum(price) from df group by sum(price) order by sum(price)
PANDAS EQUIVALENT IS
df.groupby('owner').agg({'price':'sum'}).sort_values(by=['price']).reset_index()

Select owner,count(product_name), sum(price) from df group by owner order by sum(price), count(product_name)
PANDAS EQUIVALENT IS
df.groupby(['owner']).agg({'price':'sum','product_name':'count'}).sort_values(by=['price','product_name']).reset_index()

Select owner, sum(price) from df group by sum(price) order by sum(price) desc
PANDAS EQUIVALENT IS
df.groupby('owner').agg({'price':'sum'}).sort_values(by=['price'], ascending = 'FALSE').reset_index()

Select df.owner, product_name, class, teacher from df left join df2 on df.owner = df2.owner
PANDAS EQUIVALENT IS
pd.merge(df[['owner','product_name']], df2, how="left", on=["owner"])

Select df2.*, product_name, price from df right join df2 on df.owner = df2.owner
PANDAS EQUIVALENT IS
pd.merge(df, df2, how="right", on=["owner"])

Select df2.*, product_name from df inner join df2 on df.owner = df2.owner
PANDAS EQUIVALENT IS
pd.merge(df[['product_name','owner']], df2, how="inner", on=["owner"])

Select df2.*, product_name from df outer join df2 on df.owner = df2.owner
PANDAS EQUIVALENT IS
pd.merge(df[['product_name','owner']], df2, how="outer", on=["owner"])
```
