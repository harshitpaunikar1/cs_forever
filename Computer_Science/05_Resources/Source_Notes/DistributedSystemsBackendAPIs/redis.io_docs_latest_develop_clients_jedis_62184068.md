Title: Jedis guide (Java) | Docs
Mapped Topic: Caching and in-memory data structures
Source URL: https://redis.io/docs/latest/develop/clients/jedis/
Source Type: official_docs
Trust Score: 94
Fetched At: 2026-04-17T07:08:58+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

# Jedis guide (Java)

Connect your Java application to a Redis database

[Jedis](https://github.com/redis/jedis) is a synchronous Java client for Redis.
Use [Lettuce](https://redis.io/docs/latest/develop/clients/lettuce/) if you need
a more advanced Java client that also supports asynchronous and reactive connections.
The sections below explain how to install `Jedis`

and connect your application
to a Redis database.

Jedis 7.2.0 introduced a new client connection API:

| New API class | Replaces | Use case |
|---|---|---|
`RedisClient` |
`UnifiedJedis` , `JedisPool` , `JedisPooled` |
Single connection (with connection pooling) |
`RedisClusterClient` |
`JedisCluster` |
Redis Cluster connections |
`RedisSentinelClient` |
`JedisSentinelPool` |
Redis Sentinel connections |

The old client classes are now considered deprecated.

`Jedis`

requires a running Redis server. See [here](https://redis.io/docs/latest/operate/oss_and_stack/install/) for Redis Open Source installation instructions.

##
Install
[
](https://redis.io#install)

To include `Jedis`

as a dependency in your application, edit the dependency file, as follows.

-
If you use

**Maven**:`<dependency> <groupId>redis.clients</groupId> <artifactId>jedis</artifactId> <version>7.2.0</version> </dependency>`

-
If you use

**Gradle**:`repositories { mavenCentral() } //... dependencies { implementation 'redis.clients:jedis:7.2.0' //... }`

-
If you use the JAR files, download the latest Jedis and Apache Commons Pool2 JAR files from

[Maven Central](https://central.sonatype.com/)or any other Maven repository. -
Build from

[source](https://github.com/redis/jedis)

##
Connect and test
[
](https://redis.io#connect-and-test)

Add the following imports to your source file:

```
import redis.clients.jedis.RedisClient;
import java.util.HashMap;
import java.util.Map;
public class LandingExample {
public void run() {
RedisClient jedis = new RedisClient("redis://localhost:6379");
String res1 = jedis.set("bike:1", "Deimos");
System.out.println(res1); // >>> OK
String res2 = jedis.get("bike:1");
System.out.println(res2); // >>> Deimos
Map<String, String> hash = new HashMap<>();
hash.put("name", "John");
hash.put("surname", "Smith");
hash.put("company", "Redis");
hash.put("age", "29");
Long res3 = jedis.hset("user-session:123", hash);
System.out.println(res3); // >>> 4
Map<String, String> res4 = jedis.hgetAll("user-session:123");
System.out.println(res4);
// >>> {name=John, surname=Smith, company=Redis, age=29}
jedis.close();
}
}
```

Connect to localhost on port 6379:

```
import redis.clients.jedis.RedisClient;
import java.util.HashMap;
import java.util.Map;
public class LandingExample {
public void run() {
RedisClient jedis = new RedisClient("redis://localhost:6379");
String res1 = jedis.set("bike:1", "Deimos");
System.out.println(res1); // >>> OK
String res2 = jedis.get("bike:1");
System.out.println(res2); // >>> Deimos
Map<String, String> hash = new HashMap<>();
hash.put("name", "John");
hash.put("surname", "Smith");
hash.put("company", "Redis");
hash.put("age", "29");
Long res3 = jedis.hset("user-session:123", hash);
System.out.println(res3); // >>> 4
Map<String, String> res4 = jedis.hgetAll("user-session:123");
System.out.println(res4);
// >>> {name=John, surname=Smith, company=Redis, age=29}
jedis.close();
}
}
```

After you have connected, you can check the connection by storing and
retrieving a simple [string](https://redis.io/docs/latest/develop/data-types/strings/) value:

```
import redis.clients.jedis.RedisClient;
import java.util.HashMap;
import java.util.Map;
public class LandingExample {
public void run() {
RedisClient jedis = new RedisClient("redis://localhost:6379");
String res1 = jedis.set("bike:1", "Deimos");
System.out.println(res1); // >>> OK
String res2 = jedis.get("bike:1");
System.out.println(res2); // >>> Deimos
Map<String, String> hash = new HashMap<>();
hash.put("name", "John");
hash.put("surname", "Smith");
hash.put("company", "Redis");
hash.put("age", "29");
Long res3 = jedis.hset("user-session:123", hash);
System.out.println(res3); // >>> 4
Map<String, String> res4 = jedis.hgetAll("user-session:123");
System.out.println(res4);
// >>> {name=John, surname=Smith, company=Redis, age=29}
jedis.close();
}
}
```

Store and retrieve a [hash](https://redis.io/docs/latest/develop/data-types/hashes/):

```
import redis.clients.jedis.RedisClient;
import java.util.HashMap;
import java.util.Map;
public class LandingExample {
public void run() {
RedisClient jedis = new RedisClient("redis://localhost:6379");
String res1 = jedis.set("bike:1", "Deimos");
System.out.println(res1); // >>> OK
String res2 = jedis.get("bike:1");
System.out.println(res2); // >>> Deimos
Map<String, String> hash = new HashMap<>();
hash.put("name", "John");
hash.put("surname", "Smith");
hash.put("company", "Redis");
hash.put("age", "29");
Long res3 = jedis.hset("user-session:123", hash);
System.out.println(res3); // >>> 4
Map<String, String> res4 = jedis.hgetAll("user-session:123");
System.out.println(res4);
// >>> {name=John, surname=Smith, company=Redis, age=29}
jedis.close();
}
}
```

Close the connection when you're done:

```
import redis.clients.jedis.RedisClient;
import java.util.HashMap;
import java.util.Map;
public class LandingExample {
public void run() {
RedisClient jedis = new RedisClient("redis://localhost:6379");
String res1 = jedis.set("bike:1", "Deimos");
System.out.println(res1); // >>> OK
String res2 = jedis.get("bike:1");
System.out.println(res2); // >>> Deimos
Map<String, String> hash = new HashMap<>();
hash.put("name", "John");
hash.put("surname", "Smith");
hash.put("company", "Redis");
hash.put("age", "29");
Long res3 = jedis.hset("user-session:123", hash);
System.out.println(res3); // >>> 4
Map<String, String> res4 = jedis.hgetAll("user-session:123");
System.out.println(res4);
// >>> {name=John, surname=Smith, company=Redis, age=29}
jedis.close();
}
}
```

##
More information
[
](https://redis.io#more-information)

`Jedis`

has a complete [API reference](https://www.javadoc.io/doc/redis.clients/jedis/latest/index.html) available on [javadoc.io/](https://javadoc.io/).
The `Jedis`

[GitHub repository](https://github.com/redis/jedis) also has useful docs
and examples including a page about handling
[failover with Jedis](https://github.com/redis/jedis/blob/master/docs/failover.md)

See also the other pages in this section for more information and examples:
