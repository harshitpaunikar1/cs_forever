Title: PostgreSQL: Documentation: 18: 2.7. Aggregate Functions
Mapped Topic: Relational database foundations
Source URL: https://www.postgresql.org/docs/current/tutorial-agg.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:08:37+00:00
Mapped From CSE.md Section: Part 3: Month 7

# Content

February 26, 2026: [
PostgreSQL 18.3, 17.9, 16.13, 15.17, and 14.22 Released!
](https://www.postgresql.org/about/news/postgresql-183-179-1613-1517-and-1422-released-3246/)

Development Versions:
[devel](https://www.postgresql.org/docs/devel/tutorial-agg.html)

Like most other relational database products, PostgreSQL supports *aggregate functions*. An aggregate function computes a single result from multiple input rows. For example, there are aggregates to compute the `count`

, `sum`

, `avg`

(average), `max`

(maximum) and `min`

(minimum) over a set of rows.

As an example, we can find the highest low-temperature reading anywhere with:

SELECT max(temp_lo) FROM weather;

max ----- 46 (1 row)

[ If we wanted to know what city (or cities) that reading occurred in, we might try:]

SELECT city FROM weather WHERE temp_lo = max(temp_lo);-- WRONG

but this will not work since the aggregate `max`

cannot be used in the `WHERE`

clause. (This restriction exists because the `WHERE`

clause determines which rows will be included in the aggregate calculation; so obviously it has to be evaluated before aggregate functions are computed.) However, as is often the case the query can be restated to accomplish the desired result, here by using a *subquery*:

SELECT city FROM weather WHERE temp_lo = (SELECT max(temp_lo) FROM weather);

city --------------- San Francisco (1 row)

This is OK because the subquery is an independent computation that computes its own aggregate separately from what is happening in the outer query.

[ ][ Aggregates are also very useful in combination with ]`GROUP BY`

clauses. For example, we can get the number of readings and the maximum low temperature observed in each city with:

SELECT city, count(*), max(temp_lo) FROM weather GROUP BY city;

city | count | max ---------------+-------+----- Hayward | 1 | 37 San Francisco | 2 | 46 (2 rows)

which gives us one output row per city. Each aggregate result is computed over the table rows matching that city. We can filter these grouped rows using `HAVING`

:

SELECT city, count(*), max(temp_lo) FROM weather GROUP BY city HAVING max(temp_lo) < 40;

city | count | max ---------+-------+----- Hayward | 1 | 37 (1 row)

which gives us the same results for only the cities that have all `temp_lo`

values below 40. Finally, if we only care about cities whose names begin with “`S`

”, we might do:

SELECT city, count(*), max(temp_lo) FROM weather WHERE city LIKE 'S%' -- (1) GROUP BY city;

city | count | max ---------------+-------+----- San Francisco | 2 | 46 (1 row)

|
The |

It is important to understand the interaction between aggregates and SQL's `WHERE`

and `HAVING`

clauses. The fundamental difference between `WHERE`

and `HAVING`

is this: `WHERE`

selects input rows before groups and aggregates are computed (thus, it controls which rows go into the aggregate computation), whereas `HAVING`

selects group rows after groups and aggregates are computed. Thus, the `WHERE`

clause must not contain aggregate functions; it makes no sense to try to use an aggregate to determine which rows will be inputs to the aggregates. On the other hand, the `HAVING`

clause always contains aggregate functions. (Strictly speaking, you are allowed to write a `HAVING`

clause that doesn't use aggregates, but it's seldom useful. The same condition could be used more efficiently at the `WHERE`

stage.)

In the previous example, we can apply the city name restriction in `WHERE`

, since it needs no aggregate. This is more efficient than adding the restriction to `HAVING`

, because we avoid doing the grouping and aggregate calculations for all rows that fail the `WHERE`

check.

Another way to select the rows that go into an aggregate computation is to use `FILTER`

, which is a per-aggregate option:

SELECT city, count(*) FILTER (WHERE temp_lo < 45), max(temp_lo) FROM weather GROUP BY city;

city | count | max ---------------+-------+----- Hayward | 1 | 37 San Francisco | 1 | 46 (2 rows)

`FILTER`

is much like `WHERE`

, except that it removes rows only from the input of the particular aggregate function that it is attached to. Here, the `count`

aggregate counts only rows with `temp_lo`

below 45; but the `max`

aggregate is still applied to all rows, so it still finds the reading of 46.

[this form](https://www.postgresql.org/account/comments/new/18/tutorial-agg.html/)
to report a documentation issue.
