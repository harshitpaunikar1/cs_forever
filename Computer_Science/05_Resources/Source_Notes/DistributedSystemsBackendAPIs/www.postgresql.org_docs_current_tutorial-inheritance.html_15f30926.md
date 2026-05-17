Title: PostgreSQL: Documentation: 18: 3.6. Inheritance
Mapped Topic: Relational database foundations
Source URL: https://www.postgresql.org/docs/current/tutorial-inheritance.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:08:42+00:00
Mapped From CSE.md Section: Part 3: Month 7

# Content

February 26, 2026: [
PostgreSQL 18.3, 17.9, 16.13, 15.17, and 14.22 Released!
](https://www.postgresql.org/about/news/postgresql-183-179-1613-1517-and-1422-released-3246/)

Development Versions:
[devel](https://www.postgresql.org/docs/devel/tutorial-inheritance.html)

Inheritance is a concept from object-oriented databases. It opens up interesting new possibilities of database design.

Let's create two tables: A table `cities`

and a table `capitals`

. Naturally, capitals are also cities, so you want some way to show the capitals implicitly when you list all cities. If you're really clever you might invent some scheme like this:

CREATE TABLE capitals ( name text, population real, elevation int, -- (in ft) state char(2) ); CREATE TABLE non_capitals ( name text, population real, elevation int -- (in ft) ); CREATE VIEW cities AS SELECT name, population, elevation FROM capitals UNION SELECT name, population, elevation FROM non_capitals;

This works OK as far as querying goes, but it gets ugly when you need to update several rows, for one thing.

A better solution is this:

CREATE TABLE cities ( name text, population real, elevation int -- (in ft) ); CREATE TABLE capitals ( state char(2) UNIQUE NOT NULL ) INHERITS (cities);

In this case, a row of `capitals`

*inherits* all columns (`name`

, `population`

, and `elevation`

) from its *parent*, `cities`

. The type of the column `name`

is `text`

, a native PostgreSQL type for variable length character strings. The `capitals`

table has an additional column, `state`

, which shows its state abbreviation. In PostgreSQL, a table can inherit from zero or more other tables.

For example, the following query finds the names of all cities, including state capitals, that are located at an elevation over 500 feet:

SELECT name, elevation FROM cities WHERE elevation > 500;

which returns:

name | elevation -----------+----------- Las Vegas | 2174 Mariposa | 1953 Madison | 845 (3 rows)

On the other hand, the following query finds all the cities that are not state capitals and are situated at an elevation over 500 feet:

SELECT name, elevation FROM ONLY cities WHERE elevation > 500;

name | elevation -----------+----------- Las Vegas | 2174 Mariposa | 1953 (2 rows)

Here the `ONLY`

before `cities`

indicates that the query should be run over only the `cities`

table, and not tables below `cities`

in the inheritance hierarchy. Many of the commands that we have already discussed — `SELECT`

, `UPDATE`

, and `DELETE`

— support this `ONLY`

notation.

Although inheritance is frequently useful, it has not been integrated with unique constraints or foreign keys, which limits its usefulness. See [Section 5.11](https://www.postgresql.org/ddl-inherit.html) for more detail.

[this form](https://www.postgresql.org/account/comments/new/18/tutorial-inheritance.html/)
to report a documentation issue.
