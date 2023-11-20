# psql
Some useful `psql` commands to help navigate a DB

## `\?` - Get Help

```
postgres#  \?

General
  \bind [PARAM]...       set query parameters
  \copyright             show PostgreSQL usage and distribution terms
  \crosstabview [COLUMNS] execute query and display result in crosstab
  \errverbose            show most recent error message at maximum verbosity
  \g [(OPTIONS)] [FILE]  execute query (and send result to file or |pipe);
                         \g with no arguments is equivalent to a semicolon
  \gdesc                 describe result of query, without executing it
  \gexec                 execute query, then execute each value in its result
  \gset [PREFIX]         execute query and store result in psql variables
  \gx [(OPTIONS)] [FILE] as \g, but forces expanded output mode
  \q                     quit psql
  \watch [[i=]SEC] [c=N] execute query every SEC seconds, up to N times
  ....
```

## `\l` `\l+` - list of databases

```
postgres=# \l;

   Name    |   Owner    | Encoding | Locale Provider | Collate | Ctype | ICU Locale | ICU Rules |   Access privileges   
-----------+------------+----------+-----------------+---------+-------+------------+-----------+-----------------------
 my-db     | my_db_admin| UTF8     | libc            | C       | C     |            |           | 
 postgres  | postgres   | UTF8     | libc            | C       | C     |            |           | =Tc/postgres         +
           |            |          |                 |         |       |            |           | postgres=CTc/postgres+
           |            |          |                 |         |       |            |           | my_db_ddl=c/postgres  +
           |            |          |                 |         |       |            |           | my_db_dml=c/postgres
 template0 | postgres   | UTF8     | libc            | C       | C     |            |           | =c/postgres          +
           |            |          |                 |         |       |            |           | postgres=CTc/postgres
 template1 | postgres   | UTF8     | libc            | C       | C     |            |           | =c/postgres          +
           |            |          |                 |         |       |            |           | postgres=CTc/postgres
```

## `\c` - switch(connect) to a database

```
postgres=# \c my-db

You are now connected to database "my-db" as user "postgres".
```

## `\dn` - list schemas

```
postgres=# \dn

      List of schemas
  Name  |       Owner       
--------+-------------------
 scma   | postgres
 public | pg_database_owner
```

## `SET` - to switch to a schema

```
SET search_path TO scma

SET
```

## `\dt` - to list tables in a schema

```
postgres=# \dt

                         List of relations
 Schema |                  Name                   | Type  |  Owner  
--------+-----------------------------------------+-------+---------
 scma   | authentication_user                     | table | scma_ddl
 scma   | api_token                               | table | scma_ddl
 scma   | migrations                              | table | scma_ddl
(3 rows)

```

## Querying

```
postgres=# select uuid, email from authentication_user;
                 uuid                 |        email         
--------------------------------------+----------------------
 4c1839d6-63c3-4ba3-a60c-1aa557886d89 | mitch@the_cool_one.com
 979e4da9-7397-4347-a75b-f55987da2525 | will@the_cool_one.com
 803bf903-67dc-4b5f-91b9-845511e85e24 | abdul@the_sad_one.com
```
