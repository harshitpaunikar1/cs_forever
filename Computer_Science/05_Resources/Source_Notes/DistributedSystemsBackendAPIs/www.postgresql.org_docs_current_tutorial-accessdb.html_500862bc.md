Title: PostgreSQL: Documentation: 18: 1.4. Accessing a Database
Mapped Topic: Relational database foundations
Source URL: https://www.postgresql.org/docs/current/tutorial-accessdb.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:08:35+00:00
Mapped From CSE.md Section: Part 3: Month 7

# Content

February 26, 2026: [
PostgreSQL 18.3, 17.9, 16.13, 15.17, and 14.22 Released!
](https://www.postgresql.org/about/news/postgresql-183-179-1613-1517-and-1422-released-3246/)

Development Versions:
[devel](https://www.postgresql.org/docs/devel/tutorial-accessdb.html)

Once you have created a database, you can access it by:

-
Running the PostgreSQL interactive terminal program, called

*psql*, which allows you to interactively enter, edit, and execute SQL commands. -
Using an existing graphical frontend tool like pgAdmin or an office suite with ODBC or JDBC support to create and manipulate a database. These possibilities are not covered in this tutorial.

-
Writing a custom application, using one of the several available language bindings. These possibilities are discussed further in

[Part IV](https://www.postgresql.org/client-interfaces.html).

You probably want to start up `psql`

to try the examples in this tutorial. It can be activated for the `mydb`

database by typing the command:

`$`

`psql mydb`

If you do not supply the database name then it will default to your user account name. You already discovered this scheme in the previous section using `createdb`

.

In `psql`

, you will be greeted with the following message:

psql (18.3) Type "help" for help. mydb=>

mydb=#

That would mean you are a database superuser, which is most likely the case if you installed the PostgreSQL instance yourself. Being a superuser means that you are not subject to access controls. For the purposes of this tutorial that is not important.

If you encounter problems starting `psql`

then go back to the previous section. The diagnostics of `createdb`

and `psql`

are similar, and if the former worked the latter should work as well.

The last line printed out by `psql`

is the prompt, and it indicates that `psql`

is listening to you and that you can type SQL queries into a work space maintained by `psql`

. Try out these commands:

`mydb=>`

version ------------------------------------------------------------------------------------------ PostgreSQL 18.3 on x86_64-pc-linux-gnu, compiled by gcc (Debian 4.9.2-10) 4.9.2, 64-bit (1 row)`SELECT version();`

`mydb=>`

date ------------ 2016-01-07 (1 row)`SELECT current_date;`

`mydb=>`

?column? ---------- 4 (1 row)`SELECT 2 + 2;`

The `psql`

program has a number of internal commands that are not SQL commands. They begin with the backslash character, “`\`

”. For example, you can get help on the syntax of various PostgreSQL SQL commands by typing:

`mydb=>`

`\h`

To get out of `psql`

, type:

`mydb=>`

`\q`

and `psql`

will quit and return you to your command shell. (For more internal commands, type `\?`

at the `psql`

prompt.) The full capabilities of `psql`

are documented in [psql](https://www.postgresql.org/app-psql.html). In this tutorial we will not use these features explicitly, but you can use them yourself when it is helpful.

[this form](https://www.postgresql.org/account/comments/new/18/tutorial-accessdb.html/)
to report a documentation issue.
