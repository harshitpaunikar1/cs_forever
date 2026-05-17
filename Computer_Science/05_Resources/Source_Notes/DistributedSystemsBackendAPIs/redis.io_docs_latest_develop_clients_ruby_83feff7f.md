Title: redis-rb guide (Ruby) | Docs
Mapped Topic: Caching and in-memory data structures
Source URL: https://redis.io/docs/latest/develop/clients/ruby/
Source Type: official_docs
Trust Score: 94
Fetched At: 2026-04-17T07:09:05+00:00
Mapped From CSE.md Section: Part 2: E. Distributed systems, backend systems, APIs

# Content

# redis-rb guide (Ruby)

Connect your Ruby application to a Redis database

[redis-rb](https://github.com/redis/redis-rb) is the Ruby client for Redis.
The sections below explain how to install `redis-rb`

and connect your application
to a Redis database.

`redis-rb`

requires a running Redis server. See [here](https://redis.io/docs/latest/operate/oss_and_stack/install/) for Redis Open Source installation instructions.

##
Install
[
](https://redis.io#install)

To install `redis-rb`

, run the following command:

```
gem install redis
```

##
Connect and test
[
](https://redis.io#connect-and-test)

Connect to localhost on port 6379:

```
require 'redis'
r = Redis.new
r.set 'foo', 'bar'
value = r.get('foo')
puts value # >>> bar
r.hset 'user-session:123', 'name', 'John'
r.hset 'user-session:123', 'surname', 'Smith'
r.hset 'user-session:123', 'company', 'Redis'
r.hset 'user-session:123', 'age', 29
hash_value = r.hgetall('user-session:123')
puts hash_value
# >>> {"name"=>"John", "surname"=>"Smith", "company"=>"Redis", "age"=>"29"}
r.close()
```

Store and retrieve a simple string.

```
require 'redis'
r = Redis.new
r.set 'foo', 'bar'
value = r.get('foo')
puts value # >>> bar
r.hset 'user-session:123', 'name', 'John'
r.hset 'user-session:123', 'surname', 'Smith'
r.hset 'user-session:123', 'company', 'Redis'
r.hset 'user-session:123', 'age', 29
hash_value = r.hgetall('user-session:123')
puts hash_value
# >>> {"name"=>"John", "surname"=>"Smith", "company"=>"Redis", "age"=>"29"}
r.close()
```

Store and retrieve a dict.

```
require 'redis'
r = Redis.new
r.set 'foo', 'bar'
value = r.get('foo')
puts value # >>> bar
r.hset 'user-session:123', 'name', 'John'
r.hset 'user-session:123', 'surname', 'Smith'
r.hset 'user-session:123', 'company', 'Redis'
r.hset 'user-session:123', 'age', 29
hash_value = r.hgetall('user-session:123')
puts hash_value
# >>> {"name"=>"John", "surname"=>"Smith", "company"=>"Redis", "age"=>"29"}
r.close()
```

Close the connection when you're done.

```
require 'redis'
r = Redis.new
r.set 'foo', 'bar'
value = r.get('foo')
puts value # >>> bar
r.hset 'user-session:123', 'name', 'John'
r.hset 'user-session:123', 'surname', 'Smith'
r.hset 'user-session:123', 'company', 'Redis'
r.hset 'user-session:123', 'age', 29
hash_value = r.hgetall('user-session:123')
puts hash_value
# >>> {"name"=>"John", "surname"=>"Smith", "company"=>"Redis", "age"=>"29"}
r.close()
```

##
More information
[
](https://redis.io#more-information)

The
[GitHub repository](https://github.com/redis/redis-rb) for `redis-rb`

has a
set of [examples](https://github.com/redis/redis-rb/tree/master/examples)
and further information about using redis-rb.
