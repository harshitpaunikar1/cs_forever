Title: An Asynchronous I/O Module For SQLite
Mapped Topic: Lightweight storage and SQL basics
Source URL: https://www.sqlite.org/asyncvfs.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:08:18+00:00
Mapped From CSE.md Section: Part 3: Month 7

# Content

**NOTE:**
[WAL mode](https://www.sqlite.org/wal.html) with [PRAGMA synchronous](https://www.sqlite.org/pragma.html#pragma_synchronous) set to NORMAL avoids calls to
fsync() during transaction commit and only invokes fsync() during
a [checkpoint](https://www.sqlite.org/wal.html#ckpt) operation. The use of [WAL mode](https://www.sqlite.org/wal.html) largely obviates the
need for this asynchronous I/O module. Hence, this module is no longer
supported. The source code continues to exist in the SQLite source tree,
but it is not a part of any standard build and is no longer maintained.
This documentation is retained for historical reference.

Normally, when SQLite writes to a database file, it waits until the write operation is finished before returning control to the calling application. Since writing to the file-system is usually very slow compared with CPU bound operations, this can be a performance bottleneck. The asynchronous I/O backend is an extension that causes SQLite to perform all write requests using a separate thread running in the background. Although this does not reduce the overall system resources (CPU, disk bandwidth etc.), it does allow SQLite to return control to the caller quickly even when writing to the database.

With asynchronous I/O, write requests are handled by a separate thread running in the background. This means that the thread that initiates a database write does not have to wait for (sometimes slow) disk I/O to occur. The write seems to happen very quickly, though in reality it is happening at its usual slow pace in the background.

Asynchronous I/O appears to give better responsiveness, but at a price. You lose the Durable property. With the default I/O backend of SQLite, once a write completes, you know that the information you wrote is safely on disk. With the asynchronous I/O, this is not the case. If your program crashes or if a power loss occurs after the database write but before the asynchronous write thread has completed, then the database change might never make it to disk and the next user of the database might not see your change.

You lose Durability with asynchronous I/O, but you still retain the other parts of ACID: Atomic, Consistent, and Isolated. Many applications get along fine without the Durability.

Asynchronous I/O works by creating an SQLite [VFS object](https://www.sqlite.org/c3ref/vfs.html)
and registering it with [sqlite3_vfs_register()](https://www.sqlite.org/c3ref/vfs_find.html).
When files opened via
this VFS are written to (using the vfs xWrite() method), the data is not
written directly to disk, but is placed in the "write-queue" to be
handled by the background thread.

When files opened with the asynchronous VFS are read from (using the vfs xRead() method), the data is read from the file on disk and the write-queue, so that from the point of view of the vfs reader the xWrite() appears to have already completed.

The asynchronous I/O VFS is registered (and unregistered) by calls to the API functions sqlite3async_initialize() and sqlite3async_shutdown(). See section "Compilation and Usage" below for details.

In order to gain experience with the main ideas surrounding asynchronous IO, this implementation is deliberately kept simple. Additional capabilities may be added in the future.

For example, as currently implemented, if writes are happening at a steady stream that exceeds the I/O capability of the background writer thread, the queue of pending write operations will grow without bound. If this goes on for long enough, the host system could run out of memory. A more sophisticated module could to keep track of the quantity of pending writes and stop accepting new write requests when the queue of pending writes grows too large.

Multiple connections from within a single process that use this implementation of asynchronous IO may access a single database file concurrently. From the point of view of the user, if all connections are from within a single process, there is no difference between the concurrency offered by "normal" SQLite and SQLite using the asynchronous backend.

If file-locking is enabled (it is enabled by default), then connections from multiple processes may also read and write the database file. However concurrency is reduced as follows:

When a connection using asynchronous IO begins a database transaction, the database is locked immediately. However the lock is not released until after all relevant operations in the write-queue have been flushed to disk. This means (for example) that the database may remain locked for some time after a "

[COMMIT](https://www.sqlite.org/lang_transaction.html)" or "[ROLLBACK](https://www.sqlite.org/lang_transaction.html)" is issued.If an application using asynchronous IO executes transactions in quick succession, other database users may be effectively locked out of the database. This is because when a

[BEGIN](https://www.sqlite.org/lang_transaction.html)is executed, a database lock is established immediately. But when the corresponding COMMIT or ROLLBACK occurs, the lock is not released until the relevant part of the write-queue has been flushed through. As a result, if a COMMIT is followed by a BEGIN before the write-queue is flushed through, the database is never unlocked, preventing other processes from accessing the database.

File-locking may be disabled at runtime using the sqlite3async_control() API (see below). This may improve performance when on an NFS or other network file-system, as the synchronous round-trips to the server required to establish file locks are avoided. However, if multiple connections attempt to access the same database file when file-locking is disabled, application crashes and database corruption is a likely outcome.

The asynchronous IO extension consists of a single file of C code
(sqlite3async.c), and a header file (sqlite3async.h), located in the
[
ext/async/ subfolder](https://sqlite.org/src/dir?name=ext/async) of the SQLite source tree, that defines the
C API used by applications to activate and control the modules
functionality.

To use the asynchronous IO extension, compile sqlite3async.c as part of the application that uses SQLite. Then use the APIs defined in sqlite3async.h to initialize and configure the module.

The asynchronous IO VFS API is described in detail in comments in sqlite3async.h. Using the API usually consists of the following steps:

Register the asynchronous IO VFS with SQLite by calling the sqlite3async_initialize() function.

Create a background thread to perform write operations and call sqlite3async_run().

Use the normal SQLite API to read and write to databases via the asynchronous IO VFS.

Refer to comments in the
[
sqlite3async.h header file](https://sqlite.org/src/finfo?name=ext/async/sqlite3async.h) for details.

Currently the asynchronous IO extension is compatible with win32 systems and systems that support the pthreads interface, including Mac OS X, Linux, and other varieties of Unix.

To port the asynchronous IO extension to another platform, the user must implement mutex and condition variable primitives for the new platform. Currently there is no externally available interface to allow this, but modifying the code within sqlite3async.c to include the new platforms concurrency primitives is relatively easy. Search within sqlite3async.c for the comment string "PORTING FUNCTIONS" for details. Then implement new versions of each of the following:

static void async_mutex_enter(int eMutex); static void async_mutex_leave(int eMutex); static void async_cond_wait(int eCond, int eMutex); static void async_cond_signal(int eCond); static void async_sched_yield(void);

The functionality required of each of the above functions is described in comments in sqlite3async.c.

*This page was last updated on 2025-05-31 13:08:22Z *
