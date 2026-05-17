Title: Lettuce guide (Java) | Docs
Mapped Topic: Caching and in-memory data structures
Source URL: https://redis.io/docs/latest/develop/clients/lettuce/
Source Type: official_docs
Trust Score: 94
Fetched At: 2026-04-17T07:08:59+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

# Lettuce guide (Java)

Connect your Lettuce application to a Redis database

[Lettuce](https://github.com/redis/lettuce/tree/main/src/main) is an advanced Java client for Redis
that supports synchronous, asynchronous, and reactive connections.
If you only need synchronous connections then you may find the other Java client
[Jedis](https://redis.io/docs/latest/develop/clients/jedis/) easier to use.

The sections below explain how to install `Lettuce`

and connect your application
to a Redis database.

`Lettuce`

requires a running Redis server. See [here](https://redis.io/docs/latest/operate/oss_and_stack/install/) for Redis Open Source installation instructions.

##
Install
[
](https://redis.io#install)

To include Lettuce as a dependency in your application, edit the appropriate dependency file as shown below.

If you use Maven, add the following dependency to your `pom.xml`

:

```
<dependency>
<groupId>io.lettuce</groupId>
<artifactId>lettuce-core</artifactId>
<version>6.7.1.RELEASE</version> <!-- Check for the latest version on Maven Central -->
</dependency>
```

If you use Gradle, include this line in your `build.gradle`

file:

```
dependencies {
compileOnly 'io.lettuce:lettuce-core:6.7.1.RELEASE'
}
```

If you wish to use the JAR files directly, download the latest Lettuce and, optionally, Apache Commons Pool2 JAR files from Maven Central or any other Maven repository.

To build from source, see the instructions on the [Lettuce source code GitHub repo](https://github.com/lettuce-io/lettuce-core).

##
Connect and test
[
](https://redis.io#connect-and-test)

Connect to a local server using the following code. First, import the required classes.

```
import io.lettuce.core.*;
import io.lettuce.core.api.StatefulRedisConnection;
import io.lettuce.core.api.sync.RedisCommands;
public class ConnectBasicTest {
public void connectBasic() {
RedisURI uri = RedisURI.Builder
.redis("localhost", 6379)
.build();
RedisClient client = RedisClient.create(uri);
StatefulRedisConnection<String, String> connection = client.connect();
RedisCommands<String, String> commands = connection.sync();
commands.set("foo", "bar");
String result = commands.get("foo");
System.out.println(result); // >>> bar
connection.close();
client.shutdown();
}
}
```

Use the following code to connect to the server.

```
import io.lettuce.core.*;
import io.lettuce.core.api.StatefulRedisConnection;
import io.lettuce.core.api.sync.RedisCommands;
public class ConnectBasicTest {
public void connectBasic() {
RedisURI uri = RedisURI.Builder
.redis("localhost", 6379)
.build();
RedisClient client = RedisClient.create(uri);
StatefulRedisConnection<String, String> connection = client.connect();
RedisCommands<String, String> commands = connection.sync();
commands.set("foo", "bar");
String result = commands.get("foo");
System.out.println(result); // >>> bar
connection.close();
client.shutdown();
}
}
```

Test the connection by storing and retrieving a simple string.

```
import io.lettuce.core.*;
import io.lettuce.core.api.StatefulRedisConnection;
import io.lettuce.core.api.sync.RedisCommands;
public class ConnectBasicTest {
public void connectBasic() {
RedisURI uri = RedisURI.Builder
.redis("localhost", 6379)
.build();
RedisClient client = RedisClient.create(uri);
StatefulRedisConnection<String, String> connection = client.connect();
RedisCommands<String, String> commands = connection.sync();
commands.set("foo", "bar");
String result = commands.get("foo");
System.out.println(result); // >>> bar
connection.close();
client.shutdown();
}
}
```

Close the connection when you're done.

```
import io.lettuce.core.*;
import io.lettuce.core.api.StatefulRedisConnection;
import io.lettuce.core.api.sync.RedisCommands;
public class ConnectBasicTest {
public void connectBasic() {
RedisURI uri = RedisURI.Builder
.redis("localhost", 6379)
.build();
RedisClient client = RedisClient.create(uri);
StatefulRedisConnection<String, String> connection = client.connect();
RedisCommands<String, String> commands = connection.sync();
commands.set("foo", "bar");
String result = commands.get("foo");
System.out.println(result); // >>> bar
connection.close();
client.shutdown();
}
}
```

##
More information
[
](https://redis.io#more-information)

The [Lettuce reference guide](https://redis.github.io/lettuce/) has more examples
and an API reference. You may also be interested in the
[Project Reactor](https://projectreactor.io/) library that Lettuce uses.

See also the other pages in this section for more information and examples:
