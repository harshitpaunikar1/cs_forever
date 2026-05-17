Title: PostgreSQL: Documentation: 18: Part II. The SQL Language
Mapped Topic: Relational database foundations
Source URL: https://www.postgresql.org/docs/current/sql.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:08:35+00:00
Mapped From CSE.md Section: Part 3: Month 7

# Content

February 26, 2026: [
PostgreSQL 18.3, 17.9, 16.13, 15.17, and 14.22 Released!
](https://www.postgresql.org/about/news/postgresql-183-179-1613-1517-and-1422-released-3246/)

Development Versions:
[devel](https://www.postgresql.org/docs/devel/sql.html)

This part describes the use of the SQL language in PostgreSQL. We start with describing the general syntax of SQL, then how to create tables, how to populate the database, and how to query it. The middle part lists the available data types and functions for use in SQL commands. Lastly, we address several aspects of importance for tuning a database.

The information is arranged so that a novice user can follow it from start to end and gain a full understanding of the topics without having to refer forward too many times. The chapters are intended to be self-contained, so that advanced users can read the chapters individually as they choose. The information is presented in narrative form with topical units. Readers looking for a complete description of a particular command are encouraged to review the [Part VI](https://www.postgresql.org/reference.html).

Readers should know how to connect to a PostgreSQL database and issue SQL commands. Readers that are unfamiliar with these issues are encouraged to read [Part I](https://www.postgresql.org/tutorial.html) first. SQL commands are typically entered using the PostgreSQL interactive terminal psql, but other programs that have similar functionality can be used as well.

**Table of Contents**

[4. SQL Syntax](https://www.postgresql.org/sql-syntax.html)[5. Data Definition](https://www.postgresql.org/ddl.html)-
[5.1. Table Basics](https://www.postgresql.org/ddl-basics.html)[5.2. Default Values](https://www.postgresql.org/ddl-default.html)[5.3. Identity Columns](https://www.postgresql.org/ddl-identity-columns.html)[5.4. Generated Columns](https://www.postgresql.org/ddl-generated-columns.html)[5.5. Constraints](https://www.postgresql.org/ddl-constraints.html)[5.6. System Columns](https://www.postgresql.org/ddl-system-columns.html)[5.7. Modifying Tables](https://www.postgresql.org/ddl-alter.html)[5.8. Privileges](https://www.postgresql.org/ddl-priv.html)[5.9. Row Security Policies](https://www.postgresql.org/ddl-rowsecurity.html)[5.10. Schemas](https://www.postgresql.org/ddl-schemas.html)[5.11. Inheritance](https://www.postgresql.org/ddl-inherit.html)[5.12. Table Partitioning](https://www.postgresql.org/ddl-partitioning.html)[5.13. Foreign Data](https://www.postgresql.org/ddl-foreign-data.html)[5.14. Other Database Objects](https://www.postgresql.org/ddl-others.html)[5.15. Dependency Tracking](https://www.postgresql.org/ddl-depend.html)

[6. Data Manipulation](https://www.postgresql.org/dml.html)[7. Queries](https://www.postgresql.org/queries.html)[8. Data Types](https://www.postgresql.org/datatype.html)-
[8.1. Numeric Types](https://www.postgresql.org/datatype-numeric.html)[8.2. Monetary Types](https://www.postgresql.org/datatype-money.html)[8.3. Character Types](https://www.postgresql.org/datatype-character.html)[8.4. Binary Data Types](https://www.postgresql.org/datatype-binary.html)[8.5. Date/Time Types](https://www.postgresql.org/datatype-datetime.html)[8.6. Boolean Type](https://www.postgresql.org/datatype-boolean.html)[8.7. Enumerated Types](https://www.postgresql.org/datatype-enum.html)[8.8. Geometric Types](https://www.postgresql.org/datatype-geometric.html)[8.9. Network Address Types](https://www.postgresql.org/datatype-net-types.html)[8.10. Bit String Types](https://www.postgresql.org/datatype-bit.html)[8.11. Text Search Types](https://www.postgresql.org/datatype-textsearch.html)[8.12. UUID Type](https://www.postgresql.org/datatype-uuid.html)[8.13. XML Type](https://www.postgresql.org/datatype-xml.html)[8.14. JSON Types](https://www.postgresql.org/datatype-json.html)[8.15. Arrays](https://www.postgresql.org/arrays.html)[8.16. Composite Types](https://www.postgresql.org/rowtypes.html)[8.17. Range Types](https://www.postgresql.org/rangetypes.html)[8.18. Domain Types](https://www.postgresql.org/domains.html)[8.19. Object Identifier Types](https://www.postgresql.org/datatype-oid.html)[8.20.](https://www.postgresql.org/datatype-pg-lsn.html)`pg_lsn`

Type[8.21. Pseudo-Types](https://www.postgresql.org/datatype-pseudo.html)

[9. Functions and Operators](https://www.postgresql.org/functions.html)-
[9.1. Logical Operators](https://www.postgresql.org/functions-logical.html)[9.2. Comparison Functions and Operators](https://www.postgresql.org/functions-comparison.html)[9.3. Mathematical Functions and Operators](https://www.postgresql.org/functions-math.html)[9.4. String Functions and Operators](https://www.postgresql.org/functions-string.html)[9.5. Binary String Functions and Operators](https://www.postgresql.org/functions-binarystring.html)[9.6. Bit String Functions and Operators](https://www.postgresql.org/functions-bitstring.html)[9.7. Pattern Matching](https://www.postgresql.org/functions-matching.html)[9.8. Data Type Formatting Functions](https://www.postgresql.org/functions-formatting.html)[9.9. Date/Time Functions and Operators](https://www.postgresql.org/functions-datetime.html)[9.10. Enum Support Functions](https://www.postgresql.org/functions-enum.html)[9.11. Geometric Functions and Operators](https://www.postgresql.org/functions-geometry.html)[9.12. Network Address Functions and Operators](https://www.postgresql.org/functions-net.html)[9.13. Text Search Functions and Operators](https://www.postgresql.org/functions-textsearch.html)[9.14. UUID Functions](https://www.postgresql.org/functions-uuid.html)[9.15. XML Functions](https://www.postgresql.org/functions-xml.html)[9.16. JSON Functions and Operators](https://www.postgresql.org/functions-json.html)[9.17. Sequence Manipulation Functions](https://www.postgresql.org/functions-sequence.html)[9.18. Conditional Expressions](https://www.postgresql.org/functions-conditional.html)[9.19. Array Functions and Operators](https://www.postgresql.org/functions-array.html)[9.20. Range/Multirange Functions and Operators](https://www.postgresql.org/functions-range.html)[9.21. Aggregate Functions](https://www.postgresql.org/functions-aggregate.html)[9.22. Window Functions](https://www.postgresql.org/functions-window.html)[9.23. Merge Support Functions](https://www.postgresql.org/functions-merge-support.html)[9.24. Subquery Expressions](https://www.postgresql.org/functions-subquery.html)[9.25. Row and Array Comparisons](https://www.postgresql.org/functions-comparisons.html)[9.26. Set Returning Functions](https://www.postgresql.org/functions-srf.html)[9.27. System Information Functions and Operators](https://www.postgresql.org/functions-info.html)[9.28. System Administration Functions](https://www.postgresql.org/functions-admin.html)[9.29. Trigger Functions](https://www.postgresql.org/functions-trigger.html)[9.30. Event Trigger Functions](https://www.postgresql.org/functions-event-triggers.html)[9.31. Statistics Information Functions](https://www.postgresql.org/functions-statistics.html)

[10. Type Conversion](https://www.postgresql.org/typeconv.html)[11. Indexes](https://www.postgresql.org/indexes.html)-
[11.1. Introduction](https://www.postgresql.org/indexes-intro.html)[11.2. Index Types](https://www.postgresql.org/indexes-types.html)[11.3. Multicolumn Indexes](https://www.postgresql.org/indexes-multicolumn.html)[11.4. Indexes and](https://www.postgresql.org/indexes-ordering.html)`ORDER BY`

[11.5. Combining Multiple Indexes](https://www.postgresql.org/indexes-bitmap-scans.html)[11.6. Unique Indexes](https://www.postgresql.org/indexes-unique.html)[11.7. Indexes on Expressions](https://www.postgresql.org/indexes-expressional.html)[11.8. Partial Indexes](https://www.postgresql.org/indexes-partial.html)[11.9. Index-Only Scans and Covering Indexes](https://www.postgresql.org/indexes-index-only-scans.html)[11.10. Operator Classes and Operator Families](https://www.postgresql.org/indexes-opclass.html)[11.11. Indexes and Collations](https://www.postgresql.org/indexes-collations.html)[11.12. Examining Index Usage](https://www.postgresql.org/indexes-examine.html)

[12. Full Text Search](https://www.postgresql.org/textsearch.html)[13. Concurrency Control](https://www.postgresql.org/mvcc.html)[14. Performance Tips](https://www.postgresql.org/performance-tips.html)[15. Parallel Query](https://www.postgresql.org/parallel-query.html)

[this form](https://www.postgresql.org/account/comments/new/18/sql.html/)
to report a documentation issue.
