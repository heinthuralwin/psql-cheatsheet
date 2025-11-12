PostgreSQL (psql) Essentials

Connecting to Postgres
=> psql -U postgres

Connect to Postgres CLI as the postgres user
=> psql -U postgres -d mydatabase

Common Meta Commands (\ commands)
| Command                                               | Description                                  |
| ----------------------------------------------------- | -------------------------------------------- |
| `\?`                                                  | Show all available psql commands             |
| `\q`                                                  | Quit/exit psql                               |
| `\c dbname`                                           | Connect/switch to another database           |
| `\l`                                                  | List all databases                           |
| `\dt`                                                 | List all tables in current schema            |
| `\dt *.*`                                             | List all tables in all schemas               |
| `\d tablename`                                        | Show table definition (columns, constraints) |
| `\d+ tablename`                                       | Same as above + size and description         |
| `\du`                                                 | List all users/roles                         |
| `\df`                                                 | List all functions                           |
| `\di`                                                 | List all indexes                             |
| `\dn`                                                 | List all schemas                             |
| `\dx`                                                 | Show installed extensions                    |
| `\x`                                                  | Toggle expanded (pretty) output format       |
| `\copy (SELECT * FROM table) TO 'file.csv' WITH CSV;` | Export table data to a CSV file   


User Management
| Command                                                | Description                                    |
| ------------------------------------------------------ | ---------------------------------------------- |
| `\du username`                                         | Show details of a specific user                |
| `CREATE ROLE username LOGIN PASSWORD 'pass';`          | Create a user with login                       |
| `CREATE DATABASE dbname OWNER username;`               | Create a database owned by that user           |
| `GRANT ALL PRIVILEGES ON DATABASE dbname TO username;` | Give full access to a database                 |
| `DROP ROLE username;`                                  | Delete user role                               |
| `SET ROLE username;`                                   | Switch current role (impersonate another user) |


Database Management
| Command                   | Description                                         |
| ------------------------- | --------------------------------------------------- |
| `CREATE DATABASE dbname;` | Create a new database                               |
| `DROP DATABASE dbname;`   | Delete a database                                   |
| `\l+`                     | List databases with extra info (owner, size, etc.)  |
| `\conninfo`               | Show current connection info (user, db, host, port) |


Table Management
| Command                         | Description             |
| ------------------------------- | ----------------------- |
| `CREATE TABLE tablename (...);` | Create new table        |
| `DROP TABLE tablename;`         | Delete a table          |
| `\d tablename`                  | Show structure of table |
| `SELECT * FROM tablename;`      | Show all data           |
| `TRUNCATE tablename;`           | Delete all rows (fast)  |


Monitoring & Diagnostics
| Command                                                                          | Description                                      |
| -------------------------------------------------------------------------------- | ------------------------------------------------ |
| `\watch 2`                                                                       | Re-run last command every 2 seconds (live view)  |
| `SELECT * FROM pg_stat_activity;`                                                | Show all active connections/queries              |
| `SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE datname='dbname';` | Kill all connections to a database               |
| `SELECT pg_size_pretty(pg_database_size('dbname'));`                             | Show DB size in human-readable format            |
| `SELECT pg_size_pretty(pg_total_relation_size('tablename'));`                    | Show table size                                  |
| `SELECT * FROM pg_indexes WHERE tablename='tablename';`                          | List indexes on a table                          |
| `EXPLAIN query;`                                                                 | Show query plan (how PostgreSQL will execute it) |
| `EXPLAIN ANALYZE query;`                                                         | Run + show query performance analysis            |


Server Control (Linux)
| Command                           | Description        |
| --------------------------------- | ------------------ |
| `sudo service postgresql start`   | Start PostgreSQL   |
| `sudo service postgresql stop`    | Stop PostgreSQL    |
| `sudo service postgresql restart` | Restart PostgreSQL |


Handy Queries
| Query                         | Description                |
| ----------------------------- | -------------------------- |
| `SELECT current_database();`  | Show current database name |
| `SELECT now();`               | Show current time          |
| `SELECT version();`           | Show PostgreSQL version    |
| `SHOW statement_timeout;`     | Show query timeout setting |
| `SELECT * FROM pg_extension;` | Show installed extensions  |
| `SELECT inet_server_addr();`  | Show server IP address     |


Useful Tools
| Tool               | Description                                              |
| ------------------ | -------------------------------------------------------- |
| `pg_top` or `ptop` | Like Linux `top` but for PostgreSQL processes            |
| `pg_activity`      | Live monitoring of database activity                     |
| `pgAdmin`          | GUI tool to manage databases easily                      |
| `.pgpass` file     | Store credentials (`chmod 600 ~/.pgpass`) for auto-login |
