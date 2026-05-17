Title: PostgreSQL: Documentation: 18: 3.3. Foreign Keys
Mapped Topic: Relational database foundations
Source URL: https://www.postgresql.org/docs/current/tutorial-fk.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:08:41+00:00
Mapped From CSE.md Section: Part 3: Month 7

# Content

February 26, 2026: [
PostgreSQL 18.3, 17.9, 16.13, 15.17, and 14.22 Released!
](https://www.postgresql.org/about/news/postgresql-183-179-1613-1517-and-1422-released-3246/)

Development Versions:
[devel](https://www.postgresql.org/docs/devel/tutorial-fk.html)

Recall the `weather`

and `cities`

tables from [Chapter 2](https://www.postgresql.org/tutorial-sql.html). Consider the following problem: You want to make sure that no one can insert rows in the `weather`

table that do not have a matching entry in the `cities`

table. This is called maintaining the *referential integrity* of your data. In simplistic database systems this would be implemented (if at all) by first looking at the `cities`

table to check if a matching record exists, and then inserting or rejecting the new `weather`

records. This approach has a number of problems and is very inconvenient, so PostgreSQL can do this for you.

The new declaration of the tables would look like this:

CREATE TABLE cities ( name varchar(80) primary key, location point ); CREATE TABLE weather ( city varchar(80) references cities(name), temp_lo int, temp_hi int, prcp real, date date );

Now try inserting an invalid record:

INSERT INTO weather VALUES ('Berkeley', 45, 53, 0.0, '1994-11-28');

ERROR: insert or update on table "weather" violates foreign key constraint "weather_city_fkey" DETAIL: Key (city)=(Berkeley) is not present in table "cities".

The behavior of foreign keys can be finely tuned to your application. We will not go beyond this simple example in this tutorial, but just refer you to [Chapter 5](https://www.postgresql.org/ddl.html) for more information. Making correct use of foreign keys will definitely improve the quality of your database applications, so you are strongly encouraged to learn about them.

[this form](https://www.postgresql.org/account/comments/new/18/tutorial-fk.html/)
to report a documentation issue.
