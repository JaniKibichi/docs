---
title: SHOW TABLES
summary: The SHOW TABLES statement lists the tables in a schema or database.
keywords: reflection
toc: false
---

The `SHOW TABLES` [statement](sql-statements.html) lists the tables or [views](views.html) in a schema or database.

{{site.data.alerts.callout_info}}While a table or view is being <a href="drop-table.html">dropped</a>, <code>SHOW TABLES</code> will list the object with a <code>(dropped)</code> suffix.{{site.data.alerts.end}}

<div id="toc"></div>

## Synopsis

<div>
{% include sql/{{ page.version.version }}/diagrams/show_tables.html %}
</div>

## Required privileges

No [privileges](privileges.html) are required to list the tables in a schema or database.

## Parameters

Parameter | Description
----------|------------
`name` | The name of the schema or database for which to show tables. When omitted, the tables of the [current schema](sql-name-resolution.html#current-schema) in the [current database](sql-name-resolution.html#current-database) are listed.

`SHOW TABLES` will attempt to find a schema with the specified name first. If that fails, it will try to find a database with that name instead, and list the tables of its `public` schema. For more details, see [Name Resolution](sql-name-resolution.html).

## Examples

These example assumes that the `bank` database has been set as the current database for the session, either via the [`SET`](set-vars.html) statement or in the client's connection string.

### Show tables in the current database

{% include copy-clipboard.html %}
~~~ sql
> SHOW TABLES;
~~~

~~~
+---------------+
|     Table     |
+---------------+
| accounts      |
| user_accounts |
+---------------+
(2 rows)
~~~

This uses the [current schema](sql-name-resolution.html#current-schema) `public` set by default in `search_path`.

### Show tables in a different schema

{% include copy-clipboard.html %}
~~~ sql
> SHOW TABLES FROM information_schema;
~~~

{% include copy-clipboard.html %}
~~~ sql
> SHOW TABLES FROM bank.information_schema; -- also possible
~~~

~~~
+-----------------------------------+
|               Table               |
+-----------------------------------+
| administrable_role_authorizations |
| applicable_roles                  |
| column_privileges                 |
| columns                           |
| constraint_column_usage           |
| enabled_roles                     |
| key_column_usage                  |
| referential_constraints           |
| role_table_grants                 |
| schema_privileges                 |
| schemata                          |
| sequences                         |
| statistics                        |
| table_constraints                 |
| table_privileges                  |
| tables                            |
| user_privileges                   |
| views                             |
+-----------------------------------+
(18 rows)
~~~

### Show tables in a different database

{% include copy-clipboard.html %}
~~~ sql
> SHOW TABLES FROM startrek.public;
~~~

{% include copy-clipboard.html %}
~~~ sql
> SHOW TABLES FROM startrek; -- also possible
~~~

~~~
+-------------------+
|       Table       |
+-------------------+
| episodes          |
| quotes            |
| quotes_per_season |
+-------------------+
(3 rows)
~~~

## See also

- [`SHOW DATABASES`](show-databases.html)
- [`SHOW SCHEMAS`](show-schemas.html)
- [`CREATE TABLE`](create-table.html)
- [`CREATE VIEW`](create-view.html)
- [Information Schema](information-schema.html)
