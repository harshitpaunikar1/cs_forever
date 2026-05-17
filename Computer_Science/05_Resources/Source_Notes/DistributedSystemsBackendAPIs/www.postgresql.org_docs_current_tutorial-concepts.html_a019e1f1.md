Title: PostgreSQL: Documentation: 18: 2.2. Concepts
Mapped Topic: Relational database foundations
Source URL: https://www.postgresql.org/docs/current/tutorial-concepts.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:08:39+00:00
Mapped From CSE.md Section: Part 3: Month 7

# Content

February 26, 2026: [
PostgreSQL 18.3, 17.9, 16.13, 15.17, and 14.22 Released!
](https://www.postgresql.org/about/news/postgresql-183-179-1613-1517-and-1422-released-3246/)

Development Versions:
[devel](https://www.postgresql.org/docs/devel/tutorial-concepts.html)

[ ][ ][ ][ ][ PostgreSQL is a ]*relational database management system* (RDBMS). That means it is a system for managing data stored in *relations*. Relation is essentially a mathematical term for *table*. The notion of storing data in tables is so commonplace today that it might seem inherently obvious, but there are a number of other ways of organizing databases. Files and directories on Unix-like operating systems form an example of a hierarchical database. A more modern development is the object-oriented database.

[ ][ Each table is a named collection of ]*rows*. Each row of a given table has the same set of named *columns*, and each column is of a specific data type. Whereas columns have a fixed order in each row, it is important to remember that SQL does not guarantee the order of the rows within the table in any way (although they can be explicitly sorted for display).

[ ][ Tables are grouped into databases, and a collection of databases managed by a single PostgreSQL server instance constitutes a database ]*cluster*.

[this form](https://www.postgresql.org/account/comments/new/18/tutorial-concepts.html/)
to report a documentation issue.
