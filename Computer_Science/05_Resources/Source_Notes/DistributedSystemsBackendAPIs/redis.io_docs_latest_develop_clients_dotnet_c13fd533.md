Title: NRedisStack guide (C#/.NET) | Docs
Mapped Topic: Caching and in-memory data structures
Source URL: https://redis.io/docs/latest/develop/clients/dotnet/
Source Type: official_docs
Trust Score: 94
Fetched At: 2026-04-17T07:08:52+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

# NRedisStack guide (C#/.NET)

Connect your .NET application to a Redis database

[NRedisStack](https://github.com/redis/NRedisStack) is the .NET client for Redis.
The sections below explain how to install `NRedisStack`

and connect your application
to a Redis database.

`NRedisStack`

requires a running Redis server. See [here](https://redis.io/docs/latest/operate/oss_and_stack/install/) for Redis Open Source installation instructions.

You can also access Redis with an object-mapping client interface. See
[Redis OM for .NET](https://redis.io/docs/latest/integrate/redisom-for-net/)
for more information.

##
Install
[
](https://redis.io#install)

Using the `dotnet`

CLI, run:

```
dotnet add package NRedisStack
```

##
Connect and test
[
](https://redis.io#connect-and-test)

Add the following imports to your source file:

```
using NRedisStack;
using NRedisStack.RedisStackCommands;
using StackExchange.Redis;
public class SyncLandingExample
{
public void Run()
{
var muxer = ConnectionMultiplexer.Connect("localhost:6379");
var db = muxer.GetDatabase();
db.StringSet("foo", "bar");
Console.WriteLine(db.StringGet("foo")); // >>> bar
var hash = new HashEntry[] {
new HashEntry("name", "John"),
new HashEntry("surname", "Smith"),
new HashEntry("company", "Redis"),
new HashEntry("age", "29"),
};
db.HashSet("user-session:123", hash);
var hashFields = db.HashGetAll("user-session:123");
Console.WriteLine(String.Join("; ", hashFields));
// >>> name: John; surname: Smith; company: Redis; age: 29
}
}
```

```
using NRedisStack;
using NRedisStack.RedisStackCommands;
using StackExchange.Redis;
public class AsyncLandingExample
{
public async Task Run()
{
var muxer = await ConnectionMultiplexer.ConnectAsync("localhost:6379");
var db = muxer.GetDatabase();
await db.StringSetAsync("foo", "bar");
string? fooResult = await db.StringGetAsync("foo");
Console.WriteLine(fooResult); // >>> bar
var hash = new HashEntry[] {
new HashEntry("name", "John"),
new HashEntry("surname", "Smith"),
new HashEntry("company", "Redis"),
new HashEntry("age", "29"),
};
await db.HashSetAsync("user-session:123", hash);
var hashFields = await db.HashGetAllAsync("user-session:123");
Console.WriteLine(String.Join("; ", hashFields));
// >>> name: John; surname: Smith; company: Redis; age: 29
}
}
```

Connect to localhost on port 6379. The client supports both synchronous and asynchronous commands.

```
using NRedisStack;
using NRedisStack.RedisStackCommands;
using StackExchange.Redis;
public class SyncLandingExample
{
public void Run()
{
var muxer = ConnectionMultiplexer.Connect("localhost:6379");
var db = muxer.GetDatabase();
db.StringSet("foo", "bar");
Console.WriteLine(db.StringGet("foo")); // >>> bar
var hash = new HashEntry[] {
new HashEntry("name", "John"),
new HashEntry("surname", "Smith"),
new HashEntry("company", "Redis"),
new HashEntry("age", "29"),
};
db.HashSet("user-session:123", hash);
var hashFields = db.HashGetAll("user-session:123");
Console.WriteLine(String.Join("; ", hashFields));
// >>> name: John; surname: Smith; company: Redis; age: 29
}
}
```

```
using NRedisStack;
using NRedisStack.RedisStackCommands;
using StackExchange.Redis;
public class AsyncLandingExample
{
public async Task Run()
{
var muxer = await ConnectionMultiplexer.ConnectAsync("localhost:6379");
var db = muxer.GetDatabase();
await db.StringSetAsync("foo", "bar");
string? fooResult = await db.StringGetAsync("foo");
Console.WriteLine(fooResult); // >>> bar
var hash = new HashEntry[] {
new HashEntry("name", "John"),
new HashEntry("surname", "Smith"),
new HashEntry("company", "Redis"),
new HashEntry("age", "29"),
};
await db.HashSetAsync("user-session:123", hash);
var hashFields = await db.HashGetAllAsync("user-session:123");
Console.WriteLine(String.Join("; ", hashFields));
// >>> name: John; surname: Smith; company: Redis; age: 29
}
}
```

You can test the connection by storing and retrieving a simple string.

```
using NRedisStack;
using NRedisStack.RedisStackCommands;
using StackExchange.Redis;
public class SyncLandingExample
{
public void Run()
{
var muxer = ConnectionMultiplexer.Connect("localhost:6379");
var db = muxer.GetDatabase();
db.StringSet("foo", "bar");
Console.WriteLine(db.StringGet("foo")); // >>> bar
var hash = new HashEntry[] {
new HashEntry("name", "John"),
new HashEntry("surname", "Smith"),
new HashEntry("company", "Redis"),
new HashEntry("age", "29"),
};
db.HashSet("user-session:123", hash);
var hashFields = db.HashGetAll("user-session:123");
Console.WriteLine(String.Join("; ", hashFields));
// >>> name: John; surname: Smith; company: Redis; age: 29
}
}
```

```
using NRedisStack;
using NRedisStack.RedisStackCommands;
using StackExchange.Redis;
public class AsyncLandingExample
{
public async Task Run()
{
var muxer = await ConnectionMultiplexer.ConnectAsync("localhost:6379");
var db = muxer.GetDatabase();
await db.StringSetAsync("foo", "bar");
string? fooResult = await db.StringGetAsync("foo");
Console.WriteLine(fooResult); // >>> bar
var hash = new HashEntry[] {
new HashEntry("name", "John"),
new HashEntry("surname", "Smith"),
new HashEntry("company", "Redis"),
new HashEntry("age", "29"),
};
await db.HashSetAsync("user-session:123", hash);
var hashFields = await db.HashGetAllAsync("user-session:123");
Console.WriteLine(String.Join("; ", hashFields));
// >>> name: John; surname: Smith; company: Redis; age: 29
}
}
```

Store and retrieve a HashMap.

```
using NRedisStack;
using NRedisStack.RedisStackCommands;
using StackExchange.Redis;
public class SyncLandingExample
{
public void Run()
{
var muxer = ConnectionMultiplexer.Connect("localhost:6379");
var db = muxer.GetDatabase();
db.StringSet("foo", "bar");
Console.WriteLine(db.StringGet("foo")); // >>> bar
var hash = new HashEntry[] {
new HashEntry("name", "John"),
new HashEntry("surname", "Smith"),
new HashEntry("company", "Redis"),
new HashEntry("age", "29"),
};
db.HashSet("user-session:123", hash);
var hashFields = db.HashGetAll("user-session:123");
Console.WriteLine(String.Join("; ", hashFields));
// >>> name: John; surname: Smith; company: Redis; age: 29
}
}
```

```
using NRedisStack;
using NRedisStack.RedisStackCommands;
using StackExchange.Redis;
public class AsyncLandingExample
{
public async Task Run()
{
var muxer = await ConnectionMultiplexer.ConnectAsync("localhost:6379");
var db = muxer.GetDatabase();
await db.StringSetAsync("foo", "bar");
string? fooResult = await db.StringGetAsync("foo");
Console.WriteLine(fooResult); // >>> bar
var hash = new HashEntry[] {
new HashEntry("name", "John"),
new HashEntry("surname", "Smith"),
new HashEntry("company", "Redis"),
new HashEntry("age", "29"),
};
await db.HashSetAsync("user-session:123", hash);
var hashFields = await db.HashGetAllAsync("user-session:123");
Console.WriteLine(String.Join("; ", hashFields));
// >>> name: John; surname: Smith; company: Redis; age: 29
}
}
```

##
Redis Open Source modules
[
](https://redis.io#redis-open-source-modules)

To access Redis Open Source capabilities, use the appropriate interface like this:

```
IBloomCommands bf = db.BF();
ICuckooCommands cf = db.CF();
ICmsCommands cms = db.CMS();
IGraphCommands graph = db.GRAPH();
ITopKCommands topk = db.TOPK();
ITdigestCommands tdigest = db.TDIGEST();
ISearchCommands ft = db.FT();
IJsonCommands json = db.JSON();
ITimeSeriesCommands ts = db.TS();
```

##
More information
[
](https://redis.io#more-information)

See the other pages in this section for more information and examples.
