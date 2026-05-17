Title: node-redis guide (JavaScript) | Docs
Mapped Topic: Caching and in-memory data structures
Source URL: https://redis.io/docs/latest/develop/clients/nodejs/
Source Type: official_docs
Trust Score: 94
Fetched At: 2026-04-17T07:09:00+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

# node-redis guide (JavaScript)

Connect your Node.js/JavaScript application to a Redis database

[ node-redis](https://github.com/redis/node-redis) is the Redis client for Node.js/JavaScript.
The sections below explain how to install

`node-redis`

and connect your application
to a Redis database.[. See](https://redis.io/docs/latest/develop/clients/ioredis/)

`ioredis`

[Migrate from ioredis](https://redis.io/docs/latest/develop/clients/nodejs/migration/)if you are interested in converting an existing

`ioredis`

project to `node-redis`

.`node-redis`

requires a running Redis server. See [here](https://redis.io/docs/latest/operate/oss_and_stack/install/) for Redis Open Source installation instructions.

You can also access Redis with an object-mapping client interface. See
[RedisOM for Node.js](https://redis.io/docs/latest/integrate/redisom-for-node-js/)
for more information.

##
Install
[
](https://redis.io#install)

To install node-redis, run:

```
npm install redis
```

##
Connect and test
[
](https://redis.io#connect-and-test)

Connect to localhost on port 6379.

```
import { createClient } from 'redis';
const client = createClient();
client.on('error', err => console.log('Redis Client Error', err));
await client.connect();
await client.set('key', 'value');
const value = await client.get('key');
console.log(value); // >>> value
await client.hSet('user-session:123', {
name: 'John',
surname: 'Smith',
company: 'Redis',
age: 29
})
let userSession = await client.hGetAll('user-session:123');
console.log(JSON.stringify(userSession, null, 2));
/* >>>
{
"surname": "Smith",
"name": "John",
"company": "Redis",
"age": "29"
}
*/
await client.quit();
```

Store and retrieve a simple string.

```
import { createClient } from 'redis';
const client = createClient();
client.on('error', err => console.log('Redis Client Error', err));
await client.connect();
await client.set('key', 'value');
const value = await client.get('key');
console.log(value); // >>> value
await client.hSet('user-session:123', {
name: 'John',
surname: 'Smith',
company: 'Redis',
age: 29
})
let userSession = await client.hGetAll('user-session:123');
console.log(JSON.stringify(userSession, null, 2));
/* >>>
{
"surname": "Smith",
"name": "John",
"company": "Redis",
"age": "29"
}
*/
await client.quit();
```

Store and retrieve a map.

```
import { createClient } from 'redis';
const client = createClient();
client.on('error', err => console.log('Redis Client Error', err));
await client.connect();
await client.set('key', 'value');
const value = await client.get('key');
console.log(value); // >>> value
await client.hSet('user-session:123', {
name: 'John',
surname: 'Smith',
company: 'Redis',
age: 29
})
let userSession = await client.hGetAll('user-session:123');
console.log(JSON.stringify(userSession, null, 2));
/* >>>
{
"surname": "Smith",
"name": "John",
"company": "Redis",
"age": "29"
}
*/
await client.quit();
```

To connect to a different host or port, use a connection string in the format `redis[s]://[[username][:password]@][host][:port][/db-number]`

:

```
createClient({
url: 'redis://alice:
```[[email protected]](https://redis.io/cdn-cgi/l/email-protection):6380'
});

To check if the client is connected and ready to send commands, use `client.isReady`

, which returns a Boolean. `client.isOpen`

is also available. This returns `true`

when the client's underlying socket is open, and `false`

when it isn't (for example, when the client is still connecting or reconnecting after a network error).

When you have finished using a connection, close it with `client.quit()`

.

```
import { createClient } from 'redis';
const client = createClient();
client.on('error', err => console.log('Redis Client Error', err));
await client.connect();
await client.set('key', 'value');
const value = await client.get('key');
console.log(value); // >>> value
await client.hSet('user-session:123', {
name: 'John',
surname: 'Smith',
company: 'Redis',
age: 29
})
let userSession = await client.hGetAll('user-session:123');
console.log(JSON.stringify(userSession, null, 2));
/* >>>
{
"surname": "Smith",
"name": "John",
"company": "Redis",
"age": "29"
}
*/
await client.quit();
```

##
More information
[
](https://redis.io#more-information)

The [ node-redis website](https://redis.js.org/) has more examples.
The

[Github repository](https://github.com/redis/node-redis)also has useful information, including a guide to the

[connection configuration options](https://github.com/redis/node-redis/blob/master/docs/client-configuration.md)you can use.

See also the other pages in this section for more information and examples:
