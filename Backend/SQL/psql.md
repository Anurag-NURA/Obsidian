
Connect to any database
```bash
psql <DATABASE_NAME>
```

example:
```bash
psql tourismDB
```

make a database as default database to access through psql
```bash
export PGDATABASE=tourismDB
```

and then just type this in shelll
```bash
psql
```

list all the databases 
```psql
\l
```

which is equivalent to
```psql
SELECT * FROM pg_database;
```

Connect to a database 
```psql
\c <DATABASE_NAME>
```

list all the tables in the database
```psql
\dt
```
**If shown an error, "Did not find any relations."**
```psql
show search_path;

set search_path=public;
```

To see details (columns) of a table
```psql
\d+ <TABLE_NAME>
```

To see any **View** inside the table
```psql
\dv
```

TO see any **Schemas** present in the table
```
\dn
```

**Create** a Database
```psql
CREATE DATABASE <NEW_DATABASE_NAME>;
```

**Drop** a database
```psql
DROP DATABASE <DATABASE_NAME>;
```

**Create** a User
```psql
CREATE USER <USER_NAME> WITH PASSWORD <PASSWORD>;
```

**Drop** a user
```psql
DROP USER <USER_NAME>;
```

List all users 
```psql
\du
```

Connect as another PostgreSQL user:
```bash
psql -U username -d database_name
```
If already inside `psql`, reconnect using:
```psql
\c database_name username
```