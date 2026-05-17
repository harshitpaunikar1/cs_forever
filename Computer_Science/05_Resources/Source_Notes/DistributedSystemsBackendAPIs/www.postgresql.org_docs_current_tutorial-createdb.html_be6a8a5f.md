Title: PostgreSQL: Documentation: 18: 1.3. Creating a Database
Mapped Topic: Relational database foundations
Source URL: https://www.postgresql.org/docs/current/tutorial-createdb.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:08:40+00:00
Mapped From CSE.md Section: Part 3: Month 7

# Content

February 26, 2026: [
PostgreSQL 18.3, 17.9, 16.13, 15.17, and 14.22 Released!
](https://www.postgresql.org/about/news/postgresql-183-179-1613-1517-and-1422-released-3246/)

Development Versions:
[devel](https://www.postgresql.org/docs/devel/tutorial-createdb.html)

The first test to see whether you can access the database server is to try to create a database. A running PostgreSQL server can manage many databases. Typically, a separate database is used for each project or for each user.

Possibly, your site administrator has already created a database for your use. In that case you can omit this step and skip ahead to the next section.

To create a new database from the command line, in this example named `mydb`

, you use the following command:

`$`

`createdb mydb`

If this produces no response then this step was successful and you can skip over the remainder of this section.

If you see a message similar to:

createdb: command not found

then PostgreSQL was not installed properly. Either it was not installed at all or your shell's search path was not set to include it. Try calling the command with an absolute path instead:

`$`

`/usr/local/pgsql/bin/createdb mydb`

The path at your site might be different. Contact your site administrator or check the installation instructions to correct the situation.

Another response could be this:

createdb: error: connection to server on socket "/tmp/.s.PGSQL.5432" failed: No such file or directory Is the server running locally and accepting connections on that socket?

This means that the server was not started, or it is not listening where `createdb`

expects to contact it. Again, check the installation instructions or consult the administrator.

Another response could be this:

createdb: error: connection to server on socket "/tmp/.s.PGSQL.5432" failed: FATAL: role "joe" does not exist

where your own login name is mentioned. This will happen if the administrator has not created a PostgreSQL user account for you. (PostgreSQL user accounts are distinct from operating system user accounts.) If you are the administrator, see [Chapter 21](https://www.postgresql.org/user-manag.html) for help creating accounts. You will need to become the operating system user under which PostgreSQL was installed (usually `postgres`

) to create the first user account. It could also be that you were assigned a PostgreSQL user name that is different from your operating system user name; in that case you need to use the `-U`

switch or set the `PGUSER`

environment variable to specify your PostgreSQL user name.

If you have a user account but it does not have the privileges required to create a database, you will see the following:

createdb: error: database creation failed: ERROR: permission denied to create database

Not every user has authorization to create new databases. If PostgreSQL refuses to create databases for you then the site administrator needs to grant you permission to create databases. Consult your site administrator if this occurs. If you installed PostgreSQL yourself then you should log in for the purposes of this tutorial under the user account that you started the server as. [1]

You can also create databases with other names. PostgreSQL allows you to create any number of databases at a given site. Database names must have an alphabetic first character and are limited to 63 bytes in length. A convenient choice is to create a database with the same name as your current user name. Many tools assume that database name as the default, so it can save you some typing. To create that database, simply type:

`$`

`createdb`

If you do not want to use your database anymore you can remove it. For example, if you are the owner (creator) of the database `mydb`

, you can destroy it using the following command:

`$`

`dropdb mydb`

(For this command, the database name does not default to the user account name. You always need to specify it.) This action physically removes all files associated with the database and cannot be undone, so this should only be done with a great deal of forethought.

More about `createdb`

and `dropdb`

can be found in [createdb](https://www.postgresql.org/app-createdb.html) and [dropdb](https://www.postgresql.org/app-dropdb.html) respectively.

[ [1]](https://www.postgresql.org#id-1.4.3.4.10.4) As an explanation for why this works: PostgreSQL user names are separate from operating system user accounts. When you connect to a database, you can choose what PostgreSQL user name to connect as; if you don't, it will default to the same name as your current operating system account. As it happens, there will always be a PostgreSQL user account that has the same name as the operating system user that started the server, and it also happens that that user always has permission to create databases. Instead of logging in as that user you can also specify the

`-U`

option everywhere to select a PostgreSQL user name to connect as.[this form](https://www.postgresql.org/account/comments/new/18/tutorial-createdb.html/)
to report a documentation issue.
