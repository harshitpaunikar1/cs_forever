Title: SQLite Changes From Version 3.4.2 To 3.5.0
Mapped Topic: Lightweight storage and SQL basics
Source URL: https://www.sqlite.org/34to35.html
Source Type: official_docs
Trust Score: 96
Fetched At: 2026-04-17T07:08:13+00:00
Mapped From CSE.md Section: Part 3: Month 7

# Content

SQLite version 3.5.0 (2007-09-04) introduces a new OS interface layer that is incompatible with all prior versions of SQLite. In addition, a few existing interfaces have been generalized to work across all database connections within a process rather than just all connections within a thread. The purpose of this article is to describe the changes to 3.5.0 in detail so that users of prior versions of SQLite can judge what, if any, effort will be required to upgrade to newer versions.

A quick enumeration of the changes in SQLite version 3.5.0 is provided here. Subsequent sections will describe these changes in more detail.

- The OS interface layer has been completely reworked:
- The undocumented
**sqlite3_os_switch()**interface has been removed. - The
**SQLITE_ENABLE_REDEF_IO**compile-time flag no longer functions. I/O procedures are now always redefinable. - Three new objects are defined for specifying I/O procedures:
[sqlite3_vfs](https://www.sqlite.org/c3ref/vfs.html),[sqlite3_file](https://www.sqlite.org/c3ref/file.html), and[sqlite3_io_methods](https://www.sqlite.org/c3ref/io_methods.html). - Three new interfaces are used to create alternative OS interfaces:
[sqlite3_vfs_register()](https://www.sqlite.org/c3ref/vfs_find.html),[sqlite3_vfs_unregister()](https://www.sqlite.org/c3ref/vfs_find.html), and[sqlite3_vfs_find()](https://www.sqlite.org/c3ref/vfs_find.html). - A new interface has been added to provide additional control over
the creation of new database connections:
[sqlite3_open_v2()](https://www.sqlite.org/c3ref/open.html). The legacy interfaces of[sqlite3_open()](https://www.sqlite.org/c3ref/open.html)and[sqlite3_open16()](https://www.sqlite.org/c3ref/open.html)continue to be fully supported.

- The undocumented
- The optional shared cache and memory management features that
were introduced in version 3.3.0 can now be used across multiple
threads within the same process. Formerly, these extensions only
applied to database connections operating within a single thread.
- The
[sqlite3_enable_shared_cache()](https://www.sqlite.org/c3ref/enable_shared_cache.html)interface now applies to all threads within a process, not to just the one thread in which it was run. - The
[sqlite3_soft_heap_limit()](https://www.sqlite.org/c3ref/soft_heap_limit.html)interface now applies to all threads within a process, not to just the one thread in which it was run. - The
[sqlite3_release_memory()](https://www.sqlite.org/c3ref/release_memory.html)interface will now attempt to reduce the memory usages across all database connections in all threads, not just connections in the thread where the interface is called. - The
[sqlite3_thread_cleanup()](https://www.sqlite.org/c3ref/aggregate_count.html)interface has become a no-op.

- The
- Restrictions on the use of the same database connection by multiple threads have been dropped. It is now safe for multiple threads to use the same database connection at the same time.
- There is now a compile-time option that allows an application to define alternative malloc()/free() implementations without having to modify any core SQLite code.
- There is now a compile-time option that allows an application to define alternative mutex implementations without having to modify any core SQLite code.

Of these changes, only 1a and 2a through 2c are incompatibilities in any formal sense. But users who have previously made custom modifications to the SQLite source (for example to add a custom OS layer for embedded hardware) might find that these changes have a larger impact. On the other hand, an important goal of these changes is to make it much easier to customize SQLite for use on different operating systems.

If your system defines a custom OS interface for SQLite or if you
were using the undocumented **sqlite3_os_switch()**
interface, then you will need to make modifications in order to
upgrade to SQLite version 3.5.0. This may seem painful at first
glance. But as you look more closely, you will probably discover
that your changes are made smaller and easier to understand and manage
by the new SQLite interface. It is likely that your changes will
now also work seamlessly with the SQLite amalgamation. You will
no longer need to make any changes to the core SQLite source code.
All of your changes can be effected by application code and you can
link against a standard, unmodified version of the SQLite amalgamation.
Furthermore, the OS interface layer, which was formerly undocumented,
is now an officially supported interface for SQLite. So you have
some assurance that this will be a one-time change and that your
new backend will continue to work in future versions of SQLite.

The new OS interface for SQLite is built around an object named
[sqlite3_vfs](https://www.sqlite.org/c3ref/vfs.html). The "vfs" stands for "Virtual File System".
The sqlite3_vfs object is basically a structure containing pointers
to functions that implement the primitive disk I/O operations that
SQLite needs to perform in order to read and write databases.
In this article, we will often refer to an sqlite3_vfs objects as a "VFS".

SQLite is able to use multiple VFSes at the same time. Each individual database connection is associated with just one VFS. But if you have multiple database connections, each connection can be associated with a different VFS.

There is always a default VFS.
The legacy interfaces [sqlite3_open()](https://www.sqlite.org/c3ref/open.html) and [sqlite3_open16()](https://www.sqlite.org/c3ref/open.html) always
use the default VFS.
The new interface for creating database connections,
[sqlite3_open_v2()](https://www.sqlite.org/c3ref/open.html), allows you to specify which VFS you want to
use by name.

Standard builds of SQLite for Unix or Windows come with a single
VFS named "unix" or "win32", as appropriate. This one VFS is also
the default. So if you are using the legacy open functions, everything
will continue to operate as it has before. The change is that an application
now has the flexibility of adding new VFS modules to implement a
customized OS layer. The [sqlite3_vfs_register()](https://www.sqlite.org/c3ref/vfs_find.html) API can be used
to tell SQLite about one or more application-defined VFS modules:

int sqlite3_vfs_register(sqlite3_vfs*, int makeDflt);

Applications can call sqlite3_vfs_register() at any time, though of course
a VFS needs to be registered before it can be used. The first argument
is a pointer to a customized VFS object that the application has prepared.
Set the second argument to true to make the new VFS the default VFS so that
it will be used by the legacy [sqlite3_open()](https://www.sqlite.org/c3ref/open.html) and [sqlite3_open16()](https://www.sqlite.org/c3ref/open.html) APIs.
If the new VFS is not the default, then you will probably have to use
the new [sqlite3_open_v2()](https://www.sqlite.org/c3ref/open.html) API to use it. Note, however, that if
a new VFS is the only VFS known to SQLite (if SQLite was compiled without
its usual default VFS or if the precompiled default VFS was removed
using [sqlite3_vfs_unregister()](https://www.sqlite.org/c3ref/vfs_find.html)) then the new VFS automatically becomes the
default VFS regardless of the makeDflt argument to [sqlite3_vfs_register()](https://www.sqlite.org/c3ref/vfs_find.html).

Standard builds include the default "unix" or "win32" VFSes.
But if you use the -DOS_OTHER=1 compile-time option, then SQLite is
built without a default VFS. In that case, the application must
register at least one VFS prior to calling [sqlite3_open()](https://www.sqlite.org/c3ref/open.html).
This is the approach that embedded applications should use.
Rather than modifying the SQLite source to insert an alternative
OS layer as was done in prior releases of SQLite, instead compile
an unmodified SQLite source file (preferably the amalgamation)
with the -DOS_OTHER=1 option, then invoke [sqlite3_vfs_register()](https://www.sqlite.org/c3ref/vfs_find.html)
to define the interface to the underlying filesystem prior to
creating any database connections.

The [sqlite3_vfs_unregister()](https://www.sqlite.org/c3ref/vfs_find.html) API is used to remove an existing
VFS from the system.

int sqlite3_vfs_unregister(sqlite3_vfs*);

The [sqlite3_vfs_find()](https://www.sqlite.org/c3ref/vfs_find.html) API is used to locate a particular VFS
by name. Its prototype is as follows:

sqlite3_vfs *sqlite3_vfs_find(const char *zVfsName);

The argument is the symbolic name for the desired VFS. If the
argument is a NULL pointer, then the default VFS is returned.
The function returns a pointer to the [sqlite3_vfs](https://www.sqlite.org/c3ref/vfs.html) object that
implements the VFS. Or it returns a NULL pointer if no object
could be found that matched the search criteria.

Once a VFS has been registered, it should never be modified. If
a change in behavior is required, a new VFS should be registered.
The application could, perhaps, use [sqlite3_vfs_find()](https://www.sqlite.org/c3ref/vfs_find.html) to locate
the old VFS, make a copy of the old VFS into a new [sqlite3_vfs](https://www.sqlite.org/c3ref/vfs.html)
object, make the desired modifications to the new VFS, unregister
the old VFS, then register the new VFS in its place. Existing
database connections would continue to use the old VFS even after
it is unregistered, but new database connections would use the
new VFS.

A VFS object is an instance of the following structure:

typedef struct sqlite3_vfs sqlite3_vfs; struct sqlite3_vfs { int iVersion; /* Structure version number */ int szOsFile; /* Size of subclassed sqlite3_file */ int mxPathname; /* Maximum file pathname length */ sqlite3_vfs *pNext; /* Next registered VFS */ const char *zName; /* Name of this virtual file system */ void *pAppData; /* Pointer to application-specific data */ int (*xOpen)(sqlite3_vfs*, const char *zName, sqlite3_file*, int flags, int *pOutFlags); int (*xDelete)(sqlite3_vfs*, const char *zName, int syncDir); int (*xAccess)(sqlite3_vfs*, const char *zName, int flags); int (*xGetTempName)(sqlite3_vfs*, char *zOut); int (*xFullPathname)(sqlite3_vfs*, const char *zName, char *zOut); void *(*xDlOpen)(sqlite3_vfs*, const char *zFilename); void (*xDlError)(sqlite3_vfs*, int nByte, char *zErrMsg); void *(*xDlSym)(sqlite3_vfs*,void*, const char *zSymbol); void (*xDlClose)(sqlite3_vfs*, void*); int (*xRandomness)(sqlite3_vfs*, int nByte, char *zOut); int (*xSleep)(sqlite3_vfs*, int microseconds); int (*xCurrentTime)(sqlite3_vfs*, double*); /* New fields may be appended in figure versions. The iVersion ** value will increment whenever this happens. */ };

To create a new VFS, an application fills in an instance of this
structure with appropriate values and then calls [sqlite3_vfs_register()](https://www.sqlite.org/c3ref/vfs_find.html).

The iVersion field of [sqlite3_vfs](https://www.sqlite.org/c3ref/vfs.html) should be 1 for SQLite version 3.5.0.
This number may increase in future versions of SQLite if we have to
modify the VFS object in some way. We hope that this never happens,
but the provision is made in case it does.

The szOsFile field is the size in bytes of the structure that defines
an open file: the [sqlite3_file](https://www.sqlite.org/c3ref/file.html) object. This object will be described
more fully below. The point here is that each VFS implementation can
define its own [sqlite3_file](https://www.sqlite.org/c3ref/file.html) object containing whatever information
the VFS implementation needs to store about an open file. SQLite needs
to know how big this object is, however, in order to preallocate enough
space to hold it.

The mxPathname field is the maximum length of a file pathname that this VFS can use. SQLite sometimes has to preallocate buffers of this size, so it should be as small as reasonably possible. Some filesystems permit huge pathnames, but in practice pathnames rarely extend beyond 100 bytes or so. You do not have to put the longest pathname that the underlying filesystem can handle here. You only have to put the longest pathname that you want SQLite to be able to handle. A few hundred is a good value in most cases.

The pNext field is used internally by SQLite. Specifically, SQLite uses this field to form a linked list of registered VFSes.

The zName field is the symbolic name of the VFS. This is the name
that the [sqlite3_vfs_find()](https://www.sqlite.org/c3ref/vfs_find.html) compares against when it is looking for
a VFS.

The pAppData pointer is unused by the SQLite core. The pointer is available to store auxiliary information that a VFS information might want to carry around.

The remaining fields of the [sqlite3_vfs](https://www.sqlite.org/c3ref/vfs.html) object all store pointers
to functions that implement primitive operations. We call these
"methods". The first method, xOpen, is used to open files on
the underlying storage media. The result is an [sqlite3_file](https://www.sqlite.org/c3ref/file.html)
object. There are additional methods, defined by the [sqlite3_file](https://www.sqlite.org/c3ref/file.html)
object itself that are used to read and write and close the file.
The additional methods are detailed below. The filename is in UTF-8.
SQLite will guarantee that the zFilename string passed to
xOpen() is a full pathname as generated by xFullPathname() and
that the string will be valid and unchanged until xClose() is
called. So the [sqlite3_file](https://www.sqlite.org/c3ref/file.html) can store a pointer to the
filename if it needs to remember the filename for some reason.
The flags argument to xOpen() is a copy of the flags argument
to sqlite3_open_v2(). If sqlite3_open() or sqlite3_open16()
is used, then flags is [SQLITE_OPEN_READWRITE](https://www.sqlite.org/c3ref/c_open_autoproxy.html) | [SQLITE_OPEN_CREATE](https://www.sqlite.org/c3ref/c_open_autoproxy.html).
If xOpen() opens a file read-only then it sets *pOutFlags to
include [SQLITE_OPEN_READONLY](https://www.sqlite.org/c3ref/c_open_autoproxy.html). Other bits in *pOutFlags may be
set.
SQLite will also add one of the following flags to the xOpen()
call, depending on the object being opened:

-
[SQLITE_OPEN_MAIN_DB](https://www.sqlite.org/c3ref/c_open_autoproxy.html) -
[SQLITE_OPEN_MAIN_JOURNAL](https://www.sqlite.org/c3ref/c_open_autoproxy.html) -
[SQLITE_OPEN_TEMP_DB](https://www.sqlite.org/c3ref/c_open_autoproxy.html) -
[SQLITE_OPEN_TEMP_JOURNAL](https://www.sqlite.org/c3ref/c_open_autoproxy.html) -
[SQLITE_OPEN_TRANSIENT_DB](https://www.sqlite.org/c3ref/c_open_autoproxy.html) -
[SQLITE_OPEN_SUBJOURNAL](https://www.sqlite.org/c3ref/c_open_autoproxy.html) -
[SQLITE_OPEN_SUPER_JOURNAL](https://www.sqlite.org/c3ref/c_open_autoproxy.html)

The differences between an [SQLITE_OPEN_TEMP_DB](https://www.sqlite.org/c3ref/c_open_autoproxy.html) database and an
[SQLITE_OPEN_TRANSIENT_DB](https://www.sqlite.org/c3ref/c_open_autoproxy.html) database is this: The [SQLITE_OPEN_TEMP_DB](https://www.sqlite.org/c3ref/c_open_autoproxy.html)
is used for explicitly declared and named TEMP tables (using the
CREATE TEMP TABLE syntax) or for named tables in a temporary database
that is created by opening a database with a filename that is an empty
string. An [SQLITE_OPEN_TRANSIENT_DB](https://www.sqlite.org/c3ref/c_open_autoproxy.html) holds a database table that
SQLite creates automatically in order to evaluate a subquery or
ORDER BY or GROUP BY clause. Both TEMP_DB and TRANSIENT_DB databases
are private and are deleted automatically. TEMP_DB databases last
for the duration of the database connection. TRANSIENT_DB databases
last only for the duration of a single SQL statement.

The xDelete method is used to delete a file. The name of the file is given in the second parameter. The filename will be in UTF-8. The VFS must convert the filename into whatever character representation the underlying operating system expects. If the syncDir parameter is true, then the xDelete method should not return until the change to the directory contents for the directory containing the deleted file have been synced to disk in order to ensure that the file does not "reappear" if a power failure occurs soon after.

The xAccess method is used to check for access permissions on a file.
The filename will be UTF-8 encoded. The flags argument will be
[SQLITE_ACCESS_EXISTS](https://www.sqlite.org/c3ref/c_access_exists.html) to check for the existence of the file,
[SQLITE_ACCESS_READWRITE](https://www.sqlite.org/c3ref/c_access_exists.html) to check to see if the file is both readable
and writable, or [SQLITE_ACCESS_READ](https://www.sqlite.org/c3ref/c_access_exists.html) to check to see if the file is
at least readable. The "file" named by the second parameter might
be a directory or folder name.

The xGetTempName method computes the name of a temporary file that SQLite can use. The name should be written into the buffer given by the second parameter. SQLite will size that buffer to hold at least mxPathname bytes. The generated filename should be in UTF-8. To avoid security problems, the generated temporary filename should contain enough randomness to prevent an attacker from guessing the temporary filename in advance.

The xFullPathname method is used to convert a relative pathname into a full pathname. The resulting full pathname is written into the buffer provided by the third parameter. SQLite will size the output buffer to at least mxPathname bytes. Both the input and output names should be in UTF-8.

The xDlOpen, xDlError, xDlSym, and xDlClose methods are all used for
accessing shared libraries at run-time. These methods may be omitted
(and their pointers set to zero) if the library is compiled with
[SQLITE_OMIT_LOAD_EXTENSION](https://www.sqlite.org/compile.html#omit_load_extension) or if the [sqlite3_enable_load_extension()](https://www.sqlite.org/c3ref/enable_load_extension.html)
interface is never used to enable dynamic extension loading. The
xDlOpen method opens a shared library or DLL and returns a pointer to
a handle. NULL is returned if the open fails. If the open fails,
the xDlError method can be used to obtain a text error message.
The message is written into the zErrMsg buffer of the third parameter
which is at least nByte bytes in length. The xDlSym returns a pointer
to a symbol in the shared library. The name of the symbol is given
by the second parameter. UTF-8 encoding is assumed. If the symbol
is not found a NULL pointer is returned. The xDlClose routine closes
the shared library.

The xRandomness method is used exactly once to initialize the pseudo-random number generator (PRNG) inside of SQLite. Only the xRandomness method on the default VFS is used. The xRandomness methods on other VFSes are never accessed by SQLite. The xRandomness routine requests that nByte bytes of randomness be written into zOut. The routine returns the actual number of bytes of randomness obtained. The quality of the randomness so obtained will determine the quality of the randomness generated by built-in SQLite functions such as random() and randomblob(). SQLite also uses its PRNG to generate temporary file names. On some platforms (ex: Windows) SQLite assumes that temporary file names are unique without actually testing for collisions, so it is important to have good-quality randomness even if the random() and randomblob() functions are never used.

The xSleep method is used to suspend the calling thread for at
least the number of microseconds given. This method is used to
implement the [sqlite3_sleep()](https://www.sqlite.org/c3ref/sleep.html) and [sqlite3_busy_timeout()](https://www.sqlite.org/c3ref/busy_timeout.html) APIs.
In the case of [sqlite3_sleep()](https://www.sqlite.org/c3ref/sleep.html) the xSleep method of the default
VFS is always used. If the underlying system does not have a
microsecond resolution sleep capability, then the sleep time should
be rounded up. xSleep returns this rounded-up value.

The xCurrentTime method finds the current time and date and writes the result as a double-precision floating point value into a pointer provided by the second parameter. The time and date is in coordinated universal time (UTC) and is a fractional Julian day number.

The result of opening a file is an instance of an [sqlite3_file](https://www.sqlite.org/c3ref/file.html) object.
The [sqlite3_file](https://www.sqlite.org/c3ref/file.html) object is an abstract base class defined as follows:

typedef struct sqlite3_file sqlite3_file; struct sqlite3_file { const struct sqlite3_io_methods *pMethods; };

Each VFS implementation will subclass the [sqlite3_file](https://www.sqlite.org/c3ref/file.html) by adding
additional fields at the end to hold whatever information the VFS
needs to know about an open file. It does not matter what information
is stored as long as the total size of the structure does not exceed
the szOsFile value recorded in the [sqlite3_vfs](https://www.sqlite.org/c3ref/vfs.html) object.

The [sqlite3_io_methods](https://www.sqlite.org/c3ref/io_methods.html) object is a structure that contains pointers
to methods for reading, writing, and otherwise dealing with files.
This object is defined as follows:

typedef struct sqlite3_io_methods sqlite3_io_methods; struct sqlite3_io_methods { int iVersion; int (*xClose)(sqlite3_file*); int (*xRead)(sqlite3_file*, void*, int iAmt, sqlite3_int64 iOfst); int (*xWrite)(sqlite3_file*, const void*, int iAmt, sqlite3_int64 iOfst); int (*xTruncate)(sqlite3_file*, sqlite3_int64 size); int (*xSync)(sqlite3_file*, int flags); int (*xFileSize)(sqlite3_file*, sqlite3_int64 *pSize); int (*xLock)(sqlite3_file*, int); int (*xUnlock)(sqlite3_file*, int); int (*xCheckReservedLock)(sqlite3_file*); int (*xFileControl)(sqlite3_file*, int op, void *pArg); int (*xSectorSize)(sqlite3_file*); int (*xDeviceCharacteristics)(sqlite3_file*); /* Additional methods may be added in future releases */ };

The iVersion field of [sqlite3_io_methods](https://www.sqlite.org/c3ref/io_methods.html) is provided as insurance
against future enhancements. The iVersion value should always be
1 for SQLite version 3.5.

The xClose method closes the file. The space for the [sqlite3_file](https://www.sqlite.org/c3ref/file.html)
structure is deallocated by the caller. But if the [sqlite3_file](https://www.sqlite.org/c3ref/file.html)
contains pointers to other allocated memory or resources, those
allocations should be released by the xClose method.

The xRead method reads iAmt bytes from the file beginning at a byte
offset to iOfst. The data read is stored in the pointer of the
second parameter. xRead returns the [SQLITE_OK](https://www.sqlite.org/rescode.html#ok) on success,
[SQLITE_IOERR_SHORT_READ](https://www.sqlite.org/rescode.html#ioerr_short_read) if it was not able to read the full number
of bytes because it reached end-of-file, or [SQLITE_IOERR_READ](https://www.sqlite.org/rescode.html#ioerr_read) for
any other error.

The xWrite method writes iAmt bytes of data from the second parameter
into the file beginning at an offset of iOfst bytes. If the size of
the file is less than iOfst bytes prior to the write, then xWrite should
ensure that the file is extended with zeros up to iOfst bytes prior
to beginning its write. xWrite should extend the file as
necessary so that the size of the file is at least iAmt+iOfst bytes
at the conclusion of the xWrite call. The xWrite method returns
[SQLITE_OK](https://www.sqlite.org/rescode.html#ok) on success. If the write cannot complete because the
underlying storage medium is full, then [SQLITE_FULL](https://www.sqlite.org/rescode.html#full) is returned.
[SQLITE_IOERR_WRITE](https://www.sqlite.org/rescode.html#ioerr_write) should be returned for any other error.

The xTruncate method truncates a file to be nByte bytes in length.
If the file is already nByte bytes or less in length then this
method is a no-op. The xTruncate method returns [SQLITE_OK](https://www.sqlite.org/rescode.html#ok) on
success and [SQLITE_IOERR_TRUNCATE](https://www.sqlite.org/rescode.html#ioerr_truncate) if anything goes wrong.

The xSync method is used to force previously written data out of
operating system cache and into non-volatile memory. The second
parameter is usually [SQLITE_SYNC_NORMAL](https://www.sqlite.org/c3ref/c_sync_dataonly.html). If the second parameter
is [SQLITE_SYNC_FULL](https://www.sqlite.org/c3ref/c_sync_dataonly.html) then the xSync method should make sure that
data has also been flushed through the disk controllers cache.
The [SQLITE_SYNC_FULL](https://www.sqlite.org/c3ref/c_sync_dataonly.html) parameter is the equivalent of the F_FULLSYNC
ioctl() on Mac OS X. The xSync method returns
[SQLITE_OK](https://www.sqlite.org/rescode.html#ok) on success and [SQLITE_IOERR_FSYNC](https://www.sqlite.org/rescode.html#ioerr_fsync) if anything goes wrong.

The xFileSize() method determines the current size of the file
in bytes and writes that value into *pSize. It returns [SQLITE_OK](https://www.sqlite.org/rescode.html#ok)
on success and [SQLITE_IOERR_FSTAT](https://www.sqlite.org/rescode.html#ioerr_fstat) if something goes wrong.

The xLock and xUnlock methods are used to set and clear file locks. SQLite supports five levels of file locks, in order:

The underlying implementation can support some subset of these locking levels as long as it meets the other requirements of this paragraph. The locking level is specified as the second argument to both xLock and xUnlock. The xLock method increases the locking level to the specified locking level or higher. The xUnlock method decreases the locking level to no lower than the level specified.The xCheckReservedLock() method checks to see if another connection or another process is currently holding a reserved, pending, or exclusive lock on the file. It returns true or false.

The xFileControl() method is a generic interface that allows custom
VFS implementations to directly control an open file using the
(new and experimental)
[sqlite3_file_control()](https://www.sqlite.org/c3ref/file_control.html) interface. The second "op" argument
is an integer opcode. The third
argument is a generic pointer which is intended to be a pointer
to a structure that may contain arguments or space in which to
write return values. Potential uses for xFileControl() might be
functions to enable blocking locks with timeouts, to change the
locking strategy (for example to use dot-file locks), to inquire
about the status of a lock, or to break stale locks. The SQLite
core reserves opcodes less than 100 for its own use.
A [list of opcodes](https://www.sqlite.org/c3ref/c_fcntl_begin_atomic_write.html#sqlitefcntllockstate) less than 100 is available.
Applications that define a custom xFileControl method should use opcodes
greater than 100 to avoid conflicts.

The xSectorSize returns the "sector size" of the underlying non-volatile media. A "sector" is defined as the smallest unit of storage that can be written without disturbing adjacent storage. On a disk drive the "sector size" has until recently been 512 bytes, though there is a push to increase this value to 4KiB. SQLite needs to know the sector size so that it can write a full sector at a time, and thus avoid corrupting adjacent storage space if a power loss occurs in the middle of a write.

The xDeviceCharacteristics method returns an integer bit vector that defines any special properties that the underlying storage medium might have that SQLite can use to increase performance. The allowed return is the bit-wise OR of the following values:

-
[SQLITE_IOCAP_ATOMIC](https://www.sqlite.org/c3ref/c_iocap_atomic.html) -
[SQLITE_IOCAP_ATOMIC512](https://www.sqlite.org/c3ref/c_iocap_atomic.html) -
[SQLITE_IOCAP_ATOMIC1K](https://www.sqlite.org/c3ref/c_iocap_atomic.html) -
[SQLITE_IOCAP_ATOMIC2K](https://www.sqlite.org/c3ref/c_iocap_atomic.html) -
[SQLITE_IOCAP_ATOMIC4K](https://www.sqlite.org/c3ref/c_iocap_atomic.html) -
[SQLITE_IOCAP_ATOMIC8K](https://www.sqlite.org/c3ref/c_iocap_atomic.html) -
[SQLITE_IOCAP_ATOMIC16K](https://www.sqlite.org/c3ref/c_iocap_atomic.html) -
[SQLITE_IOCAP_ATOMIC32K](https://www.sqlite.org/c3ref/c_iocap_atomic.html) -
[SQLITE_IOCAP_ATOMIC64K](https://www.sqlite.org/c3ref/c_iocap_atomic.html) -
[SQLITE_IOCAP_SAFE_APPEND](https://www.sqlite.org/c3ref/c_iocap_atomic.html) -
[SQLITE_IOCAP_SEQUENTIAL](https://www.sqlite.org/c3ref/c_iocap_atomic.html)

The preceding paragraphs contain a lot of information. To ease the task of constructing a new VFS for SQLite we offer the following implementation checklist:

- Define an appropriate subclass of the
[sqlite3_file](https://www.sqlite.org/c3ref/file.html)object. - Implement the methods required by the
[sqlite3_io_methods](https://www.sqlite.org/c3ref/io_methods.html)object. - Create a static and
constant
[sqlite3_io_methods](https://www.sqlite.org/c3ref/io_methods.html)object containing pointers to the methods from the previous step. - Implement the xOpen method that opens a file and populates an
[sqlite3_file](https://www.sqlite.org/c3ref/file.html)object, including setting pMethods to point to the[sqlite3_io_methods](https://www.sqlite.org/c3ref/io_methods.html)object from the previous step. - Implement the other methods required by
[sqlite3_vfs](https://www.sqlite.org/c3ref/vfs.html). - Define a static (but not constant)
[sqlite3_vfs](https://www.sqlite.org/c3ref/vfs.html)structure that contains pointers to the xOpen method and the other methods and which contains the appropriate values for iVersion, szOsFile, mxPathname, zName, and pAppData. - Implement a procedure that calls
[sqlite3_vfs_register()](https://www.sqlite.org/c3ref/vfs_find.html)and passes it a pointer to the[sqlite3_vfs](https://www.sqlite.org/c3ref/vfs.html)structure from the previous step. This procedure is probably the only exported symbol in the source file that implements your VFS.

Within your application, call the procedure implemented in the last step above as part of your initialization process before any database connections are opened.

Beginning with version 3.5, SQLite obtains all of the heap memory it
needs using the routines [sqlite3_malloc()](https://www.sqlite.org/c3ref/free.html), [sqlite3_free()](https://www.sqlite.org/c3ref/free.html), and
[sqlite3_realloc()](https://www.sqlite.org/c3ref/free.html). These routines have existed in prior versions
of SQLite, but SQLite has previously bypassed these routines and used
its own memory allocator. This all changes in version 3.5.0.

The SQLite source tree actually contains multiple versions of the memory allocator. The default high-speed version found in the "mem1.c" source file is used for most builds. But if the SQLITE_MEMDEBUG flag is enabled, a separate memory allocator in the "mem2.c" source file is used instead. The mem2.c allocator implements lots of hooks to do error checking and to simulate memory allocation failures for testing purposes. Both of these allocators use the malloc()/free() implementation in the standard C library.

Applications are not required to use either of these standard memory
allocators. If SQLite is compiled with [SQLITE_OMIT_MEMORY_ALLOCATION](https://www.sqlite.org/compile.html#omitfeatures)
then no implementation for the [sqlite3_malloc()](https://www.sqlite.org/c3ref/free.html), [sqlite3_realloc()](https://www.sqlite.org/c3ref/free.html),
and [sqlite3_free()](https://www.sqlite.org/c3ref/free.html) functions is provided. Instead, the application
that links against SQLite must provide its own implementation of these
functions. The application provided memory allocator is not required
to use the malloc()/free() implementation in the standard C library.
An embedded application might provide an alternative memory allocator
that uses memory for a fixed memory pool set aside for the exclusive
use of SQLite, for example.

Applications that implement their own memory allocator must provide
implementation for the usual three allocation functions
[sqlite3_malloc()](https://www.sqlite.org/c3ref/free.html), [sqlite3_realloc()](https://www.sqlite.org/c3ref/free.html), and [sqlite3_free()](https://www.sqlite.org/c3ref/free.html).
And they must also implement a fourth function:

int sqlite3_memory_alarm( void(*xCallback)(void *pArg, sqlite3_int64 used, int N), void *pArg, sqlite3_int64 iThreshold );

The [sqlite3_memory_alarm](https://www.sqlite.org/c3ref/aggregate_count.html) routine is used to register
a callback on memory allocation events.
This routine registers or clears a callback that fires when
the amount of memory allocated exceeds iThreshold. Only
a single callback can be registered at a time. Each call
to [sqlite3_memory_alarm()](https://www.sqlite.org/c3ref/aggregate_count.html) overwrites the previous callback.
The callback is disabled by setting xCallback to a NULL
pointer.

The parameters to the callback are the pArg value, the
amount of memory currently in use, and the size of the
allocation that provoked the callback. The callback will
presumably invoke [sqlite3_free()](https://www.sqlite.org/c3ref/free.html) to free up memory space.
The callback may invoke [sqlite3_malloc()](https://www.sqlite.org/c3ref/free.html) or [sqlite3_realloc()](https://www.sqlite.org/c3ref/free.html)
but if it does, no additional callbacks will be invoked by
the recursive calls.

The [sqlite3_soft_heap_limit()](https://www.sqlite.org/c3ref/soft_heap_limit.html) interface works by registering
a memory alarm at the soft heap limit and invoking
[sqlite3_release_memory()](https://www.sqlite.org/c3ref/release_memory.html) in the alarm callback. Application
programs should not attempt to use the [sqlite3_memory_alarm()](https://www.sqlite.org/c3ref/aggregate_count.html)
interface because doing so will interfere with the
[sqlite3_soft_heap_limit()](https://www.sqlite.org/c3ref/soft_heap_limit.html) module. This interface is exposed
only so that applications can provide their own
alternative implementation when the SQLite core is
compiled with [SQLITE_OMIT_MEMORY_ALLOCATION](https://www.sqlite.org/compile.html#omitfeatures).

The built-in memory allocators in SQLite also provide the following additional interfaces:

sqlite3_int64 sqlite3_memory_used(void); sqlite3_int64 sqlite3_memory_highwater(int resetFlag);

These interfaces can be used by an application to monitor how
much memory SQLite is using. The [sqlite3_memory_used()](https://www.sqlite.org/c3ref/memory_highwater.html) routine
returns the number of bytes of memory currently in use and the
[sqlite3_memory_highwater()](https://www.sqlite.org/c3ref/memory_highwater.html) returns the maximum instantaneous
memory usage. Neither routine includes the overhead associated
with the memory allocator. These routines are provided for use
by the application. SQLite never invokes them itself. So if
the application is providing its own memory allocation subsystem,
it can omit these interfaces if desired.

SQLite has always been threadsafe in the sense that it is safe to use different SQLite database connections in different threads at the same time. The constraint was that the same database connection could not be used in two separate threads at once. SQLite version 3.5.0 relaxes this constraint.

In order to allow multiple threads to use the same database connection at the same time, SQLite must make extensive use of mutexes. And for this reason a new mutex subsystem has been added. The mutex subsystem has the following interface:

sqlite3_mutex *sqlite3_mutex_alloc(int); void sqlite3_mutex_free(sqlite3_mutex*); void sqlite3_mutex_enter(sqlite3_mutex*); int sqlite3_mutex_try(sqlite3_mutex*); void sqlite3_mutex_leave(sqlite3_mutex*);

Though these routines exist for the use of the SQLite core,
application code is free to use these routines as well, if desired.
A mutex is an [sqlite3_mutex](https://www.sqlite.org/c3ref/mutex.html) object. The [sqlite3_mutex_alloc()](https://www.sqlite.org/c3ref/mutex_alloc.html)
routine allocates a new mutex object and returns a pointer to it.
The argument to [sqlite3_mutex_alloc()](https://www.sqlite.org/c3ref/mutex_alloc.html) should be
[SQLITE_MUTEX_FAST](https://www.sqlite.org/c3ref/c_mutex_fast.html) or [SQLITE_MUTEX_RECURSIVE](https://www.sqlite.org/c3ref/c_mutex_fast.html) for non-recursive
and recursive mutexes, respectively. If the underlying system does
not provide non-recursive mutexes, then a recursive mutex can be
substituted in that case. The argument to [sqlite3_mutex_alloc()](https://www.sqlite.org/c3ref/mutex_alloc.html)
can also be a constant designating one of several static mutexes:

-
[SQLITE_MUTEX_STATIC_MAIN](https://www.sqlite.org/c3ref/c_mutex_fast.html) -
[SQLITE_MUTEX_STATIC_MEM](https://www.sqlite.org/c3ref/c_mutex_fast.html) -
[SQLITE_MUTEX_STATIC_MEM2](https://www.sqlite.org/c3ref/c_mutex_fast.html) -
[SQLITE_MUTEX_STATIC_PRNG](https://www.sqlite.org/c3ref/c_mutex_fast.html) -
[SQLITE_MUTEX_STATIC_LRU](https://www.sqlite.org/c3ref/c_mutex_fast.html)

The [sqlite3_mutex_free()](https://www.sqlite.org/c3ref/mutex_alloc.html) routine should be used to deallocate
a non-static mutex. If a static mutex is passed to this routine
then the behavior is undefined.

The [sqlite3_mutex_enter()](https://www.sqlite.org/c3ref/mutex_alloc.html) attempts to enter the mutex and blocks
if another thread is already there. [sqlite3_mutex_try()](https://www.sqlite.org/c3ref/mutex_alloc.html) attempts
to enter and returns [SQLITE_OK](https://www.sqlite.org/rescode.html#ok) on success or [SQLITE_BUSY](https://www.sqlite.org/rescode.html#busy) if another
thread is already there. [sqlite3_mutex_leave()](https://www.sqlite.org/c3ref/mutex_alloc.html) exits a mutex.
The mutex is held until the number of exits matches the number of
entrances. If [sqlite3_mutex_leave()](https://www.sqlite.org/c3ref/mutex_alloc.html) is called on a mutex that
the thread is not currently holding, then the behavior is undefined.
If any routine is called for a deallocated mutex, then the behavior
is undefined.

The SQLite source code provides multiple implementations of these APIs, suitable for varying environments. If SQLite is compiled with the SQLITE_THREADSAFE=0 flag then a no-op mutex implementation that is fast but does no real mutual exclusion is provided. That implementation is suitable for use in single-threaded applications or applications that only use SQLite in a single thread. Other real mutex implementations are provided based on the underlying operating system.

Embedded applications may wish to provide their own mutex implementation. If SQLite is compiled with the -DSQLITE_MUTEX_APPDEF=1 compile-time flag then the SQLite core provides no mutex subsystem and a mutex subsystem that matches the interface described above must be provided by the application that links against SQLite.

Version 3.5.0 of SQLite changes the behavior of a few APIs in ways that are technically incompatible. However, these APIs are seldom used and even when they are used it is difficult to imagine a scenario where the change might break something. The changes makes these interfaces more useful and powerful.

Prior to version 3.5.0, the [sqlite3_enable_shared_cache()](https://www.sqlite.org/c3ref/enable_shared_cache.html) API
would enable and disable the shared cache feature for all connections
within a single thread - the same thread from which the
sqlite3_enable_shared_cache() routine was called. Database connections
that used the shared cache were restricted to running in the same
thread in which they were opened. Beginning with version 3.5.0,
the sqlite3_enable_shared_cache() applies to all database connections
in all threads within the process. Now database connections running
in separate threads can share a cache. And database connections that
use shared cache can migrate from one thread to another.

Prior to version 3.5.0 the [sqlite3_soft_heap_limit()](https://www.sqlite.org/c3ref/soft_heap_limit.html) set an upper
bound on heap memory usage for all database connections within a
single thread. Each thread could have its own heap limit. Beginning
in version 3.5.0, there is a single heap limit for the entire process.
This seems more restrictive (one limit as opposed to many) but in
practice it is what most users want.

Prior to version 3.5.0 the [sqlite3_release_memory()](https://www.sqlite.org/c3ref/release_memory.html) function would
try to reclaim memory from all database connections in the same thread
as the sqlite3_release_memory() call. Beginning with version 3.5.0,
the sqlite3_release_memory() function will attempt to reclaim memory
from all database connections in all threads.

The transition from SQLite version 3.4.2 to 3.5.0 is a major change. Every source code file in the SQLite core had to be modified, some extensively. And the change introduced some minor incompatibilities in the C interface. But we feel that the benefits of the transition from 3.4.2 to 3.5.0 far outweigh the pain of porting. The new VFS layer is now well-defined and stable and should simplify future customizations. The VFS layer, and the separable memory allocator and mutex subsystems allow a standard SQLite source code amalgamation to be used in an embedded project without change, greatly simplifying configuration management. And the resulting system is much more tolerant of highly threaded designs.

*This page was last updated on 2025-07-12 15:11:36Z *
