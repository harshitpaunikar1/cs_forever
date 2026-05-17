Title: Introduction
Mapped Topic: Lightweight storage and SQL basics
Source URL: https://www.sqlite.org/c3ref/intro.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:08:26+00:00
Mapped From CSE.md Section: Part 3: Month 7

# Content

These pages are intended to be a precise and detailed specification. For a tutorial introduction, see instead:

This same content is also available as aThe SQLite interface elements can be grouped into three categories:

This is a list of all abstract objects and datatypes used by the SQLite library. There are couple dozen objects in total, but the two most important objects are: A database connection object**List Of Objects.**[sqlite3](https://www.sqlite.org/c3ref/sqlite3.html), and the prepared statement object[sqlite3_stmt](https://www.sqlite.org/c3ref/stmt.html).This is a list of numeric constants used by SQLite and represented by #defines in the sqlite3.h header file. These constants are things such as numeric**List Of Constants.**[result codes](https://www.sqlite.org/rescode.html)from various interfaces (ex:[SQLITE_OK](https://www.sqlite.org/rescode.html#ok)) or flags passed into functions to control behavior (ex:[SQLITE_OPEN_READONLY](https://www.sqlite.org/c3ref/c_open_autoproxy.html)).This is a list of all functions and methods operating on the**List Of Functions.**[objects](https://www.sqlite.org/c3ref/objlist.html)and using and/or returning[constants](https://www.sqlite.org/c3ref/constlist.html). There are many functions, but most applications only use a handful.
