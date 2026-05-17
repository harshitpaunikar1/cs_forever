Title: Commands | Docs
Mapped Topic: Caching and in-memory data structures
Source URL: https://redis.io/docs/latest/commands/
Source Type: official_docs
Trust Score: 94
Fetched At: 2026-04-17T07:08:48+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

#
Redis 8.6 Commands Reference

Complete list of all Redis commands available in version 8.6, organized by functional group

[Read more](https://redis.io/docs/latest/commands/redis-8-6-commands/)

{"categories":null,"description":"","duplicateOf":"head:data-ai-metadata","location":"body","title":"Commands","tableOfContents":{"sections":[]},"codeExamples":[]}

Redis 8.6 Commands Reference

Complete list of all Redis commands available in version 8.6, organized by functional group

Learn more â

Redis 8.4 Commands Reference

Complete list of all Redis commands available in version 8.4, organized by functional group

Learn more â

Redis 8.2 Commands Reference

Complete list of all Redis commands available in version 8.2, organized by functional group

Learn more â

Redis 8.0 Commands Reference

Complete list of all Redis commands available in version 8.0, organized by functional group

Learn more â

Redis 7.4 Commands Reference

Complete list of all Redis commands available in version 7.4, organized by functional group

Learn more â

Redis 7.2 Commands Reference

Complete list of all Redis commands available in version 7.2, organized by functional group

Learn more â

Redis 6.2 Commands Reference

Complete list of all Redis commands available in version 6.2, organized by functional group

Learn more â

ACL CAT

Lists the ACL categories, or the commands inside a category.

Learn more â

ACL DELUSER

Deletes ACL users, and terminates their connections.

Learn more â

ACL DRYRUN

Simulates the execution of a command by a user, without executing the command.

Learn more â

ACL GENPASS

Generates a pseudorandom, secure password that can be used to identify ACL users.

Learn more â

ACL GETUSER

Lists the ACL rules of a user.

Learn more â

ACL LIST

Dumps the effective rules in ACL file format.

Learn more â

ACL LOAD

Reloads the rules from the configured ACL file.

Learn more â

ACL LOG

Lists recent security events generated due to ACL rules.

Learn more â

ACL SAVE

Saves the effective ACL rules in the configured ACL file.

Learn more â

ACL SETUSER

Creates and modifies an ACL user and its rules.

Learn more â

ACL USERS

Lists all ACL users.

Learn more â

ACL WHOAMI

Returns the authenticated username of the current connection.

Learn more â

APPEND

Appends a string to the value of a key. Creates the key if it doesn't exist.

Learn more â

ASKING

Signals that a cluster client is following an -ASK redirect.

Learn more â

AUTH

Authenticates the connection.

Learn more â

BF.ADD

Adds an item to a Bloom Filter

Learn more â

BF.CARD

Returns the cardinality of a Bloom filter

Learn more â

BF.EXISTS

Checks whether an item exists in a Bloom Filter

Learn more â

BF.INFO

Returns information about a Bloom Filter

Learn more â

BF.INSERT

Adds one or more items to a Bloom Filter. A filter will be created if it does not exist

Learn more â

BF.LOADCHUNK

Restores a filter previously saved using SCANDUMP

Learn more â

BF.MADD

Adds one or more items to a Bloom Filter. A filter will be created if it does not exist

Learn more â

BF.MEXISTS

Checks whether one or more items exist in a Bloom Filter

Learn more â

BF.RESERVE

Creates a new Bloom Filter

Learn more â

BF.SCANDUMP

Begins an incremental save of the bloom filter

Learn more â

BGREWRITEAOF

Asynchronously rewrites the append-only file to disk.

Learn more â

BGSAVE

Asynchronously saves the database(s) to disk.

Learn more â

BITCOUNT

Counts the number of set bits (population counting) in a string.

Learn more â

BITFIELD

Performs arbitrary bitfield integer operations on strings.

Learn more â

BITFIELD_RO

Performs arbitrary read-only bitfield integer operations on strings.

Learn more â

BITOP

Performs bitwise operations on multiple strings, and stores the result.

Learn more â

BITPOS

Finds the first set (1) or clear (0) bit in a string.

Learn more â

BLMOVE

Pops an element from a list, pushes it to another list and returns it. Blocks until an element is available otherwise. Deletes the list if the last element was moved.

Learn more â

BLMPOP

Pops the first element from one of multiple lists. Blocks until an element is available otherwise. Deletes the list if the last element was popped.

Learn more â

BLPOP

Removes and returns the first element in a list. Blocks until an element is available otherwise. Deletes the list if the last element was popped.

Learn more â

BRPOP

Removes and returns the last element in a list. Blocks until an element is available otherwise. Deletes the list if the last element was popped.

Learn more â

BRPOPLPUSH

Deprecated

Use BLMOVE with the RIGHT and LEFT arguments instead

Pops an element from a list, pushes it to another list and returns it. Block until an element is available otherwise. Deletes the list if the last element was popped.

Learn more â

BZMPOP

Removes and returns a member by score from one or more sorted sets. Blocks until a member is available otherwise. Deletes the sorted set if the last element was popped.

Learn more â

BZPOPMAX

Removes and returns the member with the highest score from one or more sorted sets. Blocks until a member available otherwise. Deletes the sorted set if the last element was popped.

Learn more â

BZPOPMIN

Removes and returns the member with the lowest score from one or more sorted sets. Blocks until a member is available otherwise. Deletes the sorted set if the last element was popped.

Learn more â

CF.ADD

Adds an item to a Cuckoo Filter

Learn more â

CF.ADDNX

Adds an item to a Cuckoo Filter if the item did not exist previously.

Learn more â

CF.COUNT

Return the number of times an item might be in a Cuckoo Filter

Learn more â

CF.DEL

Deletes an item from a Cuckoo Filter

Learn more â

CF.EXISTS

Checks whether one or more items exist in a Cuckoo Filter

Learn more â

CF.INFO

Returns information about a Cuckoo Filter

Learn more â

CF.INSERT

Adds one or more items to a Cuckoo Filter. A filter will be created if it does not exist

Learn more â

CF.INSERTNX

Adds one or more items to a Cuckoo Filter if the items did not exist previously. A filter will be created if it does not exist

Learn more â

CF.LOADCHUNK

Restores a filter previously saved using SCANDUMP

Learn more â

CF.MEXISTS

Checks whether one or more items exist in a Cuckoo Filter

Learn more â

CF.RESERVE

Creates a new Cuckoo Filter

Learn more â

CF.SCANDUMP

Begins an incremental save of the bloom filter

Learn more â

CLIENT CACHING

Instructs the server whether to track the keys in the next request.

Learn more â

CLIENT GETNAME

Returns the name of the connection.

Learn more â

CLIENT GETREDIR

Returns the client ID to which the connection's tracking notifications are redirected.

Learn more â

CLIENT ID

Returns the unique client ID of the connection.

Learn more â

CLIENT INFO

Returns information about the connection.

Learn more â

CLIENT KILL

Terminates open connections.

Learn more â

CLIENT LIST

Lists open connections.

Learn more â

CLIENT NO-EVICT

Sets the client eviction mode of the connection.

Learn more â

CLIENT NO-TOUCH

Controls whether commands sent by the client affect the LRU/LFU of accessed keys.

Learn more â

CLIENT PAUSE

Suspends commands processing.

Learn more â

CLIENT REPLY

Instructs the server whether to reply to commands.

Learn more â

CLIENT SETINFO

Sets information specific to the client or connection.

Learn more â

CLIENT SETNAME

Sets the connection name.

Learn more â

CLIENT TRACKING

Controls server-assisted client-side caching for the connection.

Learn more â

CLIENT TRACKINGINFO

Returns information about server-assisted client-side caching for the connection.

Learn more â

CLIENT UNBLOCK

Unblocks a client blocked by a blocking command from a different connection.

Learn more â

CLIENT UNPAUSE

Resumes processing commands from paused clients.

Learn more â

CLUSTER ADDSLOTS

Assigns new hash slots to a node.

Learn more â

CLUSTER ADDSLOTSRANGE

Assigns new hash slot ranges to a node.

Learn more â

CLUSTER BUMPEPOCH

Advances the cluster config epoch.

Learn more â

CLUSTER COUNT-FAILURE-REPORTS

Returns the number of active failure reports active for a node.

Learn more â

CLUSTER COUNTKEYSINSLOT

Returns the number of keys in a hash slot.

Learn more â

CLUSTER DELSLOTS

Sets hash slots as unbound for a node.

Learn more â

CLUSTER DELSLOTSRANGE

Sets hash slot ranges as unbound for a node.

Learn more â

CLUSTER FAILOVER

Forces a replica to perform a manual failover of its master.

Learn more â

CLUSTER FLUSHSLOTS

Deletes all slots information from a node.

Learn more â

CLUSTER FORGET

Removes a node from the nodes table.

Learn more â

CLUSTER GETKEYSINSLOT

Returns the key names in a hash slot.

Learn more â

CLUSTER INFO

Returns information about the state of a node.

Learn more â

CLUSTER KEYSLOT

Returns the hash slot for a key.

Learn more â

CLUSTER LINKS

Returns a list of all TCP links to and from peer nodes.

Learn more â

CLUSTER MEET

Forces a node to handshake with another node.

Learn more â

CLUSTER MIGRATION

Start, monitor, and cancel atomic slot migration tasks.

Learn more â

CLUSTER MYID

Returns the ID of a node.

Learn more â

CLUSTER MYSHARDID

Returns the shard ID of a node.

Learn more â

CLUSTER NODES

Returns the cluster configuration for a node.

Learn more â

CLUSTER REPLICAS

Lists the replica nodes of a master node.

Learn more â

CLUSTER REPLICATE

Configure a node as replica of a master node.

Learn more â

CLUSTER RESET

Resets a node.

Learn more â

CLUSTER SAVECONFIG

Forces a node to save the cluster configuration to disk.

Learn more â

CLUSTER SET-CONFIG-EPOCH

Sets the configuration epoch for a new node.

Learn more â

CLUSTER SETSLOT

Binds a hash slot to a node.

Learn more â

CLUSTER SHARDS

Returns the mapping of cluster slots to shards.

Learn more â

CLUSTER SLAVES

Deprecated

Use CLUSTER REPLICAS instead

Lists the replica nodes of a master node.

Learn more â

CLUSTER SLOT-STATS

Return an array of slot usage statistics for slots assigned to the current node.

Learn more â

CLUSTER SLOTS

Deprecated

Use CLUSTER SHARDS instead

Returns the mapping of cluster slots to nodes.

Learn more â

CMS.INCRBY

Increases the count of one or more items by increment

Learn more â

CMS.INFO

Returns information about a sketch

Learn more â

CMS.INITBYDIM

Initializes a Count-Min Sketch to dimensions specified by user

Learn more â

CMS.INITBYPROB

Initializes a Count-Min Sketch to accommodate requested tolerances.

Learn more â

CMS.MERGE

Merges several sketches into one sketch

Learn more â

CMS.QUERY

Returns the count for one or more items in a sketch

Learn more â

COMMAND

Returns detailed information about all commands.

Learn more â

COMMAND COUNT

Returns a count of commands.

Learn more â

COMMAND DOCS

Returns documentary information about one, multiple or all commands.

Learn more â

COMMAND GETKEYS

Extracts the key names from an arbitrary command.

Learn more â

COMMAND GETKEYSANDFLAGS

Extracts the key names and access flags for an arbitrary command.

Learn more â

COMMAND INFO

Returns information about one, multiple or all commands.

Learn more â

COMMAND LIST

Returns a list of command names.

Learn more â

Commands

Learn more â

CONFIG GET

Returns the effective values of configuration parameters.

Learn more â

CONFIG RESETSTAT

Resets the server's statistics.

Learn more â

CONFIG REWRITE

Persists the effective configuration to file.

Learn more â

CONFIG SET

Sets configuration parameters in-flight.

Learn more â

COPY

Copies the value of a key to a new key.

Learn more â

DBSIZE

Returns the number of keys in the database.

Learn more â

DECR

Decrements the integer value of a key by one. Uses 0 as initial value if the key doesn't exist.

Learn more â

DECRBY

Decrements a number from the integer value of a key. Uses 0 as initial value if the key doesn't exist.

Learn more â

DEL

Deletes one or more keys.

Learn more â

DELEX

Conditionally removes the specified key based on value or hash digest comparison.

Learn more â

DIGEST

Returns the hash digest of a string value as a hexadecimal string.

Learn more â

DISCARD

Discards a transaction.

Learn more â

DUMP

Returns a serialized representation of the value stored at a key.

Learn more â

ECHO

Returns the given string.

Learn more â

EVAL

Executes a server-side Lua script.

Learn more â

EVAL_RO

Executes a read-only server-side Lua script.

Learn more â

EVALSHA

Executes a server-side Lua script by SHA1 digest.

Learn more â

EVALSHA_RO

Executes a read-only server-side Lua script by SHA1 digest.

Learn more â

EXEC

Executes all commands in a transaction.

Learn more â

EXISTS

Determines whether one or more keys exist.

Learn more â

EXPIRE

Sets the expiration time of a key in seconds.

Learn more â

EXPIREAT

Sets the expiration time of a key to a Unix timestamp.

Learn more â

EXPIRETIME

Returns the expiration time of a key as a Unix timestamp.

Learn more â

FAILOVER

Starts a coordinated failover from a server to one of its replicas.

Learn more â

FCALL

Invokes a function.

Learn more â

FCALL_RO

Invokes a read-only function.

Learn more â

FLUSHALL

Removes all keys from all databases.

Learn more â

FLUSHDB

Remove all keys from the current database.

Learn more â

FT._LIST

Returns a list of all existing indexes

Learn more â

FT.AGGREGATE

Run a search query on an index and perform aggregate transformations on the results

Learn more â

FT.ALIASADD

Adds an alias to the index

Learn more â

FT.ALIASDEL

Deletes an alias from the index

Learn more â

FT.ALIASUPDATE

Adds or updates an alias to the index

Learn more â

FT.ALTER

Adds a new field to the index

Learn more â

FT.CONFIG GET

Deprecated

Use CONFIG GET instead

Retrieves runtime configuration options

Learn more â

FT.CONFIG SET

Deprecated

Use CONFIG SET instead

Sets runtime configuration options

Learn more â

FT.CREATE

Creates an index with the given spec

Learn more â

FT.CURSOR DEL

Deletes a cursor

Learn more â

FT.CURSOR READ

Reads from a cursor

Learn more â

FT.DICTADD

Adds terms to a dictionary

Learn more â

FT.DICTDEL

Deletes terms from a dictionary

Learn more â

FT.DICTDUMP

Dumps all terms in the given dictionary

Learn more â

FT.DROPINDEX

Deletes the index

Learn more â

FT.EXPLAIN

Returns the execution plan for a complex query

Learn more â

FT.EXPLAINCLI

Returns the execution plan for a complex query

Learn more â

FT.HYBRID

Performs hybrid search combining text search and vector similarity search

Learn more â

FT.INFO

Returns information and statistics on the index

Learn more â

FT.PROFILE

Performs a `FT.SEARCH` or `FT.AGGREGATE` command and collects performance information

Learn more â

FT.SEARCH

Searches the index with a textual query, returning either documents or just ids

Learn more â

FT.SPELLCHECK

Performs spelling correction on a query, returning suggestions for misspelled terms

Learn more â

FT.SUGADD

Adds a suggestion string to an auto-complete suggestion dictionary

Learn more â

FT.SUGDEL

Deletes a string from a suggestion index

Learn more â

FT.SUGGET

Gets completion suggestions for a prefix

Learn more â

FT.SUGLEN

Gets the size of an auto-complete suggestion dictionary

Learn more â

FT.SYNDUMP

Dumps the contents of a synonym group

Learn more â

FT.SYNUPDATE

Creates or updates a synonym group with additional terms

Learn more â

FT.TAGVALS

Deprecated

Returns the distinct tags indexed in a Tag field

Learn more â

FUNCTION DELETE

Deletes a library and its functions.

Learn more â

FUNCTION DUMP

Dumps all libraries into a serialized binary payload.

Learn more â

FUNCTION FLUSH

Deletes all libraries and functions.

Learn more â

FUNCTION KILL

Terminates a function during execution.

Learn more â

FUNCTION LIST

Returns information about all libraries.

Learn more â

FUNCTION LOAD

Creates a library.

Learn more â

FUNCTION RESTORE

Restores all libraries from a payload.

Learn more â

FUNCTION STATS

Returns information about a function during execution.

Learn more â

GEOADD

Adds one or more members to a geospatial index. The key is created if it doesn't exist.

Learn more â

GEODIST

Returns the distance between two members of a geospatial index.

Learn more â

GEOHASH

Returns members from a geospatial index as geohash strings.

Learn more â

GEOPOS

Returns the longitude and latitude of members from a geospatial index.

Learn more â

GEORADIUS

Deprecated

Use GEOSEARCH and GEOSEARCHSTORE with the BYRADIUS argument instead

Queries a geospatial index for members within a distance from a coordinate, optionally stores the result.

Learn more â

GEORADIUS_RO

Deprecated

Use GEOSEARCH with the BYRADIUS argument instead

Returns members from a geospatial index that are within a distance from a coordinate.

Learn more â

GEORADIUSBYMEMBER

Deprecated

Use GEOSEARCH and GEOSEARCHSTORE with the BYRADIUS and FROMMEMBER arguments instead

Queries a geospatial index for members within a distance from a member, optionally stores the result.

Learn more â

GEORADIUSBYMEMBER_RO

Deprecated

Use GEOSEARCH with the BYRADIUS and FROMMEMBER arguments instead

Returns members from a geospatial index that are within a distance from a member.

Learn more â

GEOSEARCH

Queries a geospatial index for members inside an area of a box or a circle.

Learn more â

GEOSEARCHSTORE

Queries a geospatial index for members inside an area of a box or a circle, optionally stores the result.

Learn more â

GET

Returns the string value of a key.

Learn more â

GETBIT

Returns a bit value by offset.

Learn more â

GETDEL

Returns the string value of a key after deleting the key.

Learn more â

GETEX

Returns the string value of a key after setting its expiration time.

Learn more â

GETRANGE

Returns a substring of the string stored at a key.

Learn more â

GETSET

Deprecated

Use SET with the !GET argument instead

Returns the previous string value of a key after setting it to a new value.

Learn more â

HDEL

Deletes one or more fields and their values from a hash. Deletes the hash if no fields remain.

Learn more â

HELLO

Handshakes with the Redis server.

Learn more â

HEXISTS

Determines whether a field exists in a hash.

Learn more â

HEXPIRE

Set expiry for hash field using relative time to expire (seconds)

Learn more â

HEXPIREAT

Set expiry for hash field using an absolute Unix timestamp (seconds)

Learn more â

HEXPIRETIME

Returns the expiration time of a hash field as a Unix timestamp, in seconds.

Learn more â

HGET

Returns the value of a field in a hash.

Learn more â

HGETALL

Returns all fields and values in a hash.

Learn more â

HGETDEL

Returns the value of a field and deletes it from the hash.

Learn more â

HGETEX

Get the value of one or more fields of a given hash key, and optionally set their expiration.

Learn more â

HINCRBY

Increments the integer value of a field in a hash by a number. Uses 0 as initial value if the field doesn't exist.

Learn more â

HINCRBYFLOAT

Increments the floating point value of a field by a number. Uses 0 as initial value if the field doesn't exist.

Learn more â

HKEYS

Returns all fields in a hash.

Learn more â

HLEN

Returns the number of fields in a hash.

Learn more â

HMGET

Returns the values of all fields in a hash.

Learn more â

HMSET

Deprecated

Use HSET with multiple field-value pairs instead

Sets the values of multiple fields.

Learn more â

HOTKEYS

A container for hotkeys tracking commands.

Learn more â

HOTKEYS GET

Returns lists of top K hotkeys depending on metrics chosen in HOTKEYS START command.

Learn more â

HOTKEYS RESET

Release the resources used for hotkey tracking.

Learn more â

HOTKEYS START

Starts hotkeys tracking.

Learn more â

HOTKEYS STOP

Stops hotkeys tracking.

Learn more â

HPERSIST

Removes the expiration time for each specified field

Learn more â

HPEXPIRE

Set expiry for hash field using relative time to expire (milliseconds)

Learn more â

HPEXPIREAT

Set expiry for hash field using an absolute Unix timestamp (milliseconds)

Learn more â

HPEXPIRETIME

Returns the expiration time of a hash field as a Unix timestamp, in msec.

Learn more â

HPTTL

Returns the TTL in milliseconds of a hash field.

Learn more â

HRANDFIELD

Returns one or more random fields from a hash.

Learn more â

HSCAN

Iterates over fields and values of a hash.

Learn more â

HSET

Creates or modifies the value of a field in a hash.

Learn more â

HSETEX

Set the value of one or more fields of a given hash key, and optionally set their expiration.

Learn more â

HSETNX

Sets the value of a field in a hash only when the field doesn't exist.

Learn more â

HSTRLEN

Returns the length of the value of a field.

Learn more â

HTTL

Returns the TTL in seconds of a hash field.

Learn more â

HVALS

Returns all values in a hash.

Learn more â

INCR

Increments the integer value of a key by one. Uses 0 as initial value if the key doesn't exist.

Learn more â

INCRBY

Increments the integer value of a key by a number. Uses 0 as initial value if the key doesn't exist.

Learn more â

INCRBYFLOAT

Increment the floating point value of a key by a number. Uses 0 as initial value if the key doesn't exist.

Learn more â

INFO

Returns information and statistics about the server.

Learn more â

JSON.ARRAPPEND

Append one or more json values into the array at path after the last element in it.

Learn more â

JSON.ARRINDEX

Returns the index of the first occurrence of a JSON scalar value in the array at path

Learn more â

JSON.ARRINSERT

Inserts the JSON scalar(s) value at the specified index in the array at path

Learn more â

JSON.ARRLEN

Returns the length of the array at path

Learn more â

JSON.ARRPOP

Removes and returns the element at the specified index in the array at path

Learn more â

JSON.ARRTRIM

Trims the array at path to contain only the specified inclusive range of indices from start to stop

Learn more â

JSON.CLEAR

Clears all values from an array or an object and sets numeric values to `0`

Learn more â

JSON.DEBUG

Debugging container command

Learn more â

JSON.DEBUG MEMORY

Reports the size in bytes of a key

Learn more â

JSON.DEL

Deletes a value

Learn more â

JSON.FORGET

Deletes a value

Learn more â

JSON.GET

Gets the value at one or more paths in JSON serialized form

Learn more â

JSON.MERGE

Merges a given JSON value into matching paths. Consequently, JSON values at matching paths are updated, deleted, or expanded with new children

Learn more â

JSON.MGET

Returns the values at a path from one or more keys

Learn more â

JSON.MSET

Sets or updates the JSON value of one or more keys

Learn more â

JSON.NUMINCRBY

Increments the numeric value at path by a value

Learn more â

JSON.NUMMULTBY

Multiplies the numeric value at path by a value

Learn more â

JSON.OBJKEYS

Returns the key names of JSON objects at the paths matching a given path expression

Learn more â

JSON.OBJLEN

Returns the number of keys in JSON objects at the paths matching a given path expression

Learn more â

JSON.RESP

Returns the JSON value at path in Redis Serialization Protocol (RESP)

Learn more â

JSON.SET

Sets or updates the JSON value at a path

Learn more â

JSON.STRAPPEND

Appends a string to JSON strings at the paths matching a given path expression

Learn more â

JSON.STRLEN

Returns the length of JSON strings at the paths matching a given path expression

Learn more â

JSON.TOGGLE

Toggles a boolean value

Learn more â

JSON.TYPE

Returns the type of the JSON value at path

Learn more â

KEYS

Returns all key names that match a pattern.

Learn more â

LASTSAVE

Returns the Unix timestamp of the last successful save to disk.

Learn more â

LATENCY DOCTOR

Returns a human-readable latency analysis report.

Learn more â

LATENCY GRAPH

Returns a latency graph for an event.

Learn more â

LATENCY HISTOGRAM

Returns the cumulative distribution of latencies of a subset or all commands.

Learn more â

LATENCY HISTORY

Returns timestamp-latency samples for an event.

Learn more â

LATENCY LATEST

Returns the latest latency samples for all events.

Learn more â

LATENCY RESET

Resets the latency data for one or more events.

Learn more â

LCS

Finds the longest common substring.

Learn more â

LINDEX

Returns an element from a list by its index.

Learn more â

LINSERT

Inserts an element before or after another element in a list.

Learn more â

LLEN

Returns the length of a list.

Learn more â

LMOVE

Returns an element after popping it from one list and pushing it to another. Deletes the list if the last element was moved.

Learn more â

LMPOP

Returns multiple elements from a list after removing them. Deletes the list if the last element was popped.

Learn more â

LOLWUT

Displays computer art and the Redis version

Learn more â

LPOP

Returns the first elements in a list after removing it. Deletes the list if the last element was popped.

Learn more â

LPOS

Returns the index of matching elements in a list.

Learn more â

LPUSH

Prepends one or more elements to a list. Creates the key if it doesn't exist.

Learn more â

LPUSHX

Prepends one or more elements to a list only when the list exists.

Learn more â

LRANGE

Returns a range of elements from a list.

Learn more â

LREM

Removes elements from a list. Deletes the list if the last element was removed.

Learn more â

LSET

Sets the value of an element in a list by its index.

Learn more â

LTRIM

Removes elements from both ends a list. Deletes the list if all elements were trimmed.

Learn more â

MEMORY DOCTOR

Outputs a memory problems report.

Learn more â

MEMORY MALLOC-STATS

Returns the allocator statistics.

Learn more â

MEMORY PURGE

Asks the allocator to release memory.

Learn more â

MEMORY STATS

Returns details about memory usage.

Learn more â

MEMORY USAGE

Estimates the memory usage of a key.

Learn more â

MGET

Atomically returns the string values of one or more keys.

Learn more â

MIGRATE

Atomically transfers a key from one Redis instance to another.

Learn more â

MODULE LIST

Returns all loaded modules.

Learn more â

MODULE LOAD

Loads a module.

Learn more â

MODULE LOADEX

Loads a module using extended parameters.

Learn more â

MODULE UNLOAD

Unloads a module.

Learn more â

MONITOR

Listens for all requests received by the server in real-time.

Learn more â

MOVE

Moves a key to another database.

Learn more â

MSET

Atomically creates or modifies the string values of one or more keys.

Learn more â

MSETEX

Atomically sets multiple string keys with a shared expiration in a single operation.

Learn more â

MSETNX

Atomically modifies the string values of one or more keys only when all keys don't exist.

Learn more â

MULTI

Starts a transaction.

Learn more â

OBJECT ENCODING

Returns the internal encoding of a Redis object.

Learn more â

OBJECT FREQ

Returns the logarithmic access frequency counter of a Redis object.

Learn more â

OBJECT IDLETIME

Returns the time since the last access to a Redis object.

Learn more â

OBJECT REFCOUNT

Returns the reference count of a value of a key.

Learn more â

PERSIST

Removes the expiration time of a key.

Learn more â

PEXPIRE

Sets the expiration time of a key in milliseconds.

Learn more â

PEXPIREAT

Sets the expiration time of a key to a Unix milliseconds timestamp.

Learn more â

PEXPIRETIME

Returns the expiration time of a key as a Unix milliseconds timestamp.

Learn more â

PFADD

Adds elements to a HyperLogLog key. Creates the key if it doesn't exist.

Learn more â

PFCOUNT

Returns the approximated cardinality of the set(s) observed by the HyperLogLog key(s).

Learn more â

PFDEBUG

Internal commands for debugging HyperLogLog values.

Learn more â

PFMERGE

Merges one or more HyperLogLog values into a single key.

Learn more â

PFSELFTEST

An internal command for testing HyperLogLog values.

Learn more â

PING

Returns the server's liveliness response.

Learn more â

PSETEX

Deprecated

Use SET with the PX argument instead

Sets both string value and expiration time in milliseconds of a key. The key is created if it doesn't exist.

Learn more â

PSUBSCRIBE

Listens for messages published to channels that match one or more patterns.

Learn more â

PSYNC

An internal command used in replication.

Learn more â

PTTL

Returns the expiration time in milliseconds of a key.

Learn more â

PUBLISH

Posts a message to a channel.

Learn more â

PUBSUB CHANNELS

Returns the active channels.

Learn more â

PUBSUB NUMPAT

Returns a count of unique pattern subscriptions.

Learn more â

PUBSUB NUMSUB

Returns a count of subscribers to channels.

Learn more â

PUBSUB SHARDCHANNELS

Returns the active shard channels.

Learn more â

PUBSUB SHARDNUMSUB

Returns the count of subscribers of shard channels.

Learn more â

PUNSUBSCRIBE

Stops listening to messages published to channels that match one or more patterns.

Learn more â

QUIT

Deprecated

Use just closing the connection instead

Closes the connection.

Learn more â

RANDOMKEY

Returns a random key name from the database.

Learn more â

READONLY

Enables read-only queries for a connection to a Redis Cluster replica node.

Learn more â

READWRITE

Enables read-write queries for a connection to a Reids Cluster replica node.

Learn more â

RENAME

Renames a key and overwrites the destination.

Learn more â

RENAMENX

Renames a key only when the target key name doesn't exist.

Learn more â

REPLCONF

An internal command for configuring the replication stream.

Learn more â

REPLICAOF

Configures a server as replica of another, or promotes it to a master.

Learn more â

RESET

Resets the connection.

Learn more â

RESTORE

Creates a key from the serialized representation of a value.

Learn more â

RESTORE-ASKING

An internal command for migrating keys in a cluster.

Learn more â

ROLE

Returns the replication role.

Learn more â

RPOP

Returns and removes the last elements of a list. Deletes the list if the last element was popped.

Learn more â

RPOPLPUSH

Deprecated

Use LMOVE with the RIGHT and LEFT arguments instead

Returns the last element of a list after removing and pushing it to another list. Deletes the list if the last element was popped.

Learn more â

RPUSH

Appends one or more elements to a list. Creates the key if it doesn't exist.

Learn more â

RPUSHX

Appends an element to a list only when the list exists.

Learn more â

SADD

Adds one or more members to a set. Creates the key if it doesn't exist.

Learn more â

SAVE

Synchronously saves the database(s) to disk.

Learn more â

SCAN

Iterates over the key names in the database.

Learn more â

SCARD

Returns the number of members in a set.

Learn more â

SCRIPT DEBUG

Sets the debug mode of server-side Lua scripts.

Learn more â

SCRIPT EXISTS

Determines whether server-side Lua scripts exist in the script cache.

Learn more â

SCRIPT FLUSH

Removes all server-side Lua scripts from the script cache.

Learn more â

SCRIPT KILL

Terminates a server-side Lua script during execution.

Learn more â

SCRIPT LOAD

Loads a server-side Lua script to the script cache.

Learn more â

SDIFF

Returns the difference of multiple sets.

Learn more â

SDIFFSTORE

Stores the difference of multiple sets in a key.

Learn more â

SELECT

Changes the selected database.

Learn more â

SET

Sets the string value of a key, ignoring its type. The key is created if it doesn't exist.

Learn more â

SETBIT

Sets or clears the bit at offset of the string value. Creates the key if it doesn't exist.

Learn more â

SETEX

Deprecated

Use SET with the EX argument instead

Sets the string value and expiration time of a key. Creates the key if it doesn't exist.

Learn more â

SETNX

Deprecated

Use SET with the NX argument instead

Set the string value of a key only when the key doesn't exist.

Learn more â

SETRANGE

Overwrites a part of a string value with another by an offset. Creates the key if it doesn't exist.

Learn more â

SHUTDOWN

Synchronously saves the database(s) to disk and shuts down the Redis server.

Learn more â

SINTER

Returns the intersect of multiple sets.

Learn more â

SINTERCARD

Returns the number of members of the intersect of multiple sets.

Learn more â

SINTERSTORE

Stores the intersect of multiple sets in a key.

Learn more â

SISMEMBER

Determines whether a member belongs to a set.

Learn more â

SLAVEOF

Deprecated

Use REPLICAOF instead

Sets a Redis server as a replica of another, or promotes it to being a master.

Learn more â

SLOWLOG GET

Returns the slow log's entries.

Learn more â

SLOWLOG LEN

Returns the number of entries in the slow log.

Learn more â

SLOWLOG RESET

Clears all entries from the slow log.

Learn more â

SMEMBERS

Returns all members of a set.

Learn more â

SMISMEMBER

Determines whether multiple members belong to a set.

Learn more â

SMOVE

Moves a member from one set to another.

Learn more â

SORT

Sorts the elements in a list, a set, or a sorted set, optionally storing the result.

Learn more â

SORT_RO

Returns the sorted elements of a list, a set, or a sorted set.

Learn more â

SPOP

Returns one or more random members from a set after removing them. Deletes the set if the last member was popped.

Learn more â

SPUBLISH

Post a message to a shard channel

Learn more â

SRANDMEMBER

Get one or multiple random members from a set

Learn more â

SREM

Removes one or more members from a set. Deletes the set if the last member was removed.

Learn more â

SSCAN

Iterates over members of a set.

Learn more â

SSUBSCRIBE

Listens for messages published to shard channels.

Learn more â

STRLEN

Returns the length of a string value.

Learn more â

SUBSCRIBE

Listens for messages published to channels.

Learn more â

SUBSTR

Deprecated

Use GETRANGE instead

Returns a substring from a string value.

Learn more â

SUNION

Returns the union of multiple sets.

Learn more â

SUNIONSTORE

Stores the union of multiple sets in a key.

Learn more â

SUNSUBSCRIBE

Stops listening to messages posted to shard channels.

Learn more â

SWAPDB

Swaps two Redis databases.

Learn more â

SYNC

An internal command used in replication.

Learn more â

TDIGEST.ADD

Adds one or more observations to a t-digest sketch

Learn more â

TDIGEST.BYRANK

Returns, for each input rank, an estimation of the value (floating-point) with that rank

Learn more â

TDIGEST.BYREVRANK

Returns, for each input reverse rank, an estimation of the value (floating-point) with that reverse rank

Learn more â

TDIGEST.CDF

Returns, for each input value, an estimation of the fraction (floating-point) of (observations smaller than the given value + half the observations equal to the given value)

Learn more â

TDIGEST.CREATE

Allocates memory and initializes a new t-digest sketch

Learn more â

TDIGEST.INFO

Returns information and statistics about a t-digest sketch

Learn more â

TDIGEST.MAX

Returns the maximum observation value from a t-digest sketch

Learn more â

TDIGEST.MERGE

Merges multiple t-digest sketches into a single sketch

Learn more â

TDIGEST.MIN

Returns the minimum observation value from a t-digest sketch

Learn more â

TDIGEST.QUANTILE

Returns, for each input fraction, an estimation of the value (floating point) that is smaller than the given fraction of observations

Learn more â

TDIGEST.RANK

Returns, for each input value (floating-point), the estimated rank of the value (the number of observations in the sketch that are smaller than the value + half the number of observations that are equal to the value)

Learn more â

TDIGEST.RESET

Resets a t-digest sketch: empty the sketch and re-initializes it.

Learn more â

TDIGEST.REVRANK

Returns, for each input value (floating-point), the estimated reverse rank of the value (the number of observations in the sketch that are larger than the value + half the number of observations that are equal to the value)

Learn more â

TDIGEST.TRIMMED_MEAN

Returns an estimation of the mean value from the sketch, excluding observation values outside the low and high cutoff quantiles

Learn more â

TIME

Returns the server time.

Learn more â

TOPK.ADD

Adds an item to a Top-k sketch. Multiple items can be added at the same time.

Learn more â

TOPK.COUNT

Return the count for one or more items are in a sketch

Learn more â

TOPK.INCRBY

Increases the count of one or more items by increment

Learn more â

TOPK.INFO

Returns information about a sketch

Learn more â

TOPK.LIST

Return full list of items in Top K list

Learn more â

TOPK.QUERY

Checks whether one or more items are in a sketch

Learn more â

TOPK.RESERVE

Initializes a TopK with specified parameters

Learn more â

TOUCH

Returns the number of existing keys out of those specified after updating the time they were last accessed.

Learn more â

TS.ADD

Append a sample to a time series

Learn more â

TS.ALTER

Update the retention, chunk size, duplicate policy, and labels of an existing time series

Learn more â

TS.CREATE

Create a new time series

Learn more â

TS.CREATERULE

Create a compaction rule

Learn more â

TS.DECRBY

Decrease the value of the sample with the maximum existing timestamp, or create a new sample with a value equal to the value of the sample with the maximum existing timestamp with a given decrement

Learn more â

TS.DEL

Delete all samples between two timestamps for a given time series

Learn more â

TS.DELETERULE

Delete a compaction rule

Learn more â

TS.GET

Get the sample with the highest timestamp from a given time series

Learn more â

TS.INCRBY

Increase the value of the sample with the maximum existing timestamp, or create a new sample with a value equal to the value of the sample with the maximum existing timestamp with a given increment

Learn more â

TS.INFO

Returns information and statistics for a time series

Learn more â

TS.MADD

Append new samples to one or more time series

Learn more â

TS.MGET

Get the sample with the highest timestamp from each time series matching a specific filter

Learn more â

TS.MRANGE

Query a range across multiple time series by filters in forward direction

Learn more â

TS.MREVRANGE

Query a range across multiple time-series by filters in reverse direction

Learn more â

TS.QUERYINDEX

Get all time series keys matching a filter list

Learn more â

TS.RANGE

Query a range in forward direction

Learn more â

TS.REVRANGE

Query a range in reverse direction

Learn more â

TTL

Returns the expiration time in seconds of a key.

Learn more â

TYPE

Determines the type of value stored at a key.

Learn more â

UNLINK

Asynchronously deletes one or more keys.

Learn more â

UNSUBSCRIBE

Stops listening to messages posted to channels.

Learn more â

UNWATCH

Forgets about watched keys of a transaction.

Learn more â

VADD

Add a new element to a vector set, or update its vector if it already exists.

Learn more â

VCARD

Return the number of elements in a vector set.

Learn more â

VDIM

Return the dimension of vectors in the vector set.

Learn more â

VEMB

Return the vector associated with an element.

Learn more â

VGETATTR

Retrieve the JSON attributes of elements.

Learn more â

VINFO

Return information about a vector set.

Learn more â

VISMEMBER

Check if an element exists in a vector set.

Learn more â

VLINKS

Return the neighbors of an element at each layer in the HNSW graph.

Learn more â

VRANDMEMBER

Return one or multiple random members from a vector set.

Learn more â

VRANGE

Return elements in a lexicographical range

Learn more â

VREM

Remove an element from a vector set.

Learn more â

VSETATTR

Associate or remove the JSON attributes of elements.

Learn more â

VSIM

Return elements by vector similarity.

Learn more â

WAIT

Blocks until the asynchronous replication of all preceding write commands sent by the connection is completed.

Learn more â

WAITAOF

Blocks until all of the preceding write commands sent by the connection are written to the append-only file of the master and/or replicas.

Learn more â

WATCH

Monitors changes to keys to determine the execution of a transaction.

Learn more â

XACK

Returns the number of messages that were successfully acknowledged by the consumer group member of a stream.

Learn more â

XACKDEL

Acknowledges and conditionally deletes one or multiple entries for a stream consumer group.

Learn more â

XADD

Appends a new message to a stream. Creates the key if it doesn't exist.

Learn more â

XAUTOCLAIM

Changes, or acquires, ownership of messages in a consumer group, as if the messages were delivered to as consumer group member.

Learn more â

XCFGSET

Sets the IDMP configuration parameters for a stream.

Learn more â

XCLAIM

Changes, or acquires, ownership of a message in a consumer group, as if the message was delivered a consumer group member.

Learn more â

XDEL

Returns the number of messages after removing them from a stream.

Learn more â

XDELEX

Deletes one or multiple entries from the stream.

Learn more â

XGROUP CREATE

Creates a consumer group.

Learn more â

XGROUP CREATECONSUMER

Creates a consumer in a consumer group.

Learn more â

XGROUP DELCONSUMER

Deletes a consumer from a consumer group.

Learn more â

XGROUP DESTROY

Destroys a consumer group.

Learn more â

XGROUP SETID

Sets the last-delivered ID of a consumer group.

Learn more â

XINFO CONSUMERS

Returns a list of the consumers in a consumer group.

Learn more â

XINFO GROUPS

Returns a list of the consumer groups of a stream.

Learn more â

XINFO STREAM

Returns information about a stream.

Learn more â

XLEN

Return the number of messages in a stream.

Learn more â

XPENDING

Returns the information and entries from a stream consumer group's pending entries list.

Learn more â

XRANGE

Returns the messages from a stream within a range of IDs.

Learn more â

XREAD

Returns messages from multiple streams with IDs greater than the ones requested. Blocks until a message is available otherwise.

Learn more â

XREADGROUP

Returns new or historical messages from a stream for a consumer in a group. Blocks until a message is available otherwise.

Learn more â

XREVRANGE

Returns the messages from a stream within a range of IDs in reverse order.

Learn more â

XSETID

An internal command for replicating stream values.

Learn more â

XTRIM

Deletes messages from the beginning of a stream.

Learn more â

ZADD

Adds one or more members to a sorted set, or updates their scores. Creates the key if it doesn't exist.

Learn more â

ZCARD

Returns the number of members in a sorted set.

Learn more â

ZCOUNT

Returns the count of members in a sorted set that have scores within a range.

Learn more â

ZDIFF

Returns the difference between multiple sorted sets.

Learn more â

ZDIFFSTORE

Stores the difference of multiple sorted sets in a key.

Learn more â

ZINCRBY

Increments the score of a member in a sorted set.

Learn more â

ZINTER

Returns the intersect of multiple sorted sets.

Learn more â

ZINTERCARD

Returns the number of members of the intersect of multiple sorted sets.

Learn more â

ZINTERSTORE

Stores the intersect of multiple sorted sets in a key.

Learn more â

ZLEXCOUNT

Returns the number of members in a sorted set within a lexicographical range.

Learn more â

ZMPOP

Returns the highest- or lowest-scoring members from one or more sorted sets after removing them. Deletes the sorted set if the last member was popped.

Learn more â

ZMSCORE

Returns the score of one or more members in a sorted set.

Learn more â

ZPOPMAX

Returns the highest-scoring members from a sorted set after removing them. Deletes the sorted set if the last member was popped.

Learn more â

ZPOPMIN

Returns the lowest-scoring members from a sorted set after removing them. Deletes the sorted set if the last member was popped.

Learn more â

ZRANDMEMBER

Returns one or more random members from a sorted set.

Learn more â

ZRANGE

Returns members in a sorted set within a range of indexes.

Learn more â

ZRANGEBYLEX

Deprecated

Use ZRANGE with the BYLEX argument instead

Returns members in a sorted set within a lexicographical range.

Learn more â

ZRANGEBYSCORE

Deprecated

Use ZRANGE with the BYSCORE argument instead

Returns members in a sorted set within a range of scores.

Learn more â

ZRANGESTORE

Stores a range of members from sorted set in a key.

Learn more â

ZRANK

Returns the index of a member in a sorted set ordered by ascending scores.

Learn more â

ZREM

Removes one or more members from a sorted set. Deletes the sorted set if all members were removed.

Learn more â

ZREMRANGEBYLEX

Removes members in a sorted set within a lexicographical range. Deletes the sorted set if all members were removed.

Learn more â

ZREMRANGEBYRANK

Removes members in a sorted set within a range of indexes. Deletes the sorted set if all members were removed.

Learn more â

ZREMRANGEBYSCORE

Removes members in a sorted set within a range of scores. Deletes the sorted set if all members were removed.

Learn more â

ZREVRANGE

Deprecated

Use ZRANGE with the REV argument instead

Returns members in a sorted set within a range of indexes in reverse order.

Learn more â

ZREVRANGEBYLEX

Deprecated

Use ZRANGE with the REV and BYLEX arguments instead

Returns members in a sorted set within a lexicographical range in reverse order.

Learn more â

ZREVRANGEBYSCORE

Deprecated

Use ZRANGE with the REV and BYSCORE arguments instead

Returns members in a sorted set within a range of scores in reverse order.

Learn more â

ZREVRANK

Returns the index of a member in a sorted set ordered by descending scores.

Learn more â

ZSCAN

Iterates over members and scores of a sorted set.

Learn more â

ZSCORE

Returns the score of a member in a sorted set.

Learn more â

ZUNION

Returns the union of multiple sorted sets.

Learn more â

ZUNIONSTORE

Stores the union of multiple sorted sets in a key.

Learn more â
